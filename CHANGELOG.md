# Changelog

## 1.0.3

- **What's worth checking, in one place:** **Collect what's worth checking** (a button in the Review view's title bar, or the Command Palette) reads every step not read yet, one after another, and opens the **Worth checking** page: the model's checks and your comments, milestone by milestone and step by step, each with its `file:line`. The page fills in as each read finishes, and a step not yet read says whether it is being read, paused at the budget or failed.
  - Questions you ask meanwhile are answered first. **Stop the review's turn** ends collecting, and a restart doesn't resume it.
  - **Copy what's worth checking** copies the page as Markdown, as far as it has got, ready to paste into the PR. The button is also on the Markdown preview's title bar.
- **Each milestone page ends with what's worth checking** in its steps. When a milestone has no diagram but has checks or comments, a step's balloon links to that list.
- **About, milestone and Worth checking pages stay current:** an open page refreshes as reads finish and comments change.

## 1.0.2

- **Apply & check remaining steps:** right-click the current milestone or step in the Plan view (or use the Command Palette), and Guide Coding works through the milestone for you: it applies each step's code as soon as the model proposes it, checks it, and moves on to the next. The step and its milestone show "applying & checking" while it runs.
  - It stops at the checkpoint, and as soon as something needs you: a check that doesn't pass or finds no changes (the notice names the step), an Apply that fails, an error, a budget pause or a revised design brief.
  - Anything you do yourself also stops it: Apply, Check, asking the model, Done, or editing or skipping a step. **Stop apply & check** ends it at any time. A restart never resumes a run.
- **Text boxes keep their size:** a text box in the Task panel (the goal, a reply, the design brief's reply) that you made taller stays that tall when the panel is hidden and shown again.

## 1.0.1

- **A release, not a pre-release:** 1.0.0 was still packaged as a pre-release, so VS Code and the Marketplace called it one. 1.0.1 is the same Guide Coding as a release. If VS Code keeps you on pre-releases, choose **Switch to Release Version** on the extension's page.

## 1.0.0

**Stop Vibe Coding, enter Guide Coding.** Guide Coding is out of preview.

- **You write the code, the model guides you.** Give it a goal: it discusses it with you, writes a design brief for each milestone, and plans small steps that show up in the editor where the code belongs. You type each step, and **Check my work** reviews it. In Learn mode it never edits your files.
- **Review mode** walks you through a branch, a pull request, the last commit or your uncommitted changes, in an order that makes sense: what the change sets out to do, a sequence diagram per milestone, and each step's diff with what to check, bugs first. Your comments export for the PR.
- **Your model, your bill.** Use your own Claude Code (on your Claude plan), an Anthropic, OpenAI or DeepSeek key, or any OpenAI-compatible endpoint, local ones included. Where the price is known, the panel shows what a task costs, in dollars, or in tokens on a Claude plan.
- **The advisor** (with Claude Code) looks things up in your own tools, such as Jira or your wiki, and you approve each call.
- **Fix:** a review step opened beside About this review or a milestone's page no longer shows its file twice, which made VS Code log "Maximum call stack size exceeded" from the step's comment box.

## 0.7.4

- **The advisor in any turn:** with Claude Code (your installation), the model can now ask the advisor whenever it needs something your project doesn't have, such as a ticket from Jira, while planning a step, writing a brief or checking your work, not only while discussing the goal. You still approve each tool call it makes.

## 0.7.3

- **Review uncommitted changes:** "What to review" now offers **Uncommitted changes only** when you have some. It reviews your staged and unstaged edits and new files on their own, never mixed with commits.
  - The review works from a saved copy of the changes, so it stays put while you keep editing. Your files, staging area, branches and stash are left as they are.
- **The advisor, with Claude Code (your installation):** while you discuss a goal, the model can ask the advisor to look something up with your own MCP servers and claude.ai connectors, such as your issue tracker or wiki. Turn it on with `guide.claudeCode.extras` and `guide.advisor.enabled`.
  - You approve each tool call it wants to make.
  - It has no built-in tools, and it runs in an empty temporary folder outside your project, so it can't see your files.
  - Its cost and tokens count toward the task's totals.

## 0.7.2

- **Show the big picture on every milestone:** the button is now on every milestone in the Review view. A milestone without a diagram still opens its page, which says the model found no new or changed calls in it.
- **Fix:** the milestone page listed its steps from 2 (or another number) when earlier milestones had steps. Each step now says its number in the review, as in "Step 2/24".

## 0.7.1

- **The big picture in a review:** a milestone that adds or changes calls between parts of the code can now have a sequence diagram of those calls, drawn by the model from the change.
  - **Show the big picture** (the button on the milestone in the Review view) opens the milestone's page: its summary, the diagram and its steps. Each of its steps' comment boxes links to it too.
  - **About this review** shows every milestone's diagram.
  - It's the model's reading of the change, so check it against the code.
- **What a review has used:** the Review view's summary shows the review's cost when you pay per token, or its tokens on a Claude plan. Each step's tooltip shows what that step used.
- **Fix:** Sonnet 5.5's cache reads were counted at twice their price ($0.20 per million instead of $0.10).

## 0.7.0

- **A cleaner review:**
  - Code in the step's comment box gets your theme's code colour, and **Why** and **Worth checking** have icons.
  - Concerns are numbered, with short places like `Form.fs:42`, and **Draft a question** links name those numbers.
  - The step's title shows once, in the header.
  - Long text is no longer cut off with "…".
  - The Review view's summary is one line, and **What it sets out to do** is the first item in the list. Click it to open **About this review**, which shows that text in full, with your PR description and the commits.
- **Fix:** a starting point typed as `head~2` (lowercase) now counts from HEAD, like `HEAD~2`.

## 0.6.8

- **Clearer review start:** starting a review now asks "What to review (1 of 2)", then "What it's for (2 of 2, optional)", and each choice says what it means.
  - **Last commit only** is the first choice, showing that commit's message.
  - **Since a branch, tag or commit…** gives examples, such as `HEAD~3` for the last 3 commits.
  - The second question says it's optional and doesn't change which commits are reviewed.

## 0.6.7

- **A review step's diff shows only that step's changes:** when one file's changes are split across several steps, each step's diff shows only its own. The other steps' changes show as ordinary unchanged lines, and the tab title says "step 3 only".
  - The step's comment box says where else the file changes, for example "also changes in step 5", with a link to that step.
  - **⇄ All changes in this file** switches to the full diff, and back.

## 0.6.6

- **A more thorough review:** the model now looks for bugs first in each step. It reads the code around the change and the callers it affects, and tries the empty, failing and boundary cases.
  - Each step can now list up to 6 things worth checking instead of 3, most serious first. Before, anything past the third was lost.
  - A problem between two steps counts too, such as a test that doesn't cover the code it's for.
  - No step holds more than about 400 changed lines unless it's a single hunk, so a big file is read in several steps instead of one.

## 0.6.5

- **Apply & check my work:** right-click the current step in the plan to apply it and have it checked in one click, without opening the balloon. If the step can't be applied, nothing is checked.
- **Plainer writing:** the model now writes the brief and the step balloons the way a colleague would explain them. It says what a change does first, uses short sentences and explains unfamiliar names. The brief's **Why** starts with what you'll have once the milestone is done.
- **How much was cached:** the token count now shows the cached share of the input, e.g. `500k in (470k cached) · 1.3k out`. Cached input costs about a tenth of fresh input.

## 0.6.4

- **One change, several places:** a step that makes the same change in several places of one file (a string renamed at each use) is now one step that covers them all. Before, **Apply** changed only the first place.
  - **Show code** lists every place, **Preview** shows them all, **Apply** makes them all, and **↩ Unapply** takes them all back.
  - If one of the places changed since the step was proposed, Apply says which one, and **Re-locate** finds every place again.

## 0.6.3

- **Saving a key offers to switch:** **Guide: Set API key** now asks "Which provider's API key?". If you save a key for a provider you aren't using, it asks whether to use that provider now. It never switches without your click.
- **Tidier Claude Code (your installation):**
  - A long system prompt's temporary file is cleaned up after a crash.
  - Listing your conversations no longer waits on a slow `git worktree list` (5 s at most).
- **Upgrades keep their usage:** tasks saved before 0.6.0 keep loading, and token counts are kept across restarts.

## 0.6.2

- **Nothing you typed is lost before planning:** on the design brief, if you've typed a reply but not sent it, **✓ Plan the steps** (or **Re-plan**) asks first: **Send it first**, or **Plan without it**. Before, the typed text was silently ignored.
- **Open questions get an answer in the open:** when you choose **Make the plan** with questions left unanswered, the model now picks the simplest answer for each and lists it with the plan's assumptions ("Q: … → assumed: …"), so you can see and correct it before approving the brief. A note under **Make the plan** says how many are open.
- **A sent brief reply no longer stays in the reply box.**

## 0.6.1

- **Start from a Claude Code conversation:** with Claude Code (your installation), the New task panel's **Start from** lists this folder's Claude Code conversations, including those of its other git worktrees (marked), newest first. Each shows its title, or its first prompt. The task continues from a copy of the one you pick, so the guide knows what you already worked out; the conversation itself is never changed. Large conversations are marked. It's on by default; turn it off with `guide.claudeCode.extras`.

## 0.6.0

- **Claude Code (your installation):** a new provider that runs your own Claude Code, unmodified, with whatever it is signed in to: your Claude plan or an API key.
  - **Setup:** pick it with **Guide: Choose model provider**. Guide Coding has no login of its own and stores no credentials; sign in to Claude Code in a terminal with `claude`, then `/login`. It needs Claude Code 2.1.265 or later, from the native installer.
  - **Read-only:** Guide Coding's guard keeps the session read-only on top of your own Claude Code settings, deny rules and hooks, which keep applying. A turn whose tool calls are refused several messages in a row is stopped with a message saying why.
  - **Cost:** on a Claude plan the panel shows tokens, and a step's tooltip shows the API-equivalent cost, an estimate rather than a charge. On an API key or a cloud provider (Amazon Bedrock, Google Cloud Vertex AI, Microsoft Foundry), costs show in dollars and the budget applies. The panel says who is billed.
  - **Settings:** `guide.claudeCode.path` if `claude` lives somewhere unusual; `guide.claudeCode.anthropicApiKey` (`ignore` by default, so a stray `ANTHROPIC_API_KEY` doesn't bill you); `guide.claudeCode.plugins` to turn your Claude Code plugins off for guide sessions.
- **A model switch is safer:** a task that moves to a provider that bills you shows dollars and pauses at its budget again.

## 0.5.3

- **Imports come with the step:** an `open`, `using` or `import` the step's code needs is no longer a step of its own. The step brings it, the balloon lists it above the shape and the code, and Apply adds it with the file's other imports (after a multi-line import, under a `module`, `namespace` or `package` line, below a Python docstring), together with the code, in one edit Undo or ↩ Unapply takes back. Imports the file already has are left out. For F#, C#, TypeScript, JavaScript, Python, Java, Kotlin, Scala and Rust.

## 0.5.2

- **A design brief before the steps:** every task, and every milestone of a big one, starts with a short design brief in the Task panel: why it exists, the interfaces as signature-only snippets, a sequence diagram of the calls it adds, the planned steps with a one-line why each, and the trade-offs (pros, cons, and the alternative it rejected). Ask about it or ask for a change in its reply box; the model answers and revises it. **✓ Plan the steps** plans from the brief you approved.
- **When the code and the brief part ways:** if you ask for another design mid-milestone, or a change of plan, a fix or your own code departs from the brief, the model revises it and holds the steps. **✓ Re-plan the remaining steps** plans every unfinished step again from the code the done steps produced; **Keep the previous brief** carries on. **Compare with previous** shows both.
- **Syntax highlighting in your theme:** the brief's snippets and fenced code in the model's panel text are highlighted with VS Code's grammars, in your colour theme, and re-coloured when you switch themes.
- **One chat per step:** a step's questions and answers are one comment in its balloon, older exchanges folded. **Enter** sends a question (Shift+Enter starts a new line), and the reply box keeps only **Ask**. With VS Code's `comments.maxHeight` off, balloons grow and the editor follows the chat; the first answer offers once to turn it off.
- **↩ Unapply:** after Apply, ↩ Unapply puts the file back as it was (a file Apply created goes) and leaves the step to do. It refuses once you've edited the file since, so your edits are never lost.
- **Done asks first:** ✓ Works, next step and ✓ Done ask "Move on from step N?" before the step is finished.
- **Code in tooltips:** `code` in the Plan view's tooltips shows as code; nothing else in them is Markdown.

## 0.5.1

- **Scaffolding first:** a plan for a new project, or a folder with no project yet, starts with the solution, the project files and the test project, before any code file, so every step has a project to go into and builds.
- **A panel that lost the extension says so:** VS Code restarts the extension when the window switches workspaces, and a Task panel left open from before is no longer connected, so Reply did nothing. Now the panel says so within 10 s and asks you to reopen it from the Plan view. The model no longer suggests opening another folder or a multi-root workspace to reach files outside the workspace (the task is kept per workspace); it asks you to copy them in.

## 0.5.0

- **Review a branch:** the new **Review** view walks you through what a branch adds over a base, in a reading order the model proposes: milestones of steps, every change in exactly one step. Each step opens as a file or a diff, with what it does, why, and what's worth a closer look. It starts from the intent: add the PR description or ticket, and the review opens with what the change sets out to do and where the code differs. Checks on choices that may be deliberate are questions for the author, and one click drafts them as `question:` comments for you to edit. Mark steps reviewed, comment on any line (with `question:`, `issue:` or `nit:` labels), and export your comments as Markdown for the PR. Read-only: git is only run to read, and generated, binary and protected files are never sent to the model.
- **Skeleton first:** a plan now maps the shape of the work before filling it in: the types and signatures, then the failing tests (one test per step), then the implementations, then the wiring, so you see the architecture early. Steps are small, about 15 lines; in Learn mode a step over 30 lines is refused and split.
- **A step can delete lines:** a step can now replace or remove a whole range, and Preview and Apply refuse an edit that would change nothing, instead of showing an empty diff.
- **Nothing left out:** a step whose location hint asks for something its code doesn't add (an import, say) is refused and split, so Apply never skips an edit.
- **Answers first:** a remark in Ask is treated as a question and answered before anything else; a fix is shown as code for you to type.
- **Comments you can skim:** the code the model suggests carries short, plain comments, and a step's shape covers everything its code adds.
- **When nothing is wrong:** after **Something's wrong with this step…**, the model can report that it found nothing to fix, with its reason, and you can describe the problem again or carry on. A turn that fails now says what the model said and offers **Retry**.

## 0.4.4

- **Custom endpoints, by example:** the README shows what each setting means and two worked examples, a local model in LM Studio and a hosted OpenAI-compatible service.

## 0.4.3

- **Your key, safely:** the README says up front where your API key is kept and where it goes, how to give Guide Coding a key of its own with a spending cap, and that you can try it with no key through Ollama.

## 0.4.2

- **A short demo on the listing:** an animation at the top of the page shows a task from goal to plan to a checked step.

## 0.4.1

- **Claude Max and Team credits:** a tip in the README and in the Anthropic key box: these plans include monthly API credits, claimed by linking a Claude Console organization, and a key from that organization works here.
- **Listing link:** the Install section now links to the real Marketplace listing (Open VSX: coming soon).
- **Clearer icon:** the text cursor in the icon is now a plain bar, so it no longer reads as a capital "I" at small sizes.

## 0.4.0

The first Marketplace release, as **Guide Coding** (`novian.guide-coding`). The earlier `guide-preview` package was a local-only preview, so there is nothing to migrate: install this one.

- **Guide Coding:** you write the code, AI guides you step by step. The product has a new name, a new icon and a new listing page.
- **Model providers:** DeepSeek, Anthropic, OpenAI, OpenRouter, a local model through Ollama, or a custom OpenAI- or Anthropic-compatible endpoint (LM Studio, for one, needs no key). **Guide: Choose model provider** sets one up and checks the key for free.
- **Learn and Control modes**, step-by-step guidance with Hint, Ask, Show code, Preview, Apply and Check, milestones with checkpoints, Split step, Finish later, and Change of plan.
- **No telemetry.** Nothing is sent to the author. Your code goes only to the provider you choose; your keys stay in your operating system's keychain.
- **Needs VS Code 1.101.2 or later** and a folder you trust.
