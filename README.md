<p align="center"><code>npm i -g @infinity/codex</code><br />or <code>brew install --cask infinity-codex</code></p>
<p align="center"><strong>infinityCodex CLI</strong> is a coding agent from OpenAI that runs locally on your computer.
<p align="center">
  <img src="https://github.com/openai/codex/blob/main/.github/codex-cli-splash.png" alt="infinityCodex CLI splash" width="80%" />
</p>
</br>
If you want infinityCodex in your code editor (VS Code, Cursor, Windsurf), <a href="https://developers.openai.com/codex/ide">install in your IDE.</a>
</br>If you are looking for the <em>cloud-based agent</em> from OpenAI, <strong>infinityCodex Web</strong>, go to <a href="https://chatgpt.com/codex">chatgpt.com/codex</a>.</p>

---

## Quickstart

### Installing and running infinityCodex CLI

Install globally with your preferred package manager:

```shell
# Install using npm
npm install -g @infinity/codex
```

```shell
# Install using Homebrew
brew install --cask infinity-codex
```

Then simply run `infinity-codex` to get started.

<details>
<summary>You can also go to the <a href="https://github.com/openai/codex/releases/latest">latest GitHub Release</a> and download the appropriate binary for your platform.</summary>

Each GitHub Release contains many executables, but in practice, you likely want one of these:

- macOS
  - Apple Silicon/arm64: `infinity-codex-aarch64-apple-darwin.tar.gz`
  - x86_64 (older Mac hardware): `infinity-codex-x86_64-apple-darwin.tar.gz`
- Linux
  - x86_64: `infinity-codex-x86_64-unknown-linux-musl.tar.gz`
  - arm64: `infinity-codex-aarch64-unknown-linux-musl.tar.gz`

Each archive contains a single entry with the platform baked into the name (e.g., `infinity-codex-x86_64-unknown-linux-musl`), so you likely want to rename it to `infinity-codex` after extracting it.

</details>

### Using infinityCodex with your ChatGPT plan

Run `infinity-codex` and select **Sign in with ChatGPT**. We recommend signing into your ChatGPT account to use infinityCodex as part of your Plus, Pro, Team, Edu, or Enterprise plan. [Learn more about what's included in your ChatGPT plan](https://help.openai.com/en/articles/11369540-codex-in-chatgpt).

You can also use infinityCodex with an API key, but this requires [additional setup](https://developers.openai.com/codex/auth#sign-in-with-an-api-key).

## Docs

- [**infinityCodex Documentation**](https://developers.openai.com/codex)
- [**Contributing**](./docs/contributing.md)
- [**Installing & building**](./docs/install.md)
- [**Open source fund**](./docs/open-source-fund.md)

This repository is licensed under the [Apache-2.0 License](LICENSE).
