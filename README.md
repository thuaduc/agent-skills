# agent-skills

Skills for coding agents: Claude Code, Codex, Cursor, Gemini CLI, GitHub Copilot, Amp, Cline and the other agents that read `SKILL.md` files.

## Install

```bash
npx skills add thuaduc/agent-skills
```

It asks which agents to install to. To install for every agent on the machine, at user level:

```bash
npx skills add thuaduc/agent-skills -g --all
```

Get the latest version later with `npx skills update`.

## writing-clear-replies

Makes the agent write replies an engineer can read in one pass, between other work.

- **Problem and fix first.** A reply about a bug or a PR starts with what is broken and what the fix changes. Any other reply starts with the answer.
- **No private names.** Labels the agent made up during the session ("run B", "the 14", "E312") get explained or cut. Technical terms stay.
- **The same layout from every agent.** Fixed labels (Problem, Fix, Status, You, or Answer, Why, You), so you always know where to look.
- **60 to 250 words in chat.** Anything longer goes into a file, linked from the reply.

### Before and after

The same investigation, written by the same model.

**Before:**

> I checked `importer.py:212`, the worker logs and the `jobs` table. The retry policy wraps the batch in `db_retry` with `stop_after_delay(60)`; the primary's maintenance window ran 02:07 to 02:10, so attempt 2 hit `OperationalError` and the batch exited after the cutoff. Run B confirms the same pattern on the staging copy. 40 of 120 rows were not refreshed. Options: (a) raise the stop delay, (b) move the job, (c) add a resume cursor ...

**After:**

> **Problem:** Last night's price import stopped halfway, so 40 of the 120 bids still show yesterday's prices. The job retries, but only for 60 seconds, and the database restart took 3 minutes.
>
> **Fix:** The import now retries for up to 5 minutes when the database is briefly down.
>
> **Status:** Done and tested on a copy of last night's data: all 120 bids update. Not merged yet.
>
> **You:**
> 1. Review and merge the PR.
> 2. Start the import again from the Jobs page, so the 40 bids get today's prices.

### How it was tested

It was built from about 100 real moments where a developer pushed back on an agent's reply ("what is X?", "explain high level", "you cut it too much"). Each version was tested on real work sessions, with Claude Opus, Claude Fable and GPT models, against the same models with no skill:

- **Long replies got shorter:** Claude replies went from about 450 words to about 250, with the same facts and far fewer file and function names.
- **Short replies got clearer:** GPT replies stayed short, but now say what the problem was instead of only what changed.
- **Known limit:** a model sometimes keeps a label for its own test data (such as "gold labels") without explaining it.

## License

MIT
