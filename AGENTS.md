# Repository Guidelines

## Project Structure & Module Organization

ZenCalendar is a static, browser-based calendar with responsive themes, printing, and PWA support.

- `index.html` loads configuration, bundled plugins, and initialization scripts in that order.
- `js/init.js` handles calendar generation, settings, theme loading, and PWA registration.
- `js/config.js` defines themes, festivals, holidays, makeup workdays, and `devMode`.
- `js/plugins.js` contains bundled third-party notification and lunar-calendar code.
- `css/base.css` styles shared controls; `themes/<id>/layout.css` styles individual calendars. Start new themes from `themes/__template/layout.css` and register them in `js/config.js`.
- `icon/`, `manifest*.json`, and `serviceworker.js` provide installation assets and offline caching.

## Build, Test, and Development Commands

There is no package manager configuration, build step, or dependency installation.

- `python3 -m http.server 8000 --bind 127.0.0.1`: serve the repository; open `http://localhost:8000`.
- `node --check js/init.js`: check JavaScript syntax without running the browser app. Repeat for other changed JavaScript files.
- `git diff --check`: catch whitespace errors before committing.

Deploy the repository's static files directly, preserving relative paths.

## Coding Style & Naming Conventions

Follow surrounding code: two-space JavaScript indentation, single-quoted strings, semicolons, and camelCase identifiers. No formatter or linter is configured. Preserve the existing script-based architecture and loading order. Keep CSS selectors and declarations consistent with neighboring rules; use existing custom properties for theme colors and sizes. Avoid reformatting bundled code in `js/plugins.js`.

Holiday keys use unpadded dates: `2027-1-1` for a specific year or `1-1` for annual recurrence. Keep year-specific holiday and workday entries grouped by year.

## Testing Guidelines

No automated test framework or coverage threshold is configured. Manually check year switching, leap-year February, month boundaries, lunar labels, holiday/workday markers, saved settings, both themes, mobile layouts, and print preview when relevant. For visual changes, capture screenshots and verify supported paper sizes.

## Commit & Pull Request Guidelines

History uses short prefixes such as `feat`, `fix`, `perf`, `doc`, and `update`, with optional colons and often Chinese descriptions. Use a specific subject, for example `update: 2027年节假日配置`.

PRs should describe the change, link relevant issues, list validation performed, and include screenshots for layout changes. Cite authoritative sources for holiday updates and distinguish predictions from confirmed arrangements.

## PWA Configuration

`devMode: true` unregisters service workers during development. Set it to `false` when testing installation and offline behavior. When changing cached assets, update `cacheVersion` in `serviceworker.js`; add new required offline assets to `cacheList`.
