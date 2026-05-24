# Azure DevOps Pull Requests — Documentation

User-facing documentation for the **Azure DevOps Pull Requests** JetBrains IDE plugin.

- **Live site**: <https://novakved.github.io/azure-docs/>
- **Plugin (Marketplace)**: <https://plugins.jetbrains.com/plugin/com.vednovak.azure>
- **Plugin source**: lives in a separate repository.

## What's in this repo

- [`Writerside/`](Writerside/) — Writerside source for the published documentation site.
- [`Writerside/README.md`](Writerside/README.md) — the authoring guide (folder layout, build instructions, contribution tips).
- [`.github/workflows/deploy-docs.yml`](.github/workflows/deploy-docs.yml) — builds the site with JetBrains' Writerside Docker action and publishes to GitHub Pages on every push to `main` that touches `Writerside/**`.

## Filing issues

- **Documentation bugs** (typos, missing pages, unclear instructions, broken links) — file them here.
- **Plugin bugs** (crashes, wrong behavior, feature requests for the plugin itself) — file them on the JetBrains Marketplace listing or wherever the plugin's main repository lives.

## Editing

See [`Writerside/README.md`](Writerside/README.md). The short version: install the [Writerside plugin](https://plugins.jetbrains.com/plugin/20158-writerside) in IntelliJ, open [`Writerside/writerside.cfg`](Writerside/writerside.cfg), edit any `.md` file under `topics/`, and the preview panel updates live.

Pushes to `main` rebuild and republish automatically.

## License

Documentation © Vedran Novak.
