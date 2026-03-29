# Installing Understand-Anything for VS Code + GitHub Copilot

## Prerequisites

- [VS Code](https://code.visualstudio.com/) with the [GitHub Copilot](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot) extension (v1.108+)
- Git

## Option A — Auto-discovery (recommended)

Clone this repo and open it in VS Code. GitHub Copilot automatically discovers the plugin via `.copilot-plugin/plugin.json` — no manual steps required.

```bash
git clone https://github.com/Lum1104/Understand-Anything.git
code Understand-Anything
```

Skills will appear in the **Configure Skills** menu inside GitHub Copilot Chat.

## Option B — Personal skills (available across all projects)

1. **Clone the repository:**
   ```bash
   git clone https://github.com/Lum1104/Understand-Anything.git ~/.copilot/understand-anything
   ```

2. **Create the skills symlink:**
   ```bash
   mkdir -p ~/.copilot/skills
   ln -s ~/.copilot/understand-anything/understand-anything-plugin/skills ~/.copilot/skills/understand-anything
   # Universal plugin root symlink — lets the dashboard skill find packages/dashboard/
   # Skip if already exists (e.g. another platform was installed first)
   [ -e ~/.understand-anything-plugin ] || [ -L ~/.understand-anything-plugin ] || ln -s ~/.copilot/understand-anything/understand-anything-plugin ~/.understand-anything-plugin
   ```

   **Windows (PowerShell):**
   ```powershell
   New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.copilot\skills"
   cmd /c mklink /J "$env:USERPROFILE\.copilot\skills\understand-anything" "$env:USERPROFILE\.copilot\understand-anything\understand-anything-plugin\skills"
   cmd /c mklink /J "$env:USERPROFILE\.understand-anything-plugin" "$env:USERPROFILE\.copilot\understand-anything\understand-anything-plugin"
   ```

3. **Restart VS Code** so GitHub Copilot can discover the skills.

## Verify

Open GitHub Copilot Chat → click **Configure Skills** — you should see the `understand-*` skills listed.

## Usage

Skills activate automatically when relevant. You can also invoke them directly in Copilot Chat:

- "Run the understand skill to analyze this codebase"
- "Use understand-dashboard to view the architecture map"
- "Use understand-chat to answer a question about the graph"

Or use the equivalent slash commands if you have Claude Code installed alongside:
- `/understand` — build the knowledge graph
- `/understand-dashboard` — open the interactive dashboard
- `/understand-chat <query>` — ask questions about the codebase
- `/understand-diff` — analyze impact of current changes
- `/understand-explain <path>` — deep-dive into a file or function
- `/understand-onboard` — generate an onboarding guide

## Updating

```bash
cd ~/.copilot/understand-anything && git pull
```

Skills update instantly through the symlink.

## Uninstalling

```bash
rm ~/.copilot/skills/understand-anything
rm ~/.understand-anything-plugin
rm -rf ~/.copilot/understand-anything
```
