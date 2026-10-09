# Adding a skill

1. **Copy the template.** Copy `templates/skill-plugin/` to `plugins/<your-plugin-name>/`.
2. **Name things.** Use kebab-case. The plugin name must not start with `claude-`,
   `anthropic-`, `anthropics-` or `cc-plugin-` (reserved; validation fails).
3. **Edit `.claude-plugin/plugin.json`.** Set `name`, `description`, `author`, and `version`.
4. **Rename `skills/your-skill-name/` and edit its `SKILL.md`.**
   - `name`: the skill's command name (defaults to the folder name).
   - `description`: what the skill does *and when Claude should use it*. This line is how
     Claude decides to load the skill, so be specific.
   - Keep `SKILL.md` under about 500 lines. Put long reference material in sibling files
     and link to them.
5. **Register it** by adding an entry to `.claude-plugin/marketplace.json`. The entry
   `name` must match the `name` in the plugin's `plugin.json`:

   ```json
   {
     "name": "your-plugin-name",
     "source": "./plugins/your-plugin-name",
     "description": "One sentence on what it does.",
     "category": "productivity",
     "tags": ["tag-one", "tag-two"]
   }
   ```

6. **Validate.**

   ```bash
   claude plugin validate .
   claude plugin validate ./plugins/your-plugin-name
   ```

7. **Try it.** Load just your plugin in a session without installing it:

   ```bash
   claude --plugin-dir ./plugins/your-plugin-name
   ```

8. **Open a pull request.**

## Versions and updates

If `version` is set in a plugin's `plugin.json`, users only receive an update when you
change that string, so bump it with every release. If you leave `version` out, every
commit counts as a new version.

Set the version in `plugin.json` only, not in the marketplace entry, so the two cannot
drift apart.
