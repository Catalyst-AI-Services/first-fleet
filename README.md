# First fleet: a starter kit

Two AI agents in one folder: a builder does a job, a reviewer checks it. You answer their questions. This is the smallest version of how Catalyst runs its own agent fleet: one agent builds, one reviews, and the human sees only what needs a human.

The folder comes with a sample job: turn `meeting-notes.txt` into a one-page summary. Run it once as it is, then replace the brief and the notes with your own job.

## What you need

- **The Herdr app** ([herdr.dev](https://herdr.dev), free and open source). It's a desktop app for running coding agents. They keep working when you close the window. Download it for Mac, or run the one-line installer from [herdr.dev/download](https://herdr.dev/download) (macOS, Linux, Windows). It comes with `hc`, the command that starts and connects agents.
- **[Claude Code](https://code.claude.com/docs/en/quickstart)**, version 2.1.224 or later. Built-in messaging between sessions needs that version. Check with `claude --version`.

## What's in the folder

| File | What it's for |
|---|---|
| `BRIEF.md` | The job: the goal, what done looks like, what's off limits. Write yours here. |
| `DOORS.md` | What can't be undone. The agents ask you before any of it. You decide the list. |
| `QUESTIONS.md` | Where the agents write a card when they need a decision from you. |
| `meeting-notes.txt` | The sample job's input. Replace it with your own. |
| `prompts/builder.txt`, `prompts/reviewer.txt` | The two opening prompts. |

The agents write `DONE.md` (what was built) and `REVIEW.md` (what was checked). Those two files are your receipts.

## Run it

1. Open Herdr, and open a terminal in this folder.
2. Start the two agents, one name each:

   ```sh
   hc run --bg --name reviewer claude -n reviewer
   hc run --bg --name builder claude -n builder
   ```

   Each name works twice: Claude Code's messaging finds the session by its `-n` name, and Herdr finds the terminal by its `--name`.
3. Open the reviewer, paste `prompts/reviewer.txt`, and press Enter. It waits.
4. Open the builder, paste `prompts/builder.txt`, and press Enter.

## What to expect

- **They talk by name.** When the builder finishes, it messages the session named `reviewer`: "ready for review". The reviewer reads the brief and the work and writes `REVIEW.md`. Then it either tells the builder what fails or tells you nothing fails. They loop until nothing fails. Either agent can also reach the other through Herdr with `hc send reviewer "..."`.
- **Permission prompts come to you.** An agent asks before it runs a command, including `hc send`. A message from the other agent never counts as your permission.
- **You don't relay.** Your job is to answer cards in `QUESTIONS.md` and the permission prompts.

A real run of this sample job in the Herdr app, on 8 November 2026, took about a minute. The builder messaged the reviewer through Herdr, the reviewer found nothing that fails the brief (and flagged two trivial slips that don't), and there were two permission prompts.

## Make it yours

Keep the first job small: something you could check yourself in ten minutes. Write the brief so a stranger could tell when it's done. Put anything you'd regret on the doors list. When one job works, add a second.
