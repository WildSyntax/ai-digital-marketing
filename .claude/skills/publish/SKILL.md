---
name: publish
description: Publish or schedule an approved content item through the right connector (Metricool for LinkedIn, Instagram, YouTube; local folder for blog until a host is connected) and move it to content/published/. Use when the owner says "publish <file>" or "publish all approved".
---

# Publish

Input: a path under `content/approved/`, or "all approved".
Output: file(s) moved to `content/published/<channel>/` with `published_url` and `published_at` set.

## Requires

- Library: not used. Publishing never calls a `marketing-skills:*` skill, so it works
  without the plugin.
- Connectors: `metricool` (required for linkedin, instagram, youtube).

## Guard

Normalise the path first (no `..` segments). Then require all of: the path is under
`content/approved/<channel>/`, it ends in `.md`, and its front matter has `status: approved`.
If any fails, reply exactly:
"Refusing: <path> is not in content/approved/. Approve it first with `approve <path>`."
and stop. Do nothing else.

Previous attempt check: if `published_url` is non-null or `publish_attempted` is non-null,
reply exactly:
"Refusing: <path> has a previous publish attempt (<published_url or publish_attempted>). Check Metricool for an existing post; say `publish <path> anyway` to retry."
and stop. Proceed only if the owner has explicitly said `publish <path> anyway`.

Placeholder check: scan the outgoing text (linkedin body; instagram caption and hashtags;
youtube title, description and tags; blog body) for `<...>` or `TODO:`. If found, reply exactly:
"Refusing: <path> still contains a placeholder: <text>. Fix it, then retry."
and stop, before any connector call.

## Steps per file

1. Read the file; take `channel`, `scheduled_for`, `title`, body sections.
2. Route by channel.

   **linkedin / instagram / youtube (Metricool):**
   a. Connector check: call `getBrandSettings` on the `metricool` connector. If the tool is
      unavailable or the call fails, reply "Metricool is not connected. Run /mcp, connect
      Metricool, then retry." and stop. Leave the file in place.
   b. Media and inputs check, before anything is written:
      - instagram: `image_url` must be an http(s) URL. If it is null or not http(s), ask the
        owner for a public image URL and stop until given.
      - youtube: if `video_file` is null, ask the owner for the video file path or URL and
        stop until given.
   c. Time: if `scheduled_for` is set, use it. Otherwise call `getBestTimeToPostByNetwork`
      for the network and use the next suggested slot after now; write it into
      `scheduled_for`.
   d. Build the post:
      - linkedin: text = the body between the front matter and the first `## ` heading
        (`## First comment`, `## Variants`). After scheduling, if `## First comment` is not
        "none", tell the owner to add it manually once the post is live (Metricool does not
        post first comments).
      - instagram: text = `## Caption` + blank line + `## Hashtags`; media = `image_url`.
      - youtube: title = title option 1, description = `## Description`, tags = `## Tags`;
        media = `video_file`.
   e. Before calling, set `publish_attempted: <ISO datetime>` in front matter and commit
      `content(<channel>): publish attempt <slug>`.
   f. Call `createScheduledPost` once with network, text, media, and the datetime. Never
      retry. If it returns an error, report it and stop; the file stays in approved with
      `publish_attempted` set. If the call times out or returns no clear result, do not call
      again. Tell the owner the post may exist, leave the file in approved/ with
      `publish_attempted` set, and stop.
   g. Immediately on success: set `published_url` (post URL, or the scheduled post id if no
      URL) and `published_at: <ISO datetime>`, and commit `content(<channel>): publish <slug>`
      so the URL is recorded before the move.

   **blog:**
   a. If no blog host connector is declared in `.mcp.json` (no `wordpress`, `notion`, or
      `webflow` key): local publish. Run the placeholder check, then set `published_url` to
      the new path under `content/published/blog/` and `published_at: <ISO datetime>`. Tell
      the owner the post is ready to paste into their CMS.
   b. If a host connector is declared: this branch is not yet written. Reply "Blog host
      connector <name> is declared but publish is not implemented for it yet; see
      docs/connectors.md" and stop.
3. Set `status: published`. `git mv` the file to `content/published/<channel>/`. For a blog,
   also run `grep -l "^source: <old path>" -r content/` and update each referencing file's
   `source` to the new path, in the same commit.
4. Commit `content(<channel>): move <slug> to published` (for the local blog branch, commit
   `content(blog): publish <slug>`; for Metricool items the URL was already committed in 2g).
5. Reply with the new path, the scheduled time, and `published_url`.

## "publish all approved"

Process every file matching `content/approved/*/*.md` in filename order, following the steps
above. A failure is any stop condition: a refusal, a connector not connected, a missing input,
or a call error. Stop at the first failure and report which files were published and which
were not.
