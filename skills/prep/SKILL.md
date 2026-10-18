---
name: prep
description: >
  This skill should be used when the user asks to "prep me for my interview",
  "research my interview at <company>", "what will they ask me", "help me prepare
  for an interview", or mentions an upcoming interview, phone screen, or onsite
  and wants to know what it will test. It sends parallel research agents out and
  writes a prep brief.
metadata:
  version: "0.2.0"
---

Run an interview-prep research operation for the user. Their request and any details they gave (company, role, job posting, stage, interviewer names) are in the conversation.

## Step 1: Collect the essentials

From the request, pull out:
- **Company** (required)
- **Role / title / level** (required)
- **Job description**: a URL (fetch it with WebFetch), a file path (Read it), or pasted text. Strongly preferred.
- **Interview stage**: recruiter screen, technical phone screen, take-home, onsite/loop, final, or unknown
- **Interviewer names**, if known
- **The user's resume or background**: check the conversation and any uploaded files, then look for `resume*`, `cv*`, or `*.pdf` in the working folder. Optional.

If the company or role is missing, ask with AskUserQuestion. Don't ask about anything else; carry on with what you have and note the gaps.

## Step 2: Send the research agents out in parallel

Launch these subagents **in a single message so they run at the same time**. Give each one the full context from Step 1, including the complete job description text.

1. `interview-prep:process-scout`: how this company runs interviews for this role (rounds, formats, timing, bar), from candidate reports.
2. `interview-prep:question-hunter`: specific questions candidates say they were asked at this company for this role or similar ones.
3. `interview-prep:role-analyst`: breaks the job description down into the skills and topics that will be tested and how deeply.
4. `interview-prep:company-intel`: products, strategy, recent news, values, tech stack, and culture signals that interviewers often probe ("why us?", product sense, values questions).
5. `interview-prep:interviewer-profiler`: **only if interviewer names were given.** Looks at their public professional background so the user can guess what each of them will focus on.

## Step 3: Combine the findings

Once every agent has reported back, cross-reference what they found. A topic that several independent sources point to ranks higher. Mark anything that rests on a single anecdote as low-confidence. Never present a guess as a confirmed fact.

Write the brief as `interview-prep/<company-slug>-<role-slug>.md` in the user's working folder (in Cowork, the outputs folder) using this structure:

```markdown
# Interview Prep: <Role> at <Company>
_Stage: <stage> · Researched: <today's date>_

## TL;DR: The 5 things most likely to come up
(ranked, each with a confidence level (High/Med/Low) and a one-line reason)

## The interview process
(rounds, format, length, who you meet, what each round assesses)

## Likely topics, ranked
| Topic | Likelihood | Evidence | How deep to go |

## Questions to practise
### Technical / domain
### Behavioural (mapped to company values)
### Company / "why us"
(Mark questions candidates actually reported with ⭐. For each, add a short note on what a strong answer covers.)

## Company talking points
(recent news, products, strategy: things to mention that show you've done your homework)

## Your interviewers
(only if profiled)

## Gaps between you and the role
(only if a resume was available: where the user is weaker and how to frame it)

## Questions to ask them
(5–8 sharp questions based on the research)

## Study plan
(prioritised by likelihood × weakness, sized to the time left if known)

## Sources
(every URL the agents relied on)
```

## Step 4: Report back

Give the user a link to the brief, the TL;DR list, and a reminder that they can say "give me a mock interview" to practise against it.
