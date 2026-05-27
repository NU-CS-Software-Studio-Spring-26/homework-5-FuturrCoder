# AGENTS.md

## Stack

- Rails `~> 8.1.3`, Ruby `3.4.1` (`.ruby-version`), SQLite (`config/database.yml`, `storage/*.sqlite3`).
- View layer: ERB, `turbo-rails`, `stimulus-rails`, `importmap-rails`, Propshaft (`app/assets/stylesheets/application.css`).
- JSON views: Jbuilder (`app/views/**/*.json.jbuilder`).
- Tests: Minitest under `test/` (unit, integration, system); Capybara + Selenium in the `:test` Gemfile group.
- Background jobs: Solid Queue (`solid_queue`, `bin/jobs`); also `solid_cache` and `solid_cable` in the Gemfile.

## Commands

- Setup: `bin/setup` (`bundle install`, `bin/rails db:prepare`; starts `bin/dev` unless `--skip-server`).
- Run: `bin/dev` (runs `bin/rails server`).
- Test: `bin/rails db:test:prepare test test:system` (same as `.github/workflows/ci.yml`).
- Lint: `bin/rubocop`.

## Conventions

- Naming: `Todo` / `TodosController`; routes use `resources :todos` (no `root` route defined).
- Authorization: none in `app/` (no auth gems in the Gemfile).
- Controllers: full-page CRUD uses `format.html` and `format.json` (`TodosController`); add `format.turbo_stream` only for partial in-place updates.
- Hotwire: prefer Turbo Streams (`*.turbo_stream.erb`, stable DOM ids) over custom JS/Stimulus for partial page updates; `turbo-rails` is in the stack for drive/frames.
- Partials: `app/views/todos/_*.html.erb`; shared layout `app/views/layouts/application.html.erb`.
- JavaScript: importmap + Stimulus under `app/javascript/controllers/` (`javascript_importmap_tags` in the layout).
- Strong params: `params.expect(todo: [...])` in `TodosController`.

## Don'ts

- Do not add new gems without explicit approval.
- Do not put inline JavaScript in ERB (match existing importmap/Stimulus setup).
- Do not use `skip_before_action :verify_authenticity_token` (layout includes `csrf_meta_tags`).
- Do not commit secrets: `/.env*` and `/config/master.key` are gitignored; `.cursorignore` excludes credentials paths.
- Do not seed real or sensitive user data—use sample records in `db/seeds.rb` only.
