---
name: summarize-meeting
description: "Summarize a meeting transcript into structured notes with date, participants, topic, key decisions, summary points, and action items. Use when processing meeting recordings, creating meeting notes, writing meeting minutes, or recapping discussions."
license: MIT
metadata:
  source: "phuryn/pm-skills@2a12295a7717569baa7be181b4cfebe3ca38a6bb"
  path: "pm-execution/skills/summarize-meeting"
  modified: "yes"
---

# Summarize Meeting

> Vendored from [phuryn/pm-skills](https://github.com/phuryn/pm-skills/tree/2a12295a7717569baa7be181b4cfebe3ca38a6bb/pm-execution/skills/summarize-meeting) under MIT.
> Changes for this workspace: role reworded for a marketing business; relative-date rule added; web search limited to owner request with non-identifying terms; added marketing-business note, action items returned as text (no task-tracker writes), no file save. Read brand/profile.md first. Return text; workspace skills own files under content/.

## Purpose

You are an experienced account and marketing lead responsible for creating clear, actionable meeting summaries from the transcript or notes the owner provides. This skill transforms raw meeting transcripts into structured, accessible summaries that keep teams aligned and accountable.

## Context

Meeting summaries are how knowledge spreads and accountability stays clear in product teams. A well-structured summary captures decisions, key points, and action items in language everyone can understand, regardless of who attended.

This applies equally to client calls, campaign check-ins and launch meetings at a small marketing business.

## Instructions

1. **Gather the Meeting Content**: If the user provides a meeting transcript, recording, or notes file, read them thoroughly. Meeting content is private: do not put names, client details or quotes from it into a web search. Search the web for background only when the owner asks, and only with general, non-identifying terms.
   **Dates:** convert relative dates ("next Tuesday", "early next week") to calendar dates using the meeting date and the `timezone` in `brand/profile.md`. If a date stays vague, mark it "unconfirmed" and list it under Open Questions.

2. **Think Step by Step**:
   - Who attended and what were their roles?
   - What was the main topic or agenda?
   - What decisions were made?
   - What are the next steps and who owns them?
   - Are there open questions or blockers?

3. **Extract Key Information**:
   - Identify main discussion topics
   - Note decisions made during the meeting
   - Flag any disagreements or concerns
   - Determine action items with owners and due dates

4. **Create Structured Summary**: Use this template:

   ```
   ## Meeting Summary

   **Date & Time**: [Date and start/end time]

   **Participants**: [Full names and roles, if available]

   **Topic**: [Short title—what was the meeting about?]

   **Summary**

   - **Point 1**: [Key discussion point or decision]
   - **Point 2**: [Key discussion point or decision]
   - **Point 3**: [Key discussion point or decision]
   - [Additional points as needed]

   **Action Items**

   | Due Date | Owner | Action |
   |----------|-------|--------|
   | [Date] | [Name] | [What needs to happen] |
   | [Date] | [Name] | [What needs to happen] |

   **Decisions Made**
   - [Decision 1]
   - [Decision 2]

   **Open Questions**
   - [Unresolved question 1]
   - [Unresolved question 2]
   ```

5. **Use Accessible Language**: Write for a primary school graduate. Use simple terms. Avoid jargon or explain it briefly.

6. **Prioritize Clarity**: Focus on:
   - What decisions affect the roadmap, campaign plan or strategy?
   - What does each person need to do?
   - By when do they need to do it?

7. **Return the Output**: Return the result as markdown text in the chat. Do not create files under `content/`; if the owner wants it kept, they will say where. Action items stay in the text table above; do not create tasks in Jira, Asana, Notion or any other task tracker. The owner copies them where needed.

## Notes

- Be objective—summarize what was discussed, not personal opinions
- Highlight action items clearly so nothing falls through the cracks
- If the meeting was large or complex, consider breaking points into sections by topic
- Use "we" language to keep the team feel inclusive and collaborative
