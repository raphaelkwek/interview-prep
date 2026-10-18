# interview-prep

A plugin for Claude (Cowork and Claude Code) that sends parallel research agents out to work out **what your interview is likely to test**, then puts what they find into a single prep brief and runs mock interviews from it.

## Using it

Just ask in plain language:

- "Prep me for my Senior Backend Engineer onsite at Stripe. Here's the job posting: <link>. Interviewers are Jane Doe and John Smith."
- "Give me a mock behavioural interview."

Or use the skills directly: `/interview-prep:prep` and `/interview-prep:mock`.

### Prep

Up to five agents run at the same time:

| Agent | Looks for |
|---|---|
| `process-scout` | Rounds, formats, and the bar, from Glassdoor, Blind, Reddit, and official hiring pages |
| `question-hunter` | Questions candidates actually reported being asked |
| `role-analyst` | Job description → testable topics and depth; resume gap analysis |
| `company-intel` | Products, news, values, tech stack; talking points and questions to ask |
| `interviewer-profiler` | Public *professional* background of named interviewers (runs only if you give names) |

The results are cross-referenced and saved as `interview-prep/<company>-<role>.md`. The brief includes a ranked list of likely topics with confidence levels, questions to practise (reported ones are starred), a study plan, and sources.

Tip: attach your resume or put it in your working folder to get the gap analysis.

### Mock

Runs a mock interview against the brief, one question at a time with realistic follow-ups, then scores your answers and adds notes to the brief.

## Install

**Cowork (Claude desktop app):** upload [`dist/interview-prep.plugin`](dist/interview-prep.plugin) from this repo.

**Claude Code (terminal):**

```sh
claude plugin marketplace add raphaelkwek/interview-prep
claude plugin install interview-prep@raphael-plugins
```
