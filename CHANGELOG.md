# Changelog

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
