# 🧰 DeepSeek Harness Tools

> ### ⚠️ Unofficial community project
>
> **Not affiliated with, endorsed by, or maintained by DeepSeek AI.** This is a
> hub for third-party add-ons to their open-source harness. For the official
> project see [deepseek-ai/deepseek-harness](https://github.com/deepseek-ai/deepseek-harness).
> Please do not report issues with these community tools to DeepSeek.

**A front door to community tools that extend the [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness) (`dsh`).**

`dsh` runs a strong local model as an agent. These add-ons give that agent
abilities the base harness does not ship: live web access, eyes for images, and
more over time. Each one is its own repo, focused and self-contained. This page
is just the map.

Everything here shares the same principles: **local-first, keyless where
possible, model-agnostic, and upgrade-safe** (nothing edits shipped `dsh` files,
so `npm i -g` never reverts your setup).

---

## The tools

| Tool | What it gives `dsh` | Status |
|---|---|---|
| **[Web Tools](https://github.com/tonyd2wild/DeepSeek-Harness-Web-Tools)** | Free, keyless `web_search` + `web_fetch`, so the agent can look things up and read pages | ✅ Live |
| **[Vision Tools](https://github.com/tonyd2wild/DeepSeek-Harness-Vision-Tools)** | Eyes for a text-only brain: a proxy that captions chat image attachments, plus an `analyze_image` tool for image files on disk | ✅ Live |
| _your tool here_ | Built something for `dsh`? See [Contributing](#contributing) | 🙌 |

---

## How they fit together

They stack. Nothing here is exclusive, and you can run all of them on the same
`dsh` at once:

- **Web Tools** registers `web_search` / `web_fetch` as model-facing tools.
- **Vision Tools** adds an `analyze_image` tool for files on disk, and a small
  proxy in front of your model for images dropped into the chat.

Because each add-on installs through the harness's normal extension points (a
per-profile plugin, a user agent-preset, or an OpenAI-compatible endpoint in
front of your model), they do not collide. Give one profile web plus vision and
leave another plain, on the same box, same model.

If you are wiring more than one, the pattern is the same every time:

1. Install the tool per profile (never into the `dsh` install's `node_modules`).
2. Compose it into a **user** agent-preset with a distinct id, and set that
   preset as your default in `settings.yaml`.
3. Verify by starting a real session, presets mount lazily, so a clean boot
   proves nothing.

Each tool's own README spells out its exact steps and the traps specific to it.

---

## What is `dsh`?

The [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness) is
DeepSeek's open-source agent harness: it drives a model (local or hosted)
through tool calls, profiles, and presets, on a web surface or headless. These
community tools plug into those same extension points.

---

## Contributing

Built a tool that extends `dsh`? Open a pull request that adds one row to the
table above: the name, a one-line description of what it gives the agent, a link,
and a status. Keep the same spirit as the existing tools:

- **Local-first and keyless where possible**, no cloud dependency the user did
  not choose.
- **Model-agnostic**, do not hardcode a specific model or endpoint.
- **Upgrade-safe**, install through profiles / presets / a proxy, never by
  editing shipped `dsh` files.
- **Honest about limits**, say what it does not do as clearly as what it does.
- **Unofficial**, carry the community-project banner and do not imply DeepSeek
  endorsement.

---

## Credits

- **[DeepSeek](https://github.com/deepseek-ai)** for the DeepSeek Harness and the
  models that make all of this worth building on.
- Every runtime and model these tools lean on is credited in its own repo.

If a tool here helped you, star the project it builds on first, they did the real work.

---

MIT, see [LICENSE](LICENSE).
