# Codeis — OpenCode-based prototype

Codeis is an MIT-licensed fork/prototype based on OpenCode. The original LICENSE and attribution are retained. This is not affiliated with OpenCode. Internal names, configuration, binaries and many UI references still use `opencode`; this is not a complete rebrand.

## What is added
The desktop/web new-session screen has Codeis project starter cards. Selecting a card shows relevant suggestions and can insert a starter prompt into the actual composer. Repository links are suggestions only; nothing is installed, connected or run automatically. This does not create Unity, Blender, model-training or hardware-design integrations. OpenCode's existing provider configuration, agent modes, command permissions and desktop/terminal functionality are inherited, not independently verified here.

## Getting started
This checkout requires Bun matching the version in the root package.json (and the upstream system dependencies). From the repo root, run `bun install`, then `bun run dev` for the terminal interface, or `bun run dev:desktop` for the desktop development application. See upstream README.md and packages/desktop/README.md for platform requirements and build instructions. Review dependencies and licenses before use.

Configure model providers and credentials using the upstream interface/documentation. Local models require a compatible provider/server and model installed separately. Check and test permission settings before using on sensitive files. Plan mode is not an OS sandbox; do not assume it protects against every side effect. Never paste API keys into prompts, source files or starter templates.

## Limitations / next steps
- Starter prompts replace the current composer text; review before use.
- Connector discovery, installation, dedicated specialist agents, training execution and chip pipelines are not implemented.
- Rename remaining upstream visual assets, CLI binaries, identifiers and release infrastructure carefully before distribution.
- Do not reuse upstream update/signing infrastructure for a fork; set up your own, audit security and test installers on each target OS.
- Hardware outputs need real tool verification and specialist review; no fabrication-readiness is implied.

## Codeis skill pack (10 curated starter skills)

Install into an existing project explicitly: `node codeis-kit/install-skills.mjs /path/to/your/project`. Existing skill files are not overwritten. Restart/reload the agent, open that project, and ask for a matching task. Skills are agent instructions, not guaranteed autonomous capabilities; installed tools, an active model and permissions are still needed. The installer makes no network calls. This is not a 1,000-skill library.

The pack covers UI/UX, web apps, games, Blender asset workflows, model training, RTL, hardware research, code review, testing and APIs. The web task cards insert prompts and link to external repositories, but do not configure MCP or run training.

## Verification in this environment
- Bun 1.4.4 dependency install completed, with dependency/patch warnings.
- `bun run dev --help` executed successfully; no live model or agent session was tested.
- `bun run --cwd packages/app typecheck` passed.
- All ten skill files parsed with the upstream SkillFile parser; installer installed them into a test directory and skipped existing files on a second run. End-to-end skill invocation with an LLM was not tested.
- Vite served its HTML (HTTP 200), but emitted a dependency-scan JSX parser warning. This is not proof that the web application functions end-to-end.
- No desktop installer, Termux, iOS, macOS, Windows, model-provider credentials, remote MCP, Unity/Blender, GPU training or actual chip workflow was tested. iOS is not an upstream desktop target; a web client requires a reachable backend.

## Local sandbox and static preview (experimental command-line tools)

These utilities are independent of the Codeis UI and do not automatically sandbox the main agent. They are not production security boundaries.

- `node codeis-kit/sandbox/codeis-lab.mjs preview /path/to/static-site` serves static files on local loopback only, with a random URL and sandboxed iframe. Stop with Ctrl+C. Use a dedicated public build folder: files inside that folder may be served to anyone who obtains the URL. Hidden files are blocked. It is not a Vite/Node backend preview and does not work as a remote or iOS proxy.
- `node codeis-kit/sandbox/codeis-lab.mjs run /path/to/project -- "node --version"` uses Docker to run an explicitly approved command in a temporary project copy. Network is off; resources are limited; changes are discarded. Hidden files, dependencies and symlinks are skipped. Docker and a locally available `node:22-alpine` image are required; Docker may download the image. Container isolation is not equivalent to a hardened VM; use a disposable host for hostile code. Docker daemon access itself is privileged. Never mount credentials or treat this as protection from kernel/container escapes.

Docker was unavailable in the development environment, so the container command was not executed against a real daemon. The preview is a local CLI tool, not a GUI integration. Neither feature is hooked into agent tool execution or remote web sessions.

## Repository catalog
`codeis-kit/REPOSITORIES.md` lists 50 candidates, also available as structured JSON. They are references only, not integrated or licence-audited.

Latest lab checks: Node syntax passed; static preview returned the test page, sandboxed iframe, blocked hidden files, escaping symlink and POST. Docker run correctly reported missing Docker (ENOENT); it has not been proven against a Docker daemon. Catalog contains 50 unique URLs, not verified individually for current availability.

## Latest integration work
The new-session UI now detects chip/model/CAD/research terms in the draft and shows relevant clickable repository references without installing them. A 3D Machine & R&D starter and an offline Python notebook download tool were added. User must manually upload the notebook to Colab or Kaggle; no training is performed. These suggestions do not activate skills or tools. The optional Forge sidecar now includes single-provider chat requests, but it is not connected to the app; see `codeis-forge/README.md`. Provider requests are mocked in tests; no live provider inference was tested.

Validation: app TypeScript check passed; two intent-router tests and 11 Forge tests passed. UI browser rendering and desktop builds were not tested.

## Branding and navigation update
New-session wordmark, window title and Windows application menu use Codeis; the home page includes Codeis branding, a New session action and an MCP connectors shortcut to the existing Extensions settings. UI fonts and existing SolidJS design are retained. This is a partial rebrand: other languages, upstream provider names, internal identifiers, configuration files, command names, attribution and other surfaces can still mention OpenCode. MCP connector navigation and the new-session button require browser verification; the local dev server was killed under memory pressure while loading Settings. This status was superseded by the automatic draft opening described below. No full end-to-end UI or MCP server connection test was completed.

## Home composer update
When an authenticated server is ready, Home opens a new real draft using the selected project, last project, or server-reported current directory. The server connection screen still appears first if authentication is needed. New task cards appear above the actual composer and insert reviewable prompts; they do not run or install tools. The default layout is side tabs for new settings; a user's saved layout is preserved. MCP connectors opens Extensions > MCPs, and Settings opens preferences.

Browser smoke check (local, 2026-11-22): authenticated server, automatic draft, website starter prompt insertion and MCP navigation were observed. Settings loaded. No actual model message was sent, no provider was connected, and no MCP server, CAD flow, hardware build or model training was tested. Screenshots represent this local state, not fully built features. The development server logged an initial Vite dependency-scan JSX error before loading dependencies on demand; startup reliability requires further work. UI TypeScript check and intent tests passed.

Branding remains incomplete beyond the main surfaces. Upstream configuration file names, provider names and notices are retained for compatibility and attribution; do not misrepresent external services as Codeis. Forge remains a separate sidecar and is not integrated with this composer.

## Compact welcome design
New-session cards are compact, theme-aware action chips above the actual composer; small screens use a horizontally scrollable row. Selected cards insert a reviewable prompt and display tool limitations. The user's chosen light or dark scheme is preserved. Local browser smoke checks verified display and website-prompt insertion on desktop, and took a mobile-viewport screenshot; no AI message was sent. The Vite dependency scan still reports an upstream JSX parsing error during cold startup before dependencies load on demand.

## Skills, discovery and simpler UI
The welcome page uses a simpler theme-native presentation with links to existing MCP, Skills, Plugins and Models settings. It provides a live, opt-in OpenRouter catalog query for IDs ending in `:free` with advertised zero prompt/completion prices; this is a discovery list, not automatic provider setup or a guarantee of zero other fees, availability, or unlimited usage. Connect OpenRouter using the existing provider UI and select a model in the composer. Ten GitHub tools are listed as external references; REA, Craft Anything, ReaCraft and the others are NOT installed, configured or tested as integrations.

19 Anthropic skill folders from https://github.com/anthropics/skills, commit e4bb5d960d87126ff3b3a8af1a104b7db67560ba, are bundled in `.agents/skills` for this project; licenses and third-party notices are preserved. They include third-party instructions/scripts and must be reviewed, and their dependencies installed separately. Copy them into a different project with `node codeis-kit/install-anthropic-skills.mjs <existing-project-directory>`; existing skill directories are skipped. This does not connect Claude or verify the skills are executed correctly by a model.

Testing: 4 Bun tests passed, TypeScript check passed. Local browser smoke test verified all 11 starter cards insert their intended prompts, Skills and Plugins navigate to the intended settings, and the live free catalog returned 11 entries at test time. Backend skill API exposed the Anthropic skills, including pptx and mcp-builder. Installer copied 19 skills and skipped them on rerun. A live Big Pickle inference attempt for the slides, semiconductor, graphics card, and CPU/GPU card prompts returned `Free usage limit reached` (HTTP 429); no model answers were produced. MCP connection, plugin execution, model training, slide creation, RTL tools, and other provider inference remain untested. Initial Vite cold dependency scan still logs an upstream JSX parse error and may be slow; warm browser smoke checks succeeded.

## Integration and build verification update

- REA 6.10.1 and Craft Anything 0.6.1 were downloaded to temporary test installations; Craft release SHA-256 matched GitHub metadata (signature not verified). MCP initialization and `tools/list` succeeded: 263 REA tools and 28 Craft restricted tools. With a separate temporary project configuration, the actual local Codeis backend reported both servers connected. That does not test tool calls or installed external analysis engines. The backend required forced termination during shutdown with both test servers active.
- Added `codeis-kit/install-integrations.sh` and `INTEGRATIONS.md`. The Linux x86-64 installer was run successfully against a separate test project. It installs REA and the Craft CLI outside the source tree and creates project MCP configuration without overwriting an existing config; REA defaults disabled pending trust review. These external binaries and dependencies are not bundled in the source archive and must be installed on the user's machine.
- Temporary Ollama 0.1.48 server pulled `qwen2:0.5b`; a real local `/api/chat` request about slides returned: “What are the main topics you would like to cover on your slides? How will your content help your audience?” This direct API test is not a Codeis agent integration test. Ollama binaries and model are not bundled. Do not assume that 0.5B model can handle tools or engineering tasks.
- A real single-slide PowerPoint was generated and reopened using python-pptx as an independent environment smoke test; it was not created by the Codeis agent or skills. Hardware tool execution and plugin execution remain unverified. No GPU or semiconductor validation was performed.
- Current UI typecheck passed (2,502 files); focused tests passed (4 tests, 10 expectations). Forge pytest passed (11, one deprecation warning). Previous browser checks confirmed all 11 cards insert prompts and checked navigation, not full task completion. A production Vite web build was attempted twice; both attempts failed to finish within 180 seconds in the memory-constrained environment and were stopped; no working production build or desktop package is claimed. GPT API inference was not tested without user credentials; earlier hosted free model inference was rate-limited (HTTP 429).
