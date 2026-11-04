# summarize-meeting test
Prompt: "Summarise this meeting."
Date: 2026-11-05
Result: PASS WITH ISSUES

Test setup: the skill was loaded by reading `.claude/skills/summarize-meeting/SKILL.md`, because the Skill tool returned `Unknown skill` in this session. The tester wrote 11 lines of fictional check-in notes, saved at
`/private/tmp/claude-501/-Users-himanshu25--claude-spares-spare-97jvgk/c9aef6d1-9353-4a3b-9c65-8ef1b46a10b1/scratchpad/tests/meeting_notes_campaign_checkin.txt`.

```
Campaign check-in, Tue 3 Nov 2026, 10:00-10:35 IST (video call)
Attendees: Priya (Northwind, account lead), Sam (Northwind, content), Dana (client, Head of Marketing, Bluebay Home Goods)
- Q4 "margin check" LinkedIn campaign week 3: 14 posts out, avg engagement 3.1% vs 2.5% target. Carousel on "best seller losing money" did best (6.8%).
- Blog traffic up 22% since launch, but only 4 data-review bookings vs goal of 10.
- Dana thinks the booking page asks too much; wants the form cut to name + email + store URL. Priya agreed.
- Sam proposed a 3-part email follow-up to blog readers. Dana OK but wants to see copy first.
- Paid boost: Dana asked to move 500 USD from Google search to LinkedIn boost of the carousel. Agreed, cap 500.
- Concern: holiday promo calendar not shared yet; Sam can't plan Dec posts without it.
- Actions: Priya to shorten booking form by Fri 6 Nov. Sam to draft email sequence by Tue 10 Nov.
- Dana to send holiday promo calendar "early next week". Priya to set up LinkedIn boost by Thu 5 Nov.
- Open: do we report bookings weekly or only at month end? Next check-in Tue 17 Nov.
```

Privacy check: no web search or other external tool was used. The notes had everything needed, and the owner did not ask for background research, which matches SKILL.md line 28. Names and the client name went nowhere outside this file.

---

## Meeting Summary

**Date & Time**: Tuesday 3 November 2026, 10:00-10:35 IST (video call)

**Participants**: Priya (Northwind, account lead), Sam (Northwind, content), Dana (Bluebay Home Goods, Head of Marketing)

**Topic**: Week 3 check-in on the Q4 "margin check" campaign

**Summary**

- **LinkedIn is ahead of target**: 14 posts so far, with average engagement of 3.1% against a 2.5% goal. The "best seller losing money" carousel did best at 6.8%.
- **Blog traffic is up, but bookings are behind**: traffic rose 22% since launch, but only 4 people booked a data review. The goal is 10.
- **The booking form is likely the problem**: Dana thinks it asks for too much. We agreed to cut it to three fields: name, email and store URL.
- **Email follow-up**: Sam suggested 3 emails to blog readers. Dana is happy to go ahead once she has seen the copy.
- **Budget move**: $500 moves from Google search ads to boosting the LinkedIn carousel, capped at $500.
- **Blocker**: Sam cannot plan December posts until Bluebay shares its holiday promo calendar.

**Action Items**

| Due Date | Owner | Action |
|----------|-------|--------|
| Thu 5 Nov 2026 | Priya | Set up the LinkedIn boost for the carousel ($500 cap, moved from Google search) |
| Fri 6 Nov 2026 | Priya | Cut the booking form to name, email and store URL |
| Tue 10 Nov 2026 | Sam | Draft the 3-part email sequence and send it to Dana for review |
| Week of 9 Nov 2026 (said "early next week"; no fixed date) | Dana | Send the holiday promo calendar to Sam |
| Tue 17 Nov 2026 | All | Next check-in |

**Decisions Made**
- The booking form drops to three fields (name, email, store URL).
- $500 moves from Google search to a LinkedIn boost of the top carousel.
- The email sequence goes ahead, subject to Dana approving the copy.

**Open Questions**
- Do we report bookings every week, or only at month end?
- When exactly will the holiday calendar arrive? December planning waits on it.

---

## Tester's judgement

The skill worked: the template covers everything a client check-in needs, and the privacy rule at line 28 is clear and was followed. The output is plain and uses no banned phrases. Brand tone (clear, confident, warm) fits the skill's plain-language rule.

Issues:
1. **`$ARGUMENTS` placeholder.** SKILL.md line 18 says "from $ARGUMENTS". That only gets filled in when the skill runs as a slash command with arguments. When it is triggered from plain chat ("Summarise this meeting"), the literal text `$ARGUMENTS` is left in the instructions. Fix: "from the transcript or notes the owner provides".
2. **Product-manager role and wording.** Line 18 ("experienced product manager"), line 22 ("product teams") and line 80 ("roadmap") come from the source repo. Line 24 adds a marketing note, but the role still does not fit a marketing business. Fix: line 18, "You are an experienced account or marketing lead"; line 22, "teams and clients".
3. **No rule for vague or missing due dates.** The notes said "early next week". The skill does not say whether to turn this into a date, mark it as uncertain, or list it under Open Questions. Fix: add to step 3 (around line 41): "Convert relative dates to calendar dates using the meeting date. If a date is vague or missing, write it as given, mark it unconfirmed, and add it to Open Questions."
4. **Section order.** The template (lines 61-74) puts Action Items before Decisions Made. Decisions usually explain the actions, so readers may expect them first. This is minor and a matter of style.
5. **The profile timezone is not used.** SKILL.md says "Read brand/profile.md first", but nothing tells the skill to use `timezone` (Asia/Kolkata) when a meeting time has no zone. Here the notes gave IST, so there was no problem. Fix (optional): "If the time has no zone, assume the profile `timezone` and say so."
6. **Skill not registered in this session.** The Skill tool returned `Unknown skill: summarize-meeting`. This is probably a stale session skill list. Check it in a fresh session.
