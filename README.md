# ai-english-tutor

English | [简体中文](README.zh-CN.md)

An AI skill that turns a chat model into an English tutor that remembers. It reads your error log before every session, teaches one point at a time, drills you with short sets, grades every answer and gives a reason for each wrong one, and writes your mistakes, vocabulary and progress back to plain Markdown files.

Written for Claude (as a Skill). It should also work with any agent that can read a Markdown instruction file and edit files in a folder; I have only used it with Claude.

## The problem

Ask a chat model to "teach me English" and every session starts from zero. It explains a lot, tests little, forgets what you got wrong yesterday, and writes multiple-choice questions whose wrong options nobody would ever pick.

## What it does

- **Starts from your files.** Profile, error log and vocabulary list are read first; the session continues from "Next step".
- **Uses your own mistakes as the wrong options.** If you have written *dose has* or *did went*, those show up as distractors, so every question also trains you to spot your own errors.
- **Practice over lecture.** A short explanation with two examples per rule, then sets of about 8 questions, half multiple choice and half fill-in.
- **Grades properly.** Score, the full correct sentence for every question, and one line of why under every wrong answer.
- **Spaced review.** Learned items come back after 1, 3, 7, 14 and 30 days; a miss sends them back to day 1.
- **Recycles vocabulary.** Words you misspell or pick up from reading are worked into later questions until they have appeared 20 times; then it asks whether you still remember them.
- **Handles voice input.** A similar-sounding real word is treated as a speech-recognition slip, a non-word as your spelling.
- **Does not do your work for you.** No essays written for you, no model answers to memorise, no pretending its score estimate is a real result.
- **Checks its own questions.** A checklist for the ways AI-written questions go wrong: two correct options, missing time signals, answers always in the first slots, hints that point at the wrong form.

See an [example session](examples/session.md) and the [pitfalls from real use](skills/ai-english-tutor/references/pitfalls.md).

## Status

This is the working method I use every day to prepare for IELTS, written down after about three weeks of sessions. I have not taken the exam yet, so there is no score to prove it works. What I can stand behind is that every pitfall in here, and most of the rules, came from a real session where something went wrong and was fixed. The longer review intervals are standard spaced repetition and I have not been at it long enough to test them. I will add results when I have them.

## Install

**Claude Code:** copy `skills/ai-english-tutor/` into `~/.claude/skills/` (or your project's `.claude/skills/`).

**Claude apps:** zip the `ai-english-tutor` folder and upload it as a skill in Settings. The memory files need a place that persists, such as a Project or a connected folder.

**Other agents:** give the agent the whole `skills/ai-english-tutor/` folder and use `SKILL.md` as the instructions.

Then set up your memory files once:

1. Copy the four templates from `references/` into the folder you will study in, and rename them `learner-profile.md`, `error-log.md`, `vocab-list.md` and `back-translation.md`. Delete the rows marked `(example, delete)`. If you skip this step, the tutor creates the files in your first session.
2. Fill in the top of `learner-profile.md`: your goal, your native language, and a few facts about your life for example sentences.
3. Say: "Continue English."

The files are the memory. Keep them in the same place and start each session by pointing the agent at them.

## Files

```
skills/ai-english-tutor/
├── SKILL.md                              # Session flow, teaching, question writing, grading
└── references/
    ├── learner-profile-template.md       # Goal, level, route, scores, next step
    ├── error-log-template.md             # Mistakes by status + spaced-review schedule
    ├── vocab-list-template.md            # Words to recycle, with use counts
    ├── back-translation-template.md      # Paragraphs to translate back the next day
    └── pitfalls.md                       # What went wrong in real sessions, and the fix
examples/
└── session.md                            # A full practice-and-grading round (fictional learner)
```

## Notes

- The examples use Chinese as the learner's native language because that is mine. The skill itself is not tied to any language or exam.
- If you follow a grammar book's order of topics, the skill tells the model to write its own explanations and questions rather than copy the book.
- For exam preparation, use official past papers for real reading and listening practice. Passages written by a model are for building foundations.

## License

[MIT](LICENSE)
