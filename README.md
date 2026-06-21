# opencode-skill-web-designer

A self-improving web design agent for [opencode](https://opencode.ai). Reads past design patterns, applies frontend best practices, and captures learnings every session so designs get better over time.

## What It Does

When you type `/design <description>`, this skill activates a **web-designer agent** that:

1. **Reads your knowledge base** — loads design patterns, build gotchas, and reusable components from every project you've done
2. **Loads design skills** — applies `frontend-design` (aesthetic guidance) and `web-design-guidelines` (accessibility/UX)
3. **Generates production-ready code** — never uses templated defaults
4. **Captures learnings** — after every session, writes what worked to the knowledge base so the next project is better

## Installation

### 1. Clone the skill

```bash
git clone https://github.com/jeremygideonbareh/opencode-skill-web-designer.git ~/.opencode-skills/web-designer
```

### 2. Add to your opencode config

Edit `~/.config/opencode/opencode.jsonc`:

```jsonc
{
  "skills": {
    "paths": [
      "~/.opencode-skills/web-designer"
    ]
  }
}
```

### 3. Add the agent and command

Add this agent to the `"agent"` section of your `~/.config/opencode/opencode.jsonc`:

```jsonc
"web-designer": {
  "description": "Web design specialist — loads frontend-design and web-design-guidelines skills, reads knowledge base for past design patterns",
  "mode": "subagent",
  "prompt": "You are a senior web designer specializing in distinctive, intentional visual design. Before starting: read ~/.config/opencode/knowledge/ for past design patterns. Load the frontend-design skill for aesthetic guidance. Load the web-design-guidelines skill for accessibility/UX compliance. Apply the most successful patterns from past projects. Never use templated/default designs — every element should be intentional. Output complete, production-ready code.",
  "tools": {
    "read": true,
    "write": true,
    "edit": true,
    "glob": true,
    "grep": true,
    "bash": true
  }
}
```

Add this command to the `"command"` section:

```jsonc
"design": {
  "description": "Design or redesign UI using past learnings and design skills",
  "template": "Design/redesign the following: $ARGUMENTS\n\nRead the knowledge base at ~/.config/opencode/knowledge/. Load frontend-design and web-design-guidelines skills. Apply the best design patterns from past projects. Never use templated defaults.",
  "agent": "web-designer",
  "subtask": true
}
```

### 4. Create the knowledge base directory

```bash
mkdir -p ~/.config/opencode/knowledge
```

Copy the starter entry from this repo:

```bash
cp ~/.opencode-skills/web-designer/knowledge/starter.md ~/.config/opencode/knowledge/
```

### 5. Add to global AGENTS.md (optional but recommended)

Append to `~/.config/opencode/AGENTS.md`:

```markdown
## Cross-Project Pipeline

### Before Every Project
- Read ALL files from `~/.config/opencode/knowledge/`
- Load relevant skills (frontend-design, web-design-guidelines)

### After Every Session
- Write learnings to `~/.config/opencode/knowledge/<project>.md`
```

## Usage

```bash
/design a hero section with gradient mesh background
/design review this component
/design redesign the navigation to be more accessible
```

The agent reads your knowledge base, loads design skills, and outputs complete code that improves over time as you use it.

## How Learning Works

```
Session 1 → you build a site → captured to knowledge/
Session 2 → AI reads knowledge/ → applies best patterns
Session 3 → knowledge base has 2+ projects → patterns compound
...
After 10 projects → AI has a rich corpus of your style
```

Each `~/.config/opencode/knowledge/<project>.md` file stores:
- Design patterns that worked (and verdict to keep/drop)
- Build pipeline gotchas
- Reusable component paths
- Agent performance notes
- Mistakes to avoid

## License

MIT
