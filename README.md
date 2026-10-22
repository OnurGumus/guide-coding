# Guide Coding

**No more vibe coding. Enter Guide Coding.**

You write the code. AI guides you, one step at a time.

![Guide Coding in VS Code: type a goal, get a plan of small steps, write each step yourself, and the AI reviews your attempt](https://raw.githubusercontent.com/OnurGumus/guide-coding/main/images/guide-coding-demo.gif)

Guide Coding is a VS Code extension that plans a coding task with the model of your choice and then walks you through it. It does not write the code for you. Each step shows up in the editor, right where the code belongs: what to do, why, and where.

- **The human writes, the AI guides.** The model plans, explains, hints and reviews. You type.
- **Understanding is the goal.** You finish a task knowing why the code is the way it is, not only holding code that works.
- **Generating code is a choice, not the default.** Show code, Preview and Apply are there when you want them, one level at a time.

Your API key stays in your operating system's keychain and goes only to the provider you pick; nothing is sent to us. Want to try it without a key? Use a local model through Ollama, and nothing leaves your machine.

> **Preview.** Guide Coding is an early release. It works, but expect rough edges. Please [tell us what breaks](#feedback).

## Install

Search for **Guide Coding** in the Extensions view (publisher `novian`), or install it from the [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=novian.guide-coding) (Open VSX: coming soon). Then open a folder you trust, and open **Guide Coding** in the activity bar.

## Choose a provider

Guide Coding runs on your own model account. On first run, choose **Choose provider** (or run **Guide: Choose model provider**), pick one, and paste its API key. The key is checked for free (it only asks for the provider's model list), then stored in your operating system's keychain.

| `guide.provider` | Your code is sent to | You need |
|---|---|---|
| `deepseek` | api.deepseek.com | a DeepSeek API key |
| `anthropic` | api.anthropic.com (Claude models) | an Anthropic Console API key |
| `openai` | api.openai.com | an OpenAI API key; you pick the model at setup |
| `openrouter` | openrouter.ai, and the vendor of the model you pick | an OpenRouter key; you pick the model at setup |
| `ollama` | nowhere: the model runs on your machine (localhost:11434) | no key; you pick one of your installed models |
| `custom` | the endpoint in `guide.baseUrl` | optional: a local server such as LM Studio takes no key |
| `claudeCodeCli` | Anthropic, through your own Claude Code | Claude Code installed and signed in: your Claude plan or a key ([below](#claude-code-your-installation)) |

- **Anthropic with Claude Max or Team.** Have Claude Max or Team? Your plan includes monthly API credits (Max 5x $100, Max 20x $200, Team up to $500 pooled). Claim them in claude.ai under Settings → Billing by linking a Claude Console organization, create an API key in that organization, and choose Anthropic. (Pro, Free and Enterprise plans don't include these credits.) [Details](https://support.claude.com/en/articles/17154008-api-credits-for-max-and-team-plans).
- **Ollama and context length.** Ollama's default context is 4k tokens on machines with less than 24 GiB of VRAM, and it silently cuts long prompts from the front. Guide Coding needs at least 32k. Raise it with the Ollama app's context slider, or set `OLLAMA_CONTEXT_LENGTH` (64k, `65536`, is a good choice for coding tools). Pick a model that can call tools, for example `ollama pull qwen3-coder`.
- **Cost.** For a model whose price is known (Anthropic's, DeepSeek's) the cost is shown in dollars, and the task pauses at `guide.maxTaskCostUsd` (default 5). For any other model, each turn's tokens are written to the log instead.

### Claude Code (your installation)

Have Claude Code installed? Pick **Claude Code (your installation)**, and Guide Coding runs your own `claude`, unmodified, with whatever it is signed in to: your Claude plan or an API key.

- **What it needs.** Claude Code 2.1.265 or later, installed with the [native installer](https://code.claude.com/docs/en/setup). On Windows that is the native `claude.exe`, not npm's `claude.cmd`. Sign in in a terminal: run `claude`, then `/login`. If it lives somewhere unusual, set `guide.claudeCode.path`.
- **Guide Coding stores no credentials.** It has no login of its own and never reads Claude Code's sign-in; Claude Code signs in as it always does. Anthropic bills the usage to the account Claude Code uses.
- **A plan shows tokens.** On a Claude plan the panel shows tokens, and a step's tooltip shows the API-equivalent cost, which is an estimate, not a charge. The budget doesn't pause the task.
- **An API key in your environment.** If `ANTHROPIC_API_KEY` is set, Guide Coding leaves it out by default so that your plan is used (`guide.claudeCode.anthropicApiKey` is `ignore`). Set it to `use` to bill the key instead: costs then show in dollars, and the budget applies.
- **Start from a Claude Code conversation.** In the New task panel, **Start from** lists this folder's Claude Code conversations, its other git worktrees' included (marked), newest first. The task continues from a copy of the one you pick, so the guide knows what you already worked out; the conversation itself is never changed. Turn it off with `guide.claudeCode.extras`.
- **Your Claude Code settings apply.** Your permissions, deny rules and hooks work as they do in Claude Code, and Guide Coding's read-only guard comes on top. Your plugins run too; if they pull the guidance off course, set `guide.claudeCode.plugins` to `false`.

### A custom endpoint

Any server that speaks the OpenAI Chat Completions API or Anthropic's Messages API works. Add three settings to your user settings (**Preferences: Open User Settings (JSON)**), then run **Guide: Choose model provider** and pick **Custom endpoint**:

- `guide.baseUrl`: the API's base address. For the `openai` shape it ends just before `/chat/completions`, usually with `/v1`; for the `anthropic` shape it ends just before `/v1/messages`. It must be HTTPS, or plain HTTP only to `localhost` or `127.0.0.1`: nothing is ever sent over plain HTTP to another machine.
- `guide.apiShape`: `openai` or `anthropic`.
- `guide.model`: the model's id exactly as the endpoint names it. Pick a model that can call tools: the guide works through tool calls.

A local model in LM Studio, with no key, so nothing leaves your machine (start LM Studio's server, and copy the model's API identifier from its Developer tab):

```json
"guide.baseUrl": "http://localhost:1234/v1",
"guide.apiShape": "openai",
"guide.model": "qwen/qwen3-coder-30b"
```

Leave the key box empty when it asks.

A hosted OpenAI-compatible service, Groq for example:

```json
"guide.baseUrl": "https://api.groq.com/openai/v1",
"guide.apiShape": "openai",
"guide.model": "<a model id from Groq's model list>"
```

Paste the service's key when asked; it is stored in your keychain and sent only to that host. The cost of a custom endpoint is not shown in dollars: each turn's tokens are written to the log instead.

### Your key, safely

- **Where it lives.** Keys are stored in your operating system's keychain (VS Code's secret storage), one per provider, and each is sent only to its own provider. Guide Coding has no server of its own and no telemetry.
- **Give it a key of its own, with a cap.** Create a key just for Guide Coding and limit what it can spend: DeepSeek is prepaid, so your balance is the cap; OpenRouter keys take a credit limit; Anthropic Console workspaces and OpenAI projects take spend limits. Revoke the key at your provider whenever you like.
- **Change or remove it.** **Guide: Set API key** replaces a key, and **Guide: Clear API key** deletes it from the keychain.

## Your first task

1. Open a folder, then choose **Start a task** in the Guide Coding view and say what you want to build.
2. The model reads your code (read-only) and proposes a plan. For a bigger goal, the plan is split into **milestones**, each a slice that runs and shows something. The next milestone is planned only once you reach it, from the code as it is by then.
3. The current step appears in the editor. **Type it yourself**, then choose **Check my work**: the model reviews what you changed.
4. Stuck? Go one level further at a time:
   - **Hint**: the shape of the code
   - **Ask**: ask the model about the step, in the step's own balloon
   - **Show code**, **Preview** (a diff of the file with the step applied) and **Apply** (one undoable edit)
5. At the end of a milestone, a checkpoint asks you to try what you built before moving on.

You own the plan: edit, skip, reorder, add and delete steps, and the model adapts. Two more tools for when a step does not fit:

- **Split step** replaces the current step with smaller ones.
- **Finish later** keeps your stub for now; a later step finishes it.

### Learn or Control

- **Learn** (the default) explains first: why the step is needed, how it works, where it goes.
- **Control** is terse and shows the code at once, for when you know the ground and want the model out of your way.

Switch any time from the Guide Coding view's title bar, or with the `guide.mode` setting.

## Review a branch

PRs have got too big to review well. **Review** reads what a branch adds over a base, proposes an order to read it in, and walks you through it. It helps you understand the change; you do the judging. It's read-only: it never writes to your files or your repository.

1. Check out the branch (for a GitHub PR, `gh pr checkout 123`), then choose **Start a review** in the **Review** view, under Plan.
2. Pick the base: the default branch is offered first, or enter any branch, tag or commit. The review covers what the branch adds over it, like a PR. Uncommitted changes aren't included.
3. **Start from the intent.** Optionally add the PR description or ticket, from the clipboard or typed. The review opens with what the change sets out to do, and where the code does more, or less, than the description says.
4. The model groups the changes into **milestones** of **steps** in reading order: types and contracts first, then the code, the callers and the tests, with mechanical changes such as renames on their own. Every change is in exactly one step, so nothing is skipped by accident.
5. **Each step opens where its code is:** as a file when it only adds code (the new lines marked in green), as a diff when it changes or removes lines. **Open as diff / Open as file** switches.
6. **The balloon** says what the part does and why, and up to three specific things worth a closer look, each at `file:line`. Where a choice may be deliberate, a check is a question for the author, not a verdict, and **✎ Draft as a question** turns it into a `question:` comment for you to edit. Ask the model about the step, or save a note as a comment on it.
7. **Mark reviewed** moves on to the next step, and the view counts what you've covered (`12/31 steps · 640/2,300 lines reviewed`).
8. **Comment on any line** with the comment "+" in the gutter, on either side of a diff. Start a comment with `question:`, `issue:` or `nit:` to label it. **Export review** opens your comments as Markdown, ready to paste into the PR. Nothing is posted anywhere.

Reviews are kept per branch, so you can stop and come back. When the branch gets new commits, **Review the new commits** reviews just those. Generated files (lockfiles, `dist/`, minified files), binary files and protected files such as `.env` are listed for you, but never sent to the model. Git is only ever run to read: Guide Coding never fetches, checks out or commits.

## Privacy

Guide Coding collects nothing and sends nothing to its author; it has no telemetry. Your goal, the files the model reads, the diff of your changes when you Check, and your messages go only to the model provider you chose, under that provider's terms (with Ollama they stay on your machine; with Claude Code (your installation), to Anthropic through your own Claude Code, under your account's terms). The model can read your workspace but cannot change it: only your Apply and Create file write, and a path guard keeps it out of anything outside the folder and secrets such as `.env*`, `*.pem` and `.ssh`. Your keys live in your keychain, and the task and its conversation in VS Code's workspace storage on your machine. Read the full [PRIVACY.md](PRIVACY.md); the terms of use are in the [EULA.md](EULA.md).

## Requirements

- VS Code 1.101.2 or later (desktop).
- A folder you trust, opened in VS Code. Untrusted and virtual workspaces are not supported, because the model reads your files.
- An API key for one of the providers above, a local model through Ollama, or Claude Code signed in on this machine.

## Feedback

Found a bug, or have an idea? Open an issue at [github.com/OnurGumus/guide-coding/issues](https://github.com/OnurGumus/guide-coding/issues). For a bug, please say your VS Code version, provider and model, and what you did. The **Guide: Show log** output helps, but remove any code and keys from it first.
