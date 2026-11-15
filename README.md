# ejaje

Shared home for our AI tooling: Claude Code plugins and skills, plus instruction files for AI tools.

## Layout

```
.claude-plugin/marketplace.json     # makes this repo a Claude Code plugin marketplace
plugins/<plugin>/
  .claude-plugin/plugin.json        # plugin manifest
  skills/<name>/SKILL.md            # one folder per skill (+ optional scripts/, references/)
instructions/<tool>/                # instruction files per tool (e.g. claude-code/CLAUDE.md)
```

## Use the plugins

```bash
claude plugin marketplace add krzyszur/ejaje
claude plugin install <plugin>@ejaje
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).
