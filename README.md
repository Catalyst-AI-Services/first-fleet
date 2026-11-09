# First fleet: a starter kit

Two AI agents in one folder: one does a job, one checks it. You answer their questions. This is the smallest version of how Catalyst runs its own agent fleet: a doer, a checker, and a human who only sees what needs a human.

The folder comes with a sample job: turn `meeting-notes.txt` into a one-page summary. Run it once as it is, then replace the brief and the notes with your own job.

## What you need

- [Claude Code](https://code.claude.com/docs/en/quickstart), version 2.1.224 or later, on macOS, Linux or WSL 2. Built-in messaging between sessions needs that version. Check with `claude --version`.
- [herdr](https://herdr.dev), a terminal workspace for coding agents. Install it with `brew install herdr` or the installer on herdr.dev.

## What's in the folder

| File | What it's for |
|---|---|
| `BRIEF.md` | The job: the goal, what done looks like, what's off limits. Write yours here. |
| `DOORS.md` | What can't be undone. The agents ask you before any of it. You decide the list. |
| `QUESTIONS.md` | Where the agents write a card when they need a decision from you. |
| `meeting-notes.txt` | The sample job's input. Replace it with your own. |
| `prompts/doer.txt`, `prompts/checker.txt` | The two opening prompts. |

The agents write `DONE.md` (what was done) and `CHECK.md` (what was checked). Those two files are your receipts.

## Run it

1. Open a terminal in this folder and run `herdr`.
2. Split the window into two panes (right-click, then split).
3. In the left pane, run `claude -n doer`. In the right pane, run `claude -n checker`. The `-n` name is how the two sessions find each other.
4. Paste `prompts/checker.txt` into the checker first. It names its pane and waits.
5. Paste `prompts/doer.txt` into the doer.

## What to expect

- **Permission prompts come to you.** Each agent asks before it runs its `herdr agent rename` line. Say yes. A message from the other agent never counts as your permission.
- **They talk by name.** When the doer finishes, it messages the session named `checker`: "ready for a check". The checker reads the brief and the work, writes `CHECK.md`, and either sends the doer what fails or tells you nothing fails. They loop until nothing fails. In herdr, either agent can also reach the other with `herdr agent prompt checker "..."`.
- **You don't relay.** Your job is to answer cards in `QUESTIONS.md` and the permission prompts.

A real run of this sample job, on 8 November 2026, took about a minute. It asked 2 permission prompts, both for the rename lines. The checker found nothing to fix on the first pass.

## Make it yours

Keep the first job small: something you could check yourself in ten minutes. Write the brief so a stranger could tell when it's done. Put anything you'd regret on the doors list. When one job works, add a second.
