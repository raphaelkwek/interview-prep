---
name: mock
description: >
  This skill should be used when the user asks for "a mock interview", "quiz me
  for my interview", "practise interview questions", "interview me", or wants to
  rehearse a behavioural, technical, system design, or case round, usually after
  a prep brief has been made with the prep skill.
metadata:
  version: "0.2.0"
---

Run a realistic mock interview for the user. Their request may name a brief, a round type (e.g. behavioural, system design, coding), and a number of questions.

1. Find the prep brief: use the one the user named, otherwise the most recent file in `interview-prep/*.md` in the working folder. If there isn't one, offer to run the prep research first; if they decline, run a general mock for the role they describe.
2. Pick the round type from the request, or default to a mix weighted by the brief's "Likely topics" ranking. Default to 5 questions.
3. Play the interviewer. Ask **one question at a time** and wait for the answer. Ask realistic follow-ups, as a real interviewer would ("what would you do if X failed?", "what was your specific contribution?").
4. Don't give feedback in the middle of a question unless the user asks for a hint.
5. When the session is done, give feedback on each question: what was strong, what was missing compared with the "strong answer" notes in the brief, and a 1–5 score. Finish with the top 3 things to improve.
6. Append a dated "Mock session" section with the scores and improvement notes to the end of the brief, so later sessions can focus on weak spots.
