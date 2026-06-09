---
name: html-visualizer
description: 'Create user-facing outputs as rendered HTML instead of Markdown. Use when the user asks to visualize results, present dashboards/cards/tables, or preview rich content in a browser-ready format.'
argument-hint: 'What to visualize, target audience, and preferred layout style'
user-invocable: true
disable-model-invocation: false
---

# HTML Visualizer

## What This Skill Produces
- A standalone HTML document that presents requested content visually.
- Semantic structure with accessible labels and readable typography.
- Embedded CSS and optional lightweight JavaScript for interactivity.
- A short summary of what was visualized and where the output file is located.

## When to Use
- The user wants visual output instead of Markdown.
- The response should be presented as cards, tables, timelines, dashboards, or reports.
- The user asks to show results in a browser preview.

## Input Checklist
Collect or infer before rendering:
- Content to display (text, lists, metrics, code snippets, links, images).
- Visual format (report, comparison table, KPI board, gallery, etc.).
- Constraints (mobile support, accessibility, branding, dark/light preference).
- Output target (inline snippet only, or HTML file in workspace).

## Workflow
1. Confirm the visualization goal
- Restate what should be shown and who it is for.
- If ambiguous, ask one focused clarification question.

2. Choose a layout pattern
- Use table layout for structured comparisons.
- Use card grid for grouped items.
- Use sections plus anchors for long-form reports.
- Use chart-like blocks only when true chart libraries are not requested.

3. Build semantic HTML
- Use `header`, `main`, `section`, `article`, `nav`, and `footer` appropriately.
- Keep heading hierarchy valid (`h1` then `h2/h3`).
- Use real `table` markup for tabular data.

4. Add presentation styling
- Define CSS custom properties at `:root` for colors and spacing.
- Ensure responsive behavior with simple breakpoints.
- Maintain strong contrast and readable line lengths.

5. Add optional interaction
- Keep JavaScript minimal and dependency-free by default.
- Avoid inline event handlers when possible.
- Preserve functionality without JavaScript when feasible.

6. Validate output quality
- Ensure no Markdown wrappers around final HTML.
- Escape unsafe user-provided text before inserting into HTML.
- Verify links and image paths are valid in workspace context.

7. Deliver
- If user asks for a file, create an `.html` file in workspace and provide the path.
- Provide a concise explanation of major sections and how to preview it.

## Output Rules
- Prefer returning pure HTML blocks when the user asks to "show" content visually.
- Do not convert final answer back to Markdown tables unless explicitly requested.
- If both explanation and HTML are needed, keep explanation short and place full HTML in a fenced `html` block or file.

## Accessibility and Safety Rules
- Include `lang` on the root `html` element.
- Include viewport meta tag for mobile rendering.
- Use meaningful alt text for non-decorative images.
- Do not inject unescaped raw user input into HTML.
- Avoid remote third-party scripts unless explicitly requested.

## Quick Template

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Visualization</title>
  <style>
    :root {
      --bg: #f5f7fb;
      --surface: #ffffff;
      --text: #17212f;
      --muted: #5a6a80;
      --accent: #0b6ef3;
      --border: #dbe3f0;
    }
    body {
      margin: 0;
      font-family: "IBM Plex Sans", "Segoe UI", sans-serif;
      background: radial-gradient(circle at 10% 0%, #eef3ff 0%, var(--bg) 40%);
      color: var(--text);
    }
    .wrap {
      max-width: 1100px;
      margin: 0 auto;
      padding: 24px;
    }
    .grid {
      display: grid;
      gap: 16px;
      grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    }
    .card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 14px;
      padding: 16px;
      box-shadow: 0 8px 24px rgba(16, 24, 40, 0.06);
    }
    .muted {
      color: var(--muted);
    }
  </style>
</head>
<body>
  <main class="wrap">
    <h1>Visualization Title</h1>
    <p class="muted">Short summary of what is shown.</p>
    <section class="grid" aria-label="Visualized content">
      <article class="card">Card content</article>
      <article class="card">Card content</article>
      <article class="card">Card content</article>
    </section>
  </main>
</body>
</html>
```

## Quality Gate Checklist
- HTML is valid and standalone.
- Layout is responsive on desktop and mobile.
- Content hierarchy is clear and accessible.
- User request is represented visually (not only text dump).
- If file output is requested, path is provided and preview instructions are included.

## Example Prompts
- /html-visualizer Visualize this sprint summary as a clean dashboard with KPI cards and a risk table.
- /html-visualizer Turn these API test results into an HTML report I can share with stakeholders.
- /html-visualizer Show this product comparison in a responsive, accessible HTML layout instead of Markdown.
