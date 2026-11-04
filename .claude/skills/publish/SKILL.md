---
name: publish
description: Publish or schedule an approved content item through the right connector (Metricool for LinkedIn, Instagram, YouTube; local folder for blog until a host is connected) and move it to content/published/. Use when the owner says "publish <file>" or "publish all approved".
---

# Publish

Input: a path under `content/approved/`, or "all approved".
Output: file(s) moved to `content/published/<channel>/` with `published_url` set.

## Guard

If the path does not start with `content/approved/`, reply exactly:
"Refusing: <path> is not in content/approved/. Approve it first with `approve <path>`."
and stop. Do nothing else.

## Steps per file

1. Read the file; take `channel`, `scheduled_for`, `title`, body sections.
2. Route by channel.

   **linkedin / instagram / youtube (Metricool):**
   a. Check the `metricool` connector is connected by calling `getBrandSettings`. If the tool
      is unavailable or the call fails, reply "Metricool is not connected. Run /mcp, connect
      Metricool, then retry." and stop. Leave the file in place.
   b. Time: if `scheduled_for` is set, use it. Otherwise call `getBestTimeToPostByNetwork`
      for the network and use the next suggested slot after now; write it into
      `scheduled_for`.
   c. Build the post:
      - linkedin: text = the body between the front matter and `## First comment`.
        After scheduling, if `## First comment` is not "none", tell the owner to add it
        manually once the post is live (Metricool does not post first comments).
      - instagram: text = `## Caption` + blank line + `## Hashtags`; media = `canva_design_url`
        exported PNG. If `canva_design_url` is null, ask the owner for an image path or URL
        and stop until given.
      - youtube: title = title option 1, description = `## Description`, tags = `## Tags`;
        media = `video_file`. If `video_file` is null, ask the owner for the video file path
        or URL and stop until given.
   d. Call `createScheduledPost` once with network, text, media, and the datetime. Never
      retry. If it fails, report the error and stop; the file stays in approved.
   e. Set `published_url` to the post URL returned, or the scheduled post id if no URL.

   **blog:**
   a. If no blog host connector is declared in `.mcp.json` (no `wordpress`, `notion`, or
      `webflow` key): local publish. Set `published_url` to the new path under
      `content/published/blog/`. Tell the owner the post is ready to paste into their CMS.
   b. If a host connector is declared: this branch is not yet written. Reply "Blog host
      connector <name> is declared but publish is not implemented for it yet; see
      docs/connectors.md" and stop.
3. Set `status: published`. `git mv` the file to `content/published/<channel>/`.
4. Commit `content(<channel>): publish <slug>`.
5. Reply with the new path, the scheduled time, and `published_url`.

## "publish all approved"

Process every file under `content/approved/*/` in filename order, following the steps above.
Stop at the first failure and report which files were published and which were not.
