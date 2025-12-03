# Repository Guidelines

## Project Structure & Module Organization
- `manifest.json` defines MV3 entry points and permissions (ChatGPT domains, `storage`, `scripting`).
- `content.js` injects UI hooks, fetches conversations, caches branches, and forwards tree updates.
- `panel.html` / `panel.js` render the side panel UI, settings, and navigation; resources are exposed via `web_accessible_resources`.
- `background.js` is the service worker that routes messages between tabs and toggles the panel.
- `README.md` covers user usage; tooling config lives in `eslint.config.js` and `.prettierrc.json`.

## Build, Test, and Development Commands
- `npm install` restores tooling (ESLint, Prettier, Husky, lint-staged).
- `npm run lint` checks all JS against the Chrome/WebExtensions-aware ESLint config.
- `npm run lint:fix` autofixes style issues.
- `npm run prettier` formats Markdown/HTML/JSON; JS formatting is enforced via ESLint + prettier plugin.
- Manual run: load the folder in `chrome://extensions` (Developer Mode → Load unpacked), open ChatGPT/chat.openai.com, and toggle the tree.

## Coding Style & Naming Conventions
- Prettier: 2-space indent, 80-char wrap, semicolons, single quotes, arrow parens always.
- Prefer `const`/`let`; `no-var` and unused-vars warnings are enforced. Keep browser-specific globals in sync with `eslint.config.js`.
- Use `camelCase` for functions/variables, `SCREAMING_SNAKE_CASE` for constants and message types (e.g., `TREE_UPDATED`), and kebab-case for DOM IDs/classes.
- Keep content and panel scripts self-contained; add globals only if registered in the ESLint config.

## Testing Guidelines
- No automated tests yet; always run `npm run lint` before pushing.
- Manual QA: load the extension, open a conversation, toggle the panel, verify nodes scroll to messages, branches appear after “Branch in new chat,” and clearing data resets state.
- When adding pure logic (parsing, caching), keep functions side-effect-light to ease future Jest coverage.

## Commit & Pull Request Guidelines
- Keep commits small and imperative (e.g., `Add branch cache expiry`, `Polish panel theme`); history is minimal, so be descriptive.
- Ensure Husky/lint-staged hooks stay green (`npm run lint` / `npm run prettier`) and commit any regenerated assets.
- PRs should summarize scope, list manual test steps/results, link issues, and include screenshots/GIFs for UI changes; call out manifest or permission changes explicitly.

## Security & Configuration Tips
- Do not log or persist access tokens; branch data should remain in `chrome.storage.local` only.
- Keep host permissions limited to ChatGPT domains; avoid remote scripts and stick to packaged resources for MV3 compliance.
- If adding new storage keys or messaging channels, namespace them clearly to avoid collisions with existing `branch` data.
