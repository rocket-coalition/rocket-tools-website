



awesome—here’s a pragmatic, end-to-end **developer checklist** that starts from zero and gets the Rocket Tools site live. it’s organized in the most natural build order and includes the key commands, files, and milestones.

# phase 0 — prerequisites

* [ ] install: **Hugo (extended)**, **Node 18+**, **Git**, **Netlify CLI** (`npm i -g netlify-cli`)
* [ ] verify:

  * [ ] `hugo version` (should say *extended*)
  * [ ] `node -v`, `npm -v`
  * [ ] `netlify -v`

# phase 1 — project bootstrap

* [ ] create repo & empty hugo site

  ```bash
  hugo new site rocket-tools
  cd rocket-tools
  git init
  echo "public/" >> .gitignore
  ```
* [ ] add base config

  * [ ] create `config.yaml` with minimal site info and disable built-in taxonomies:

    ```yaml
    baseURL: "/"
    languageCode: "en-us"
    title: "Rocket Tools"
    disableKinds: ["taxonomy", "taxonomyTerm"]
    taxonomies: {}
    build:
      writeStats: true
    params:
      env: "development"
    ```
* [ ] commit

  ```bash
  git add .
  git commit -m "chore: init hugo site"
  ```

# phase 2 — asset pipeline: tailwind + daisyui

* [ ] initialize npm & install deps

  ```bash
  npm init -y
  npm i -D tailwindcss postcss autoprefixer daisyui
  npx tailwindcss init -p
  ```
* [ ] configure **tailwind**

  * [ ] in `tailwind.config.js`:

    ```js
    module.exports = {
      content: ["./layouts/**/*.{html,js}", "./content/**/*.{md,html}"],
      theme: { extend: {} },
      plugins: [require("daisyui")],
      daisyui: { themes: ["light","dark"] }
    }
    ```
  * [ ] create `assets/css/tailwind.css`:

    ```css
    @tailwind base;
    @tailwind components;
    @tailwind utilities;
    ```
* [ ] wire CSS into base layout

  * [ ] create `layouts/_default/baseof.html` with Hugo Pipes build:

    ```html
    {{ $css := resources.Get "css/tailwind.css" | postCSS }}
    <link rel="stylesheet" href="{{ $css.RelPermalink }}">
    ```
* [ ] add **HTMX** and **Alpine.js** to base layout (head or end of body):

  ```html
  <script src="https://unpkg.com/htmx.org@1.9.12"></script>
  <script src="https://unpkg.com/alpinejs@3.x.x" defer></script>
  ```

# phase 3 — site structure & layouts

* [ ] directories

  ```
  /archetypes/
  /content/tools/
  /data/
  /layouts/_default/
  /layouts/partials/
  /static/
  /netlify/functions/
  ```
* [ ] base shell (DaisyUI layout)

  * [ ] in `layouts/_default/baseof.html`, add a two-pane layout: fixed left sidebar, right main content (container).

# phase 4 — custom data: tool groups & tags (no built-ins)

* [ ] create `/data/tool_groups.yaml` with initial 5 groups and placeholder tools (ids).
* [ ] create `/data/tool_tags.yaml` (the taxonomy you defined earlier).
* [ ] commit:

  ```bash
  git add data
  git commit -m "feat: tool groups and tags data"
  ```

# phase 5 — partials & templates

* [ ] **sidebar** partial rendering groups & tools

  * [ ] `layouts/partials/sidebar.html`:

    * read `.Site.Data.tool_groups`
    * Alpine.js for expand/collapse
    * highlight active tool based on `.RelPermalink`
* [ ] **tool page** template

  * [ ] `layouts/tool/single.html` (or `_default/single.html` with conditional):

    * sections: metadata, input box + run button, status area, results area, article content beneath
    * include partials:

      * `partials/tool/meta.html`
      * `partials/tool/input.html`
      * `partials/tool/output.html`
      * `partials/tool/tags.html`
* [ ] **head** partial for SEO/meta (optional):

  * [ ] use `title`, `description`, `tool_tags`.

# phase 6 — official archetype (front matter schema)

* [ ] create `/archetypes/tool.md` using the **official schema** you approved (title, tool_group, tool_tags, educational_objectives, system_prompt, user_prompt_template, etc.).
* [ ] test archetype generation

  ```bash
  hugo new --kind tool tools/example-tool/index.md
  ```
* [ ] open generated file and ensure all keys exist.

# phase 7 — initial content (5 groups × 4 tools)

* [ ] for each initial tool id from `tool_groups.yaml`, generate content:

  ```bash
  hugo new --kind tool tools/<tool-id>/index.md
  ```
* [ ] set realistic placeholder values for `system_prompt`, `user_prompt_template`, `backend_function`, etc.
* [ ] add `article_content` markdown text (beneath results in template).

# phase 8 — HTMX wiring (client → function → response)

* [ ] in `partials/tool/input.html`:

  * [ ] create `<form hx-post="/.netlify/functions/{{ .Params.backend_function }}" hx-trigger="submit" hx-target="#results" hx-swap="innerHTML">`
  * [ ] include a hidden field with the tool’s prompts/metadata as needed.
  * [ ] visible input textbox/textarea and **Run Tool** button.
  * [ ] bind Alpine state for loading/error:

    * `x-data="{loading:false, error:''}"`
    * htmx events: `hx-on:htmx:beforeRequest="loading=true"`; `htmx:afterRequest="loading=false"`; `htmx:error="error='Something went wrong'"`
* [ ] in `partials/tool/output.html`:

  * [ ] `<div id="results" x-transition></div>`
  * [ ] a small status area: spinner when `loading`, error banner when `error`.

# phase 9 — serverless backend (Netlify Functions)

* [ ] initialize Netlify config

  * [ ] `netlify.toml`:

    ```toml
    [build]
      command = "npm run build && hugo"
      publish = "public"
      functions = "netlify/functions"

    [[redirects]]
      from = "/api/*"
      to = "/.netlify/functions/:splat"
      status = 200
    ```
* [ ] add env vars (in Netlify UI or `.env` for local dev with `netlify dev`)

  * [ ] `LLM_API_KEY`, `LLM_BASE_URL`, optional `MODEL`, `TIMEOUT_MS`
* [ ] scaffold a lightweight executor function per `backend_function`:

  * [ ] `netlify/functions/summarizer.ts` (or `.js`):

    * parse `event.body` (user input + metadata)
    * assemble prompt from `system_prompt` + `user_prompt_template`
    * call LLM (via your lightweight library)
    * return HTML/Markdown fragment for HTMX target
* [ ] add common utils

  * [ ] `netlify/functions/_shared/llmClient.ts` for HTTP calls/timeouts
  * [ ] central error handling → send meaningful messages to UI
* [ ] local test

  ```bash
  netlify dev
  ```

  * [ ] verify HTMX form posts → function → response rendered.

# phase 10 — build pipeline for CSS & Hugo

* [ ] add scripts in `package.json`:

  ```json
  {
    "scripts": {
      "dev": "hugo server -D",
      "css:build": "tailwindcss -i ./assets/css/tailwind.css -o ./assets/css/_generated.css --minify",
      "build": "npm run css:build"
    }
  }
  ```
* [ ] ensure `baseof.html` points to the built CSS (Hugo Pipes or generated file—keep one approach consistent).
* [ ] run:

  ```bash
  npm run build
  hugo server -D
  ```

# phase 11 — UX polish (DaisyUI + Alpine)

* [ ] apply DaisyUI components: sidebar, buttons, alerts, tabs/cards.
* [ ] loading states always visible (no “dead air”):

  * [ ] spinner on submit
  * [ ] progress/typing indicator if you simulate streaming
* [ ] accessibility pass:

  * [ ] focus states, ARIA live region for result area, color contrast.

# phase 12 — quality gates

* [ ] validate front matter for all tools (keys present, types correct).
* [ ] test flows:

  * [ ] select group → select tool → view metadata
  * [ ] input → run → output → rerun
  * [ ] error path (simulate function failure)
* [ ] mobile & tablet responsiveness on sidebar and main panel.
* [ ] 404s, home, top nav/logo.

# phase 13 — analytics & telemetry (optional)

* [ ] add privacy-friendly client analytics (e.g., Plausible, Netlify Analytics).
* [ ] log function timings & errors (without storing user content) for perf insights.

# phase 14 — deploy

* [ ] push to GitHub/GitLab.
* [ ] connect repo to Netlify; configure environment variables.
* [ ] set build command: `npm run build && hugo`
* [ ] set publish dir: `public`
* [ ] trigger first deploy and verify:

  * [ ] sidebar groups render from `/data/tool_groups.yaml`
  * [ ] tool tags render from `/data/tool_tags.yaml`
  * [ ] HTMX calls hit `/.netlify/functions/...`

# phase 15 — content ops (AI agent workflow)

* [ ] script (or function) to **generate/update** tool pages:

  * [ ] produce front matter per archetype
  * [ ] write to `content/tools/<tool-id>/index.md`
  * [ ] update `/data/tool_groups.yaml` to include the tool id in correct group
* [ ] optional pre-commit check: validate new tools against a JSON Schema of front matter.

# phase 16 — handoff docs

* [ ] add `/docs/SETUP.md` (summarize the above for onboarding).
* [ ] add `/docs/CONTENT.md` (how to add tools, groups, tags).
* [ ] add `/docs/BACKEND.md` (function contract: request/response shape, env vars).

---

## acceptance checklist (ship-ready)

* [ ] five groups visible with four tools each
* [ ] each tool renders: name, description, examples, educational points (10), input, run button, output area, article content
* [ ] HTMX request succeeds and error states are user-friendly
* [ ] no Hugo taxonomy pages generated
* [ ] mobile layout clean and accessible
* [ ] first deploy on Netlify green

want me to generate the initial `tool_groups.yaml` with 5 groups × 4 tool ids and the matching **scaffold commands** you can paste in your terminal?
