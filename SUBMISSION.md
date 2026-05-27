# Homework 5 - Submission

## Artifact links

| Artifact | Link |
|----------|------|
| **GitHub Classroom hw5 repository** (`main`) | [homework-5-FuturrCoder](https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-FuturrCoder) · [tree/main](https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-FuturrCoder/tree/main) |
| **`.cursorignore`** | [.cursorignore](https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-FuturrCoder/blob/main/.cursorignore) |
| **`AGENTS.md`** | [AGENTS.md](https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-FuturrCoder/blob/main/AGENTS.md) |
| **`.cursor/rules/rails-conventions.mdc`** | [rails-conventions.mdc](https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-FuturrCoder/blob/main/.cursor/rules/rails-conventions.mdc) |
| **`.cursor/rules/security.mdc`** | [security.mdc](https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-FuturrCoder/blob/main/.cursor/rules/security.mdc) |

---

## Part 3 - Ask mode

### Prompt used

```
Where in this codebase is todo editing currently implemented? Cite the exact files and line numbers. Do not propose changes.
```

### File paths and line numbers Cursor returned

- `config/routes.rb` - lines 2 - real
- `app/controllers/todos_controller.rb` - lines 2, 18-20, 37-48, 69-76 - real
- `app/views/todos/edit.html.erb` - lines 1-12 - real
- `app/views/todos/_form.html.erb` - lines 1-22 - real
- `app/views/todos/show.html.erb` - lines 5-6 - real
- `app/views/todos/index.html.erb` - lines 7-14 - real
- `app/views/todos/_todo.html.erb` - lines 1-7 - real
- `app/views/todos/show.json.jbuilder` - line 1 - real
- `app/views/todos/_todo.json.jbuilder` - line 1 - real
- `app/models/todo.rb` - lines 1-2 - real
- `test/controllers/todos_controller_test.rb` - lines 31-39 - real
- `test/system/todos_test.rb` - lines 24-33 - real

---

## Part 3 - Plan mode

### Prompt used

```
I want to change todo editing so that only the user who created a todo can edit it. Propose a plan as a numbered list of changes, including files to edit, new tests to add, and any migration. Do not write code.
```

(Cursor also asked how to identify the current user; I chose **User model + email/password login** — uncomment bcrypt in Gemfile, no new gems.)

### Plan returned

**Creator-only todo editing**

**Context:** Todos have no owner; no authentication. Edit/update are open in `TodosController`; edit link on `show.html.erb`. Approach: User + bcrypt + session login.

**Scope:** Restrict edit and update only. Require sign-in to create todos. Non-owners may still view. Unauthorized edit/update → 403 Forbidden (HTML and JSON).

**Numbered changes:**

1. **Enable bcrypt** — Uncomment `gem "bcrypt"` in `Gemfile`; `bundle install`.

2. **Migrations** — Create `users` (`email`, `password_digest`, unique email). Add `user_id` to `todos` (`null: false`, FK). Backfill existing rows if needed. Run `db:migrate`.

3. **Models** — New `app/models/user.rb` (`has_secure_password`, `has_many :todos`, email validations). Edit `app/models/todo.rb` (`belongs_to :user`).

4. **Session / current user** — Edit `application_controller.rb` (`current_user`, `logged_in?`, `require_login`). New `sessions_controller.rb` (login/logout). New `users_controller.rb` (sign-up).

5. **Todo controller authorization** — `require_login` on `new`/`create`; `authorize_todo_owner!` on `edit`/`update` (403 if not owner); `create` via `current_user.todos.build`; do not permit `user_id` in strong params.

6. **Routes** — `resource :session`; `resources :users, only: [:new, :create]`; keep `resources :todos`.

7. **Views** — Login and sign-up forms; layout auth links; conditional “Edit this todo” on show; optional forbidden template.

8. **Fixtures and seeds** — `test/fixtures/users.yml` (alice, bob); update `todos.yml` with owners; update `db/seeds.rb`.

9. **Test helper** — `sign_in_as(user)` in `test/test_helper.rb`.

10. **New and updated tests** — `user_test.rb`, `todo_test.rb`, `sessions_controller_test.rb`; update `todos_controller_test.rb` (owner success, non-owner/unauthenticated forbidden, create assigns owner); update `todos_test.rb` (system). Run `db:test:prepare test test:system` and `rubocop`.

11. **Documentation (optional)** — Brief note in `AGENTS.md` that authorization is owner-only on edit/update.

**Out of scope:** Devise/other auth gems, owner-only destroy, Pundit/CanCanCan, turbo_stream inline edit.

**Risk notes:** Existing tests need sign-in and fixture owners; bcrypt in fixtures; never mass-assign `user_id`.

### My edit

```
remove step 11
```

Removed step 11 (optional `AGENTS.md` documentation). Plan now ends at step 10 (tests).
