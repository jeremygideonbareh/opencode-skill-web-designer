# Starter Knowledge Entry

Copy this file to `~/.config/opencode/knowledge/<your-project>.md` and fill it out after each project.

```markdown
# <Project Name> — <Date>

## Design Patterns Used
- pattern description — verdict: Keep/Drop/Needs Improvement

## Build Pipeline
- commands: npm run dev / npm run build / deploy method
- gotchas: any issues encountered

## Reusable Components
- path/to/component.jsx: what it does

## Agent Performance
- which agents helped most, what prompts worked best

## Mistakes to Avoid
- what went wrong and how to prevent it next time
```

## Example

```markdown
# Website Development Homepage — June 21, 2026

## Design Patterns Used
- **Looping video hero** over scroll animation — video feels premium, no scroll-timing issues. Keep
- **Day/night palette via JS object** — simple inline styles, no CSS variables needed. Keep
- **Favicon fallback for blocked iframes** — Google favicons API, free no auth. Keep

## Build Pipeline
- npm run dev / npm run build
- Deploy: temp dir git push to gh-pages (npm gh-pages broken on long Windows paths)
- Gotcha: Vite base must be "/repo-name/" for GitHub Pages subpath

## Reusable Components
- BrowserFrame.jsx: macOS browser chrome with iframe/favicon previews
- AnimatedBeamTimeline.jsx: SVG animated execution timeline
- WhyUsSection.jsx: horizontal scroll snap section with custom scrollbar

## Agent Performance
- 21st.dev magic component builder: excellent for generating components
- explore agent: best for tracing bugs across multiple files

## Mistakes to Avoid
- Don't use framer-motion useScroll with position:fixed targets — use window.scrollY
- Always git add new component files before building — untracked files cause CI failures
```
