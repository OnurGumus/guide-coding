# Changelog

## 0.5.3 (preview)

- **Imports come with the step:** an `open`, `using` or `import` the step's code needs is no longer a step of its own. The step brings it, the balloon lists it above the shape and the code, and Apply adds it with the file's other imports (after a multi-line import, under a `module`, `namespace` or `package` line, below a Python docstring), together with the code, in one edit Undo or ↩ Unapply takes back. Imports the file already has are left out. For F#, C#, TypeScript, JavaScript, Python, Java, Kotlin, Scala and Rust.

## 0.5.2 (preview)

- **A design brief before the steps:** every task, and every milestone of a big one, starts with a short design brief in the Task panel: why it exists, the interfaces as signature-only snippets, a sequence diagram of the calls it adds, the planned steps with a one-line why each, and the trade-offs (pros, cons, and the alternative it rejected). Ask about it or ask for a change in its reply box; the model answers and revises it. **✓ Plan the steps** plans from the brief you approved.
- **When the code and the brief part ways:** if you ask for another design mid-milestone, or a change of plan, a fix or your own code departs from the brief, the model revises it and holds the steps. **✓ Re-plan the remaining steps** plans every unfinished step again from the code the done steps produced; **Keep the previous brief** carries on. **Compare with previous** shows both.
- **Syntax highlighting in your theme:** the brief's snippets and fenced code in the model's panel text are highlighted with VS Code's grammars, in your colour theme, and re-coloured when you switch themes.
- **One chat per step:** a step's questions and answers are one comment in its balloon, older exchanges folded. **Enter** sends a question (Shift+Enter starts a new line), and the reply box keeps only **Ask**. With VS Code's `comments.maxHeight` off, balloons grow and the editor follows the chat; the first answer offers once to turn it off.
- **↩ Unapply:** after Apply, ↩ Unapply puts the file back as it was (a file Apply created goes) and leaves the step to do. It refuses once you've edited the file since, so your edits are never lost.
- **Done asks first:** ✓ Works, next step and ✓ Done ask "Move on from step N?" before the step is finished.
- **Code in tooltips:** `code` in the Plan view's tooltips shows as code; nothing else in them is Markdown.

## 0.5.1 (preview)

- **Scaffolding first:** a plan for a new project, or a folder with no project yet, starts with the solution, the project files and the test project, before any code file, so every step has a project to go into and builds.
- **A panel that lost the extension says so:** VS Code restarts the extension when the window switches workspaces, and a Task panel left open from before is no longer connected, so Reply did nothing. Now the panel says so within 10 s and asks you to reopen it from the Plan view. The model no longer suggests opening another folder or a multi-root workspace to reach files outside the workspace (the task is kept per workspace); it asks you to copy them in.

## 0.5.0 (preview)

- **Review a branch:** the new **Review** view walks you through what a branch adds over a base, in a reading order the model proposes: milestones of steps, every change in exactly one step. Each step opens as a file or a diff, with what it does, why, and what's worth a closer look. It starts from the intent: add the PR description or ticket, and the review opens with what the change sets out to do and where the code differs. Checks on choices that may be deliberate are questions for the author, and one click drafts them as `question:` comments for you to edit. Mark steps reviewed, comment on any line (with `question:`, `issue:` or `nit:` labels), and export your comments as Markdown for the PR. Read-only: git is only run to read, and generated, binary and protected files are never sent to the model.
- **Skeleton first:** a plan now maps the shape of the work before filling it in: the types and signatures, then the failing tests (one test per step), then the implementations, then the wiring, so you see the architecture early. Steps are small, about 15 lines; in Learn mode a step over 30 lines is refused and split.
- **A step can delete lines:** a step can now replace or remove a whole range, and Preview and Apply refuse an edit that would change nothing, instead of showing an empty diff.
- **Nothing left out:** a step whose location hint asks for something its code doesn't add (an import, say) is refused and split, so Apply never skips an edit.
- **Answers first:** a remark in Ask is treated as a question and answered before anything else; a fix is shown as code for you to type.
- **Comments you can skim:** the code the model suggests carries short, plain comments, and a step's shape covers everything its code adds.
- **When nothing is wrong:** after **Something's wrong with this step…**, the model can report that it found nothing to fix, with its reason, and you can describe the problem again or carry on. A turn that fails now says what the model said and offers **Retry**.

## 0.4.4 (preview)

- **Custom endpoints, by example:** the README shows what each setting means and two worked examples, a local model in LM Studio and a hosted OpenAI-compatible service.

## 0.4.3 (preview)

- **Your key, safely:** the README says up front where your API key is kept and where it goes, how to give Guide Coding a key of its own with a spending cap, and that you can try it with no key through Ollama.

## 0.4.2 (preview)

- **A short demo on the listing:** an animation at the top of the page shows a task from goal to plan to a checked step.

## 0.4.1 (preview)

- **Claude Max and Team credits:** a tip in the README and in the Anthropic key box: these plans include monthly API credits, claimed by linking a Claude Console organization, and a key from that organization works here.
- **Listing link:** the Install section now links to the real Marketplace listing (Open VSX: coming soon).
- **Clearer icon:** the text cursor in the icon is now a plain bar, so it no longer reads as a capital "I" at small sizes.

## 0.4.0 (preview)

The first Marketplace release, as **Guide Coding** (`novian.guide-coding`). The earlier `guide-preview` package was a local-only preview, so there is nothing to migrate: install this one.

- **Guide Coding:** you write the code, AI guides you step by step. The product has a new name, a new icon and a new listing page.
- **Model providers:** DeepSeek, Anthropic, OpenAI, OpenRouter, a local model through Ollama, or a custom OpenAI- or Anthropic-compatible endpoint (LM Studio, for one, needs no key). **Guide: Choose model provider** sets one up and checks the key for free.
- **Learn and Control modes**, step-by-step guidance with Hint, Ask, Show code, Preview, Apply and Check, milestones with checkpoints, Split step, Finish later, and Change of plan.
- **No telemetry.** Nothing is sent to the author. Your code goes only to the provider you choose; your keys stay in your operating system's keychain.
- **Needs VS Code 1.101.2 or later** and a folder you trust.
