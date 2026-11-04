# pi-bondhu

A companion for your pi terminal — an animated pixel-art avatar that reacts to what
the agent is doing (thinking, talking, reading, writing, tools), paired with a live
status strip: model, token counts, elapsed time, turn count, and a context-usage bar.

Forked from [cgxeiji/pi-emote](https://github.com/cgxeiji/pi-emote).

## Install

```bash
pi install npm:pi-bondhu
```

Or from source (bleeding edge):

```bash
pi install git:github.com/azmainadel/pi-bondhu
```

## Commands

| Command | Description |
| --- | --- |
| `/bondhu:set` | Pick an emote set (persists to your user config) |
| `/bondhu:sleep` | Put bondhu to sleep — one-line status only (persists) |
| `/bondhu:wake` | Wake bondhu — bring back the avatar and info panel (persists) |

While pi-bondhu is enabled, pi's built-in footer is hidden — the status strip takes
over that job in every mode.

## One-line mode

`/bondhu:sleep` collapses everything into a single line:

```text
🧠 openrouter • z-ai/glm-5.3-flash • high  |  ⚡️ ↑244k ↓17k ♻️ 6.2M  |  ⏰ 13m · 🔁 7     ● ▕░░░░░░░░░░░░░░░░▏ 4.3% / 1.0M
```

Model • thinking level, token stats (input/output/cache), elapsed time and turn
count, with the context-usage bar right-aligned. The status dot turns amber past 60%
and red past 85% context. The choice persists across restarts.

## Image rendering

pi-bondhu auto-detects the terminal and picks a renderer: kitty graphics, iTerm2
inline images, or ASCII pixel-art as fallback. Terminals that merely *claim* kitty
support get probed at startup — if the terminal doesn't actually answer the kitty
graphics query, bondhu falls back to ASCII automatically instead of showing a blank
space. You can force a renderer per terminal via the `terminals` config (see below).

## Emotes

![All emote states](emotes-contact-sheet.png)

Emote sets are directories of PNG frames per state (`idle`, `think`, `talk`, `read`,
`write`, `tool`, `hi`, `success`, `failure`, `compact`). See
[AGENTS.md](AGENTS.md) for the full configuration reference, custom emote-set
creation, and per-model emote mapping.

## Releasing (maintainers)

```bash
npm version patch && git push --tags   # CI stages the release
npm stage approve pi-bondhu            # approve with 2FA to go live
```

Publishes go through npm trusted publishing (OIDC) — no stored tokens; the GitHub
Action runs tests and stages the release on `v*` tags.

## License

MIT
