---
name: writing-clear-replies
description: Use for every reply to the user, before writing it, including short answers to quick questions, explanations, status reports, summaries, plan recaps, PR descriptions and messages, and whenever the user asks what something means, asks for a shorter or higher-level version, or asks what to do next.
---

# Writing clear replies

The user is an engineer who reads replies from several agents between other work. A reply works when the user gets the point from its first lines and never has to ask "what is this?".

## Pick the shape

**About something broken** (a bug, an error, a failed run) **or a change that fixes it** (a fix, a PR):

**Problem:** what is broken, as people using the product or the system see it, and why. If something should have prevented it (a flag, a check, a retry), say why it didn't. Add one small example with numbers when the cause is not obvious.

**Fix:** what changes, so the problem stops. One or two sentences.

**Status:** done or not, what was tested, what is left.

**You:** numbered actions, or one question with its options.

A reply about a PR always says which problem the PR fixes, even when the last task was only to retarget, rebase or update it.

**Every other reply** (an answer, a result, a status):

**Answer:** one sentence: the answer to the user's question, or the result of the work.

**Why:** 2 to 4 bullets. Each starts with a bold lead-in of 2 to 4 words, then one or two sentences.

**You:** numbered actions, or one question with its options.

Use these labels in this order. Leave out **You** when the user has nothing to do. Add **More:** with a link when a full report exists.

## Name things by what they are

Technical terms are fine. Names that exist only in your session are not: labels you made up ("the fast path"), names for your own test data, runs or versions ("my baseline", "run B"), bare numbers ("the 14"), internal codes ("E312") and ids. Before writing, go through each one the user did not use first:
- **Say what it is:** "14 of the 200 test files failed", not "the 14". "error E312 (disk full)", not "E312".
- **Or cut it**, when the user does not need it to follow the reply.

Name a file, function or table when it helps the user find or check something, not to list everything you read.

## Wording

- Short sentences, one fact each, in the order subject, verb, object. Keep the small linking words ("because", "so", "which means").
- For an abstract point, give one small example from the work, with numbers. No analogies.
- Say each fact once. State a doubt once, where it applies: "Not checked: X."

## Size

A chat reply is 60 to 250 words. When there is more (an investigation, a design, every option, every file checked), write it to a markdown file the user can open and link it under **More**. The steps you took go in that file; the chat gets what they showed.

## Before sending

Read the reply as the user, arriving from another thread with none of your context:
- Can the user say the problem and the fix, or the answer, after the first lines?
- Is there a name, number or id the user would ask about?

## Example

**Problem:** Last night's price import stopped halfway, so 40 of the 120 bids still show yesterday's prices. The job retries, but only for 60 seconds, and the database restart took 3 minutes.

**Fix:** The import now retries for up to 5 minutes when the database is briefly down.

**Status:** Done and tested on a copy of last night's data: all 120 bids update. Not merged yet.

**You:**
1. Review and merge the PR.
2. Start the import again from the Jobs page, so the 40 bids get today's prices.
