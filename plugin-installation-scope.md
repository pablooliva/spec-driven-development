# Claude Code Plugin Installation Scope

## Overview

[Claude Code plugins](https://docs.claude.com/en/docs/claude-code/plugins) can be installed and configured in two ways: system-wide (globally) or at the project level. Understanding these options helps you choose the right approach for your workflow.

## System-Wide Installation (Default)

When you install a plugin using the standard installation command, it's installed globally and available across all your projects.

### Installation Commands

```bash
# Install a specific plugin
/plugin install spec-driven-development@pablooliva

# Or use the interactive menu
/plugin
```

### Characteristics

- Available in all projects after installation
- Installed once, used everywhere
- Simple for individual developers
- Easy to enable/disable as needed

## Project-Level Configuration

You can configure plugins at the repository/project level by adding them to your project's `.claude/settings.json` file.

### Configuration File Location

```text
your-project/
└── .claude/
    └── settings.json
```

### Example Configuration

```json
{
  "extraKnownMarketplaces": {
    "pablooliva": {
      "source": {
        "source": "github",
        "repo": "pablooliva/spec-driven-development"
      }
    }
  },
  "enabledPlugins": {
    "spec-driven-development@pablooliva": true,
    ...
  }
}
```

### Benefits

- **Team Consistency**: When team members trust your repository folder, Claude Code automatically installs specified marketplaces and plugins for all team members
- **Standardized Tooling**: Ensures everyone on the team uses the same plugins and configurations
- **Zero Setup**: New team members get the right plugins automatically
- **Version Control**: Plugin configuration is tracked in git alongside your code

## Use Cases

### System-Wide Installation Best For

- Personal development preferences
- Tools you use across all projects
- Experimenting with new plugins
- Individual developer workflows

### Project-Level Configuration Best For

- Team projects requiring specific tooling
- Open source projects with contributor guidelines
- Enterprise environments with standardized setups
- Ensuring consistent development environments

## Managing Plugins

### Toggle Plugins On/Off

Plugins are designed to be toggled as needed:

- Enable them when you need specific capabilities
- Disable them when you don't to reduce system prompt context and complexity

### Verification

After installing a plugin:

```bash
# Check available commands
/help

# Manage plugins
/plugin
```

## Best Practices

1. **For Individual Use**: Install system-wide for flexibility across projects
2. **For Teams**: Configure in `.claude/settings.json` for consistency
3. **Don't Over-Install**: Too many plugins can make Claude lose focus
4. **Document Your Setup**: Add comments to your settings file explaining why certain plugins are required

## Summary

|Aspect|System-Wide|Project-Level|
|---|---|---|
|Installation|`/plugin install` command|`.claude/settings.json`|
|Scope|All projects|Specific project|
|Best For|Individual preferences|Team standardization|
|Auto-Install|No|Yes (when repo trusted)|
|Version Control|No|Yes|

---

_For more information, visit the [official Claude Code documentation](https://docs.claude.com/en/docs/claude-code/plugins)._
