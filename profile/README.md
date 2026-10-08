<!-- Header: profile/assets/readme-header*.svg, the Sidevoice brand's banner, as in every repository's README. -->
<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/readme-header-on-dark.svg">
    <img alt="Sidevoice — Give your coding agent a voice. Keep the conversation." src="assets/readme-header.svg" width="750">
  </picture>
</p>

<h3 align="center">Less reading. More thinking.</h3>

<p align="center">
  Sidevoice turns the conversation you already have with your coding agent into a voice call.
  The agent keeps its context and keeps writing as usual; it also speaks its replies, and you answer by voice
  and can interrupt it — from the sofa, not only at your desk.
</p>

<p align="center">
  <b>Beta</b> · Works with Claude Code and Codex; Cursor experimentally · Open source (Apache&#8209;2.0)
</p>

<p align="center">
  <a href="https://sidevoice.ai"><b>sidevoice.ai</b></a> ·
  <a href="#get-started">Get started</a> ·
  <a href="mailto:contact@sidevoice.ai">contact@sidevoice.ai</a>
</p>

## Get started

Your **machine** is the computer where your coding agents run; a **device** is what you call from (the desktop app,
a browser).

1. On your machine (macOS on Apple silicon, or Linux x64/arm64 with glibc 2.28+), with Node.js 18+:

   ```sh
   npx sidevoice install
   ```

   It installs and starts Sidevoice and registers its voice tools with the agents it finds.
   `npx sidevoice uninstall` reverses it.
2. Install the [desktop app](https://github.com/sidevoice/sidevoice-desktop#get-it) — nightly builds for now, for
   macOS on Apple silicon, Windows and Linux; on macOS the first open needs one extra step, explained there.
3. Ask your agent to pair a device and enter the one-time code in the app's settings, under machines. Then ask the
   agent to join the voice call, and talk.

## Repositories

**What you install**

- [**sidevoice-connector**](https://github.com/sidevoice/sidevoice-connector) — install this on your machine (npm:
  `sidevoice`): your agents' voice tools (an MCP server), and what installs and runs sidevoice-core.
- [**sidevoice-desktop**](https://github.com/sidevoice/sidevoice-desktop) — the app you call from, for macOS on
  Apple silicon, Windows and Linux.

**What runs underneath**

- [**sidevoice-core**](https://github.com/sidevoice/sidevoice-core) — runs next to your agents: holds their
  conversations, runs one voice pipeline per call, and decides which devices may connect.
- [**sidevoice-web**](https://github.com/sidevoice/sidevoice-web) — the call interface. The desktop app bundles it;
  it can also be served as a static site.

**In development**

- [**sidevoice-engine**](https://github.com/sidevoice/sidevoice-engine) — local speech models on the device: catalogue,
  choice and lifecycle, as Rust crates and a WebAssembly package. A skeleton: no model runs through it yet.

## Where your voice goes

- Your device talks to your machine directly. Out of the box a pairing code works only on the machine itself;
  another device needs the machine reachable over HTTPS. Reaching it from outside your
  network needs a relay, which is still being built.
- Transcription and speech can run locally — in the browser, or in the desktop app on Macs with Apple silicon — so
  your audio stays on your own devices. Or use OpenAI or ElevenLabs with your own key, kept on your machine; the
  Windows and Linux builds of the desktop app use these for now.

## Contributing

Issues and pull requests are welcome in every repository. Each README says how to build and test it; its
`AGENTS.md` holds the rules for code and docs, for people and coding agents alike. Please report security issues
privately by email to [contact@sidevoice.ai](mailto:contact@sidevoice.ai), not in a public issue.

## Licence

The code is under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0). Bundled third-party
components keep their own licences, listed in `THIRD_PARTY_NOTICES.md` where a repository has them.
The Sidevoice name and logo are trademarks: forks are welcome under their own name (each repository's
`TRADEMARKS.md`).
