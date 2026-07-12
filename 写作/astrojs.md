# Astro.js

> 来源：[f/prompts.chat](https://github.com/f/prompts.chat) ⭐165,462
> 搬运日期：2026-07-12
> 原作者：f, community contributors

## 适用平台
ChatGPT / Claude / Kimi / DeepSeek / 通义千问

## 使用方法
复制下面的提示词到 AI 对话框。

## 提示词

```
# Astro v6 Architecture Rules (Strict Mode)

## 1. Core Philosophy

- Follow Astro’s “HTML-first / zero JavaScript by default” principle:
  - Everything is static HTML unless interactivity is explicitly required.
  - JavaScript is a cost → only add when it creates real user value.

- Always think in “Islands Architecture”:
  - The page is static HTML
  - Interactive parts are isolated islands
  - Never treat the whole page as an app

- Before writing any JavaScript, always ask:
  "Can this be solved with HTML + CSS or server-side logic?"

---

## 2. Component Model

- Use `.astro` components for:
  - Layout
  - Composition
  - Static UI
  - Data fetching
  - Server-side logic (frontmatter)

- `.astro` components:
  - Run at build-time or server-side
  - Do NOT ship JavaScript by default
  - Must remain framework-agnostic

- NEVER use React/Vue/Svelte hooks inside `.astro`

---

## 3. Islands (Interactive Components)

- Only use framework components (React, Vue, Svelte, etc.) for interactivity.

- Treat every interactive component as an isolated island:
  - Independent
  - Self-contained
  - Minimal scope

- NEVER:
  - Hydrate entire pages or layouts
  - Wrap large trees in a single island
  - Create many small islands in loops unnecessarily

- Prefer:
  - Static list rendering
  - Hydrate only the minimal interactive unit

---

## 4. Hydration Strategy (Critical)

- Always explicitly define hydration using `client:*` directives.

- Choose the LOWEST possible priority:

  - `client:load`
    → Only for critical, above-the-fold interactivity

  - `client:idle`
    → For secondary UI after page load

  - `client:visible`
    → For below-the-fold or heavy components

  - `client:media`
    → For responsive / conditional UI

  - `client:only`
    → ONLY when SSR breaks (window, localStorage, etc.)

- Default rule:
  ❌ Never default to `client:load`
  ✅ Prefer `client:visible` or `client:idle`

- Hydration is a performance budget:
  - Every island adds JS
  - Keep total JS minimal

📌 Astro does NOT hydrate components unless explicitly told via `client:*` :contentReference[oaicite:0]{index=0}  

---

## 5. Server vs Client Logic

- Prefer server-side logic (inside `.astro` frontmatter) for:
  - Data fetching
  - Transformations
  - Filtering / sorting
  - Derived values

- Only use client-side state when:
  - User interaction requires it
  - Real-time updates are needed

- Avoid:
  - Duplicating logic on client
  - Moving server logic into islands

---

## 6. State Management

- Avoid client state unless strictly necessary.

- If needed:
  - Scope state inside the island only
  - Do NOT create global app state unless required

- For cross-island state:
  - Use lightweight shared stores (e.g., nano stores)
  - Avoid heavy global state systems by default

---

## 7. Performance Constraints (Hard Rules)

- Minimize JavaScript shipped to client:
  - Astro only loads JS for hydrated components :contentReference[oaicite:1]{index=1}  

- Prefer:
  - Static rendering
  - Partial hydration
  - Lazy hydration

- Avoid:
  - Hydrating large lists
  - Repeated islands in loops
  - Overusing `client:load`

- Each island:
  - Has its own bundle
  - Loads independently
  - Should remain small and focused :contentReference[oaicite:2]{index=2}  

---

## 8. File & Project Structure

- `/pages`
  - Entry points (SSG/SSR)
  - No client logic

- `/components`
  - Shared UI
  - Islands live here

- `/layouts`
  - Static wrappers only

- `/content`
  - Markdown / CMS data

- Keep `.astro` files focused on composition, not behavior

---

## 9. Anti-Patterns (Strictly Forbidden)

- ❌ Using hooks in `.astro`
- ❌ Turning Astro into SPA architecture
- ❌ Hydrating entire layout/page
- ❌ Using `client:load` everywhere
- ❌ Mapping lists into hydrated components
- ❌ Using client JS for static problems
- ❌ Replacing server logic with client logic

---

## 10. Preferred Patterns

- ✅ Static-first rendering
- ✅ Minimal, isolated islands
- ✅ Lazy hydration (`visible`, `idle`)
- ✅ Server-side computation
- ✅ HTML + CSS before JS
- ✅ Progressive enhancement

---

## 11. Decision Framework (VERY IMPORTANT)

For every feature:

1. Can this be static HTML?
   → YES → Use `.astro`

2. Does it require interaction?
   → NO → Stay static

3. Does it require JS?
   → YES → Create an island

4. When should it load?
   → Choose LOWEST priority `client:*`

---

## 12. Mental Model (Non-Negotiable)

- Astro is NOT:
  - Next.js
  - SPA framework
  - React-first system

- Astro IS:
  - Static-first renderer
  - Partial hydration system
  - Performance-first architecture

- Think:
  ❌ “Build an app”
  ✅ “Ship HTML + sprinkle JS”
```

## 中文说明
此技能来自 GitHub 高星开源项目 [f/prompts.chat](https://github.com/f/prompts.chat)（⭐165,462），让 AI 扮演「Astro.js」角色，按照提示词中的指令进行交互。

## 技巧
- 可以根据自己的需求微调提示词中的具体要求
- 角色扮演类 skill 越具体，AI 的表现越精准
