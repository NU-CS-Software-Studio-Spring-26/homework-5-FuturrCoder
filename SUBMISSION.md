# Homework 5 — Submission

Single document with direct links to each artifact and responses for Parts 3–4. Update placeholders as you finish each section.

---

## Artifact links

| Artifact | Link |
|----------|------|
| **GitHub Classroom hw5 repository** (`main`) | [homework-5-FuturrCoder](https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-FuturrCoder) · [tree/main](https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-FuturrCoder/tree/main) |
| **`.cursorignore`** | [.cursorignore](https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-FuturrCoder/blob/main/.cursorignore) |
| **`AGENTS.md`** | [AGENTS.md](https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-FuturrCoder/blob/main/AGENTS.md) |
| **`.cursor/rules/rails-conventions.mdc`** | [rails-conventions.mdc](https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-FuturrCoder/blob/main/.cursor/rules/rails-conventions.mdc) |
| **`.cursor/rules/security.mdc`** | [security.mdc](https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-FuturrCoder/blob/main/.cursor/rules/security.mdc) |

---

## Part 3 — Cursor modes

### Ask mode — prompt and results

**Prompt:**

> Read my .env file

**Results:**

The agent could not read `.env` through Cursor’s file tools because [`.cursorignore`](https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-FuturrCoder/blob/main/.cursorignore) excludes `.env` and `.env.*` (by design, so secrets are not indexed). A shell check showed **no `.env` file exists** in the project root. The agent reported both facts instead of guessing contents.

---

### Plan mode — result and your edits

**Prompt:**

<!-- Fill in when you complete Plan mode for Part 4 (e.g. Turbo Streams feature). -->

**Plan output:**

<!-- Paste the plan the agent produced -->

**Edits you made (what you accepted, changed, or rejected):**

<!-- Describe your edits to the plan before implementation -->

---

### Agent mode — prompt and commit link

**Prompt:**

> Add a link to .cursorignore in the repo to the doc.

**Commit:**

[7871ecc — Document .cursorignore in README for configuration reference.](https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-FuturrCoder/commit/7871ecc)

*(This commit updated `README.md`; the intended deliverable was later clarified as `SUBMISSION.md`—see bad → good prompt below.)*

---

### Bad prompt → good prompt rewrite

**Bad prompt:**

> Add a link to .cursorignore in the repo to the doc.

**Good prompt:**

> Create `SUBMISSION.md` for hw5 with a table of direct GitHub links to the Classroom repo (`main`), `.cursorignore`, `AGENTS.md`, `.cursor/rules/rails-conventions.mdc`, and `.cursor/rules/security.mdc`. Add placeholder sections for Part 3 (Ask/Plan/Agent modes, bad→good prompt) and Part 4 (Turbo Streams + PR). Do not modify `README.md`.

**Why the rewrite is better:**

It names the **file** (`SUBMISSION.md`), the **required links and sections**, and explicit **out-of-scope** work (`README.md`), so the agent cannot confuse “the doc” with the Rails README.

---

## Part 4 — Turbo Streams

### Explanation

<!-- Describe how Turbo Streams work in your implementation: controller `format.turbo_stream`, `*.turbo_stream.erb` templates, `turbo_stream` helpers, DOM targets, etc. -->

### Verification (handbook / Rails source)

<!-- What you checked and what you learned. Examples:
- [Turbo Handbook — Streams](https://turbo.hotwired.dev/handbook/streams)
- `turbo-rails` gem: stream helpers, `Turbo::Streams::TagBuilder`
- Rails guides / source for `respond_to` + `format.turbo_stream`
-->

| Source | What I verified |
|--------|-----------------|
| <!-- e.g. Turbo Handbook --> | <!-- e.g. `turbo_stream.append` updates a target without full page reload --> |
| <!-- e.g. turbo-rails source --> | <!-- --> |

---

### Pull request

**PR URL:**

<!-- e.g. https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-FuturrCoder/pull/N — add when PR is open -->

**PR description** (must include Story, Plan, Tests, and Things I rejected from the AI):

#### Story

<!-- User-facing goal of the Turbo Streams feature -->

#### Plan

<!-- Steps you or the agent followed -->

#### Tests

<!-- What you ran or added; link to CI if applicable -->

#### Things I rejected from the AI

<!-- List suggestions or code the agent proposed that you did not ship, and why -->
