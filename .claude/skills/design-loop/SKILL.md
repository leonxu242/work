---
name: design-loop
description: Takes a goal and a real-world reference, extracts what actually makes the reference good, then runs a builder and three fresh-context critics on every piece until all three agree ours wins. Token-hungry, so reserve it for a hero asset (landing page, flagship carousel), not a whole site. Triggers on "/design-loop", "design loop", "run the critic loop", "loop this against".
---

# Design Loop

Four phases: interview, preflight, teardown, loop. Do not skip ahead. Do not start building during phases 1 to 3.

The one thing to remember: a critic that shares memory with the builder is grading its own homework. Everything else here is detail.

## Phase 1: Interview

Ask exactly these three, together, then stop and wait.

1. What are you building, and how long or how big?
2. Name something that already does this brilliantly. A site, a video, a doc, anything I can open. If nothing comes to mind, say skip.
3. Any files I should work from? Design system, brand doc, script, existing draft.

If they name something vague ("Apple's website", "good SaaS design"), push once for the specific page or file. A vague bar is the number one reason this method fails: the critic invents a comparison and approves everything on round one.

If they say skip on question 2, propose three candidate bars, one line each on why, and wait. If they do not answer, take the hardest one.

If there is no `design-system.md`, say so and suggest exporting one (for example, ask Claude Design to write the project's design system out as a single `design-system.md`). Without it the System critic goes blind; see Phase 2.

## Phase 2: Preflight

A check, not a question. Run it before any work and report in one block.

- Fetch the bar now. Screenshot the URL or read the file. If it is blocked or missing, say so and ask for another.
- Confirm you can render our output: screenshots for a site, a filmstrip of frames for animation, a PDF render for a doc. No render means no craft critic.
- Name any generation tools the goal needs (image, video, voice) and confirm they are connected.
- Confirm the input files exist: design-system.md, brand doc, script.

Then print: what is working, what is missing, and **which critic goes blind** if something is missing. Never carry on quietly with a critic that cannot see.

## Phase 3: Teardown

Read the reference properly and write 5 to 7 mechanisms to `bar.md`.

Mechanisms, not adjectives. Adjectives are unfalsifiable; measurements are not.

| Useless | Checkable |
|---|---|
| Feels premium | Headline is 5x body size |
| Clean and modern | Three type sizes total, no more |
| Good use of whitespace | Whitespace above the fold is at least 40% of the frame |
| Strong visual hierarchy | One accent colour, used at most twice per screen |
| Smooth motion | Nothing animates for under 400ms; motion always resolves in one direction |

Every line must be something a critic can check by looking. Show `bar.md` to the user before continuing.

## Phase 4: Loop

Split the goal into the smallest pieces that can be improved and judged on their own. You choose the pieces. Keep it to three or four unless told otherwise, because every extra piece multiplies the run.

For each piece: fan out a builder, then three critics, each a separate subagent with fresh context and no knowledge of how the builder worked. Give critics only what their row below lists — never the builder's transcript, reasoning, or code.

| Critic | Judges against | Model | Why |
|---|---|---|---|
| **Brief** | The stated goal only. Does it do the thing? Ignore aesthetics. | `sonnet` | Simple judgment, no vision needed |
| **System** | `design-system.md` only. Objective adherence. | `haiku` | Mechanical adherence checking |
| **Craft** | `bar.md` and rendered output only. Put ours next to the reference blind with labels stripped, say which is better, name the single biggest gap. | Strongest available (`opus`) | Never downgrade this one. A cheap craft critic approves everything and the loop dies on round one. |

The three roles are fixed so they never converge into the same opinion; each can fail work the other two would pass. But write each critic's brief yourself, adapted to this specific goal ("does it hit the brief" means something different for an animation than for a pricing page). Do not reuse generic wording across different goals.

Rules:
- Critics are harsh. Praise is not useful.
- Critics judge rendered output, never the code. Reading the implementation makes a critic evaluate intent instead of result.
- Binary verdicts (PASS / FAIL), not scores. Scores drift upward every round.
- All three must pass. Any fail goes back to the builder with the single biggest gap named.
- No fixed round count. The exit is winning, or the user stopping the run.

Keep a live progress page updating as work evolves (for example `design-loop-progress.md`): piece status, each critic's verdict, gap history, round count.

## Cost

Every round is a build plus three judgments. It is genuinely token-hungry.

There is no reliable self-reported token cost, so do not pretend to show one. Show round count and elapsed pieces instead.

If the user names a ceiling, treat it as a checkpoint: pause and ask before continuing past it. Tell them plainly that the real controls, in order, are:
1. Them watching and stopping the run. They are the brake.
2. Capping the pieces to three or four (not the rounds).
3. Their weekly usage limit as the hard stop.

## What breaks this

- A vague bar. By far the most common failure.
- The builder judging its own work. Critics need fresh context.
- A soft critic. Binary job, not a score.
- A fixed round count. The exit is winning.
- Over-specifying. Every extra instruction is one fewer decision the model makes with its own judgment.
