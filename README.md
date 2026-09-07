# omarchy-omasushi 🍣

Omarchy bar widget for [omasushi](https://github.com/polidog/omasushi): shows how many
actions are pending between this machine and the packs it uses, and syncs from the bar.

![kind: bar-widget](https://img.shields.io/badge/omarchy-bar--widget-informational)

## Install

```sh
omarchy plugin add https://github.com/polidog/omarchy-omasushi.git --enable
```

Or, if you already use omasushi, take it as a pack of the omasushi repository:

```sh
omasushi use polidog/omasushi/plugin
omasushi sync
```

The widget needs the [`omasushi`](https://github.com/polidog/omasushi) CLI on `PATH`:

```sh
go install github.com/polidog/omasushi/cmd/omasushi@latest
```

## What it does

- Runs `omasushi diff --json` in the background and shows the pending action count
  (nothing pending: a plain sushi glyph, or hidden entirely — see settings).
- Clicking it opens the diff: every action with the pack behind it, plus unrecorded extras.
- **Sync** / **Export** / **Update** run in the Omarchy floating terminal, because
  `yay` and `git` may ask questions. The diff is refreshed once the terminal closes.
- Opens a pack's `omasushi.yaml` in your editor.

## Settings

| key | default | what |
|---|---|---|
| `refreshMinutes` | `10` | how often to re-run `omasushi diff` in the background |
| `hideWhenUpToDate` | `false` | hide the counter entirely when nothing is pending |

## Layout

```
manifest.json   # plugin manifest (id polidog.omasushi, kind bar-widget)
Panel.qml       # the widget: bar item + diff panel
Model.js        # diff parsing, action grouping, terminal command building
```

`omarchy plugin validate .` checks the manifest before publishing.

## Releasing

Bump `version` in `manifest.json` and tag:

```sh
git tag v0.2.0 && git push origin v0.2.0
```

## License

MIT
