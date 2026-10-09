# the-wong-marketplace

A Claude Code plugin marketplace for sharing skills.

## Install a skill

Add the marketplace once, then install any plugin from it:

```
/plugin marketplace add thewongdirection/the-wong-marketplace
/plugin install securities-filings-lookup@the-wong-marketplace
```

Or from a shell:

```bash
claude plugin marketplace add thewongdirection/the-wong-marketplace
claude plugin install securities-filings-lookup@the-wong-marketplace
```

Installed skills are namespaced by plugin:
`/securities-filings-lookup:securities-filings-lookup`.

To try the marketplace from a local clone, use a path instead of the GitHub name:

```bash
claude plugin marketplace add ./the-wong-marketplace
```

## Layout

```
.claude-plugin/marketplace.json   the catalog: lists every plugin and where to find it
plugins/<plugin-name>/            one folder per plugin that lives in this repo
  .claude-plugin/plugin.json      plugin manifest (name, version, description, author)
  skills/<skill-name>/SKILL.md    one folder per skill
templates/skill-plugin/           copy this to start a new plugin
```

A plugin doesn't have to live in this repo: a catalog entry can point at another GitHub
repo instead (see `securities-filings-lookup`). A plugin can hold several skills. Group related skills in one plugin; split unrelated
ones into separate plugins so people can install only what they need.

## Add a skill

See [CONTRIBUTING.md](CONTRIBUTING.md).

## Validate

```bash
claude plugin validate .
claude plugin validate ./plugins/<plugin-name>
```

Validate the marketplace and each plugin directory separately; the marketplace run does
not open the skill files inside the plugins it lists.
