<!-- Header: profile/assets/readme-header*.svg, from the Sidevoice brand's banner. -->
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/sidevoice/.github/main/profile/assets/readme-header-on-dark.svg" />
  <img alt="Sidevoice — Give your coding agent a voice. Keep the conversation." src="https://raw.githubusercontent.com/sidevoice/.github/main/profile/assets/readme-header.svg" width="750" />
</picture>

Reading your coding agent's plans, diffs and summaries all day is tiring. **Sidevoice** turns the conversation you
already have with your agent into a voice call. The agent keeps its context and keeps writing as usual; it also
speaks its replies, and you answer by voice and can interrupt it — from the sofa or on a walk, not only at your desk.
Your agent stays where it runs.

Open source; the licence is being decided ([#11](https://github.com/sidevoice/.github/issues/11)). Beta.

## The pieces

| Repository | What it is |
|---|---|
| [**sidevoice-connector**](https://github.com/sidevoice/sidevoice-connector) | What you install on the machine where your agents run (`npx -y @sidevoice/uplink install`). It gives each conversation its voice tools and delivers what you say into it. |
| [**sidevoice-core**](https://github.com/sidevoice/sidevoice-core) | Runs next to your agents: the conversations, one voice pipeline per call, and which devices may use the machine. The connector installs and supervises it. |
| [**sidevoice-desktop**](https://github.com/sidevoice/sidevoice-desktop) | The app you call from, for macOS, Windows and Linux; on Apple-Silicon Macs, speech models run natively. |
| [**sidevoice-web**](https://github.com/sidevoice/sidevoice-web) | The call interface. The desktop app bundles it; it can also be served as a static site. |

Your device talks to your machine directly once it is paired. Reaching it from outside your network needs a
relay, which is still being built.

## Get started

1. On the machine where your agents run: `npx -y @sidevoice/uplink install` (needs Node.js 22+ and
   [uv](https://docs.astral.sh/uv/)), then finish any step it prints for your agent
   ([supported agents](https://github.com/sidevoice/sidevoice-connector#supported-agents)).
2. Install the [desktop app](https://github.com/sidevoice/sidevoice-desktop/releases) and pair it with the one-time
   code your agent gives you when you ask it to pair a device.
3. Ask your agent to join the voice call, and talk.

## Supported agents

Claude Code and Codex today; Cursor experimentally. Details per agent in the
[connector's README](https://github.com/sidevoice/sidevoice-connector#supported-agents).

## Contributing

Issues and pull requests are welcome in each repository; each one's README says how to build and test it, and its
`AGENTS.md` holds the rules for code and texts.
