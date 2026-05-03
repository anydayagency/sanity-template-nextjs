# Commit Message Rules — Conventional Commits v1.0.0

When creating git commits, you MUST strictly follow the [Conventional Commits v1.0.0](https://www.conventionalcommits.org/en/v1.0.0/) specification. Every rule below is mandatory.

### Structure

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### Types

Use the correct type for the change being committed:

| Type       | When to use                                                        |
| ---------- | ------------------------------------------------------------------ |
| `feat`     | A new feature (correlates with SemVer MINOR)                       |
| `fix`      | A bug fix (correlates with SemVer PATCH)                           |
| `docs`     | Documentation-only changes                                         |
| `style`    | Formatting, whitespace, semicolons — no code logic change          |
| `refactor` | Code change that neither fixes a bug nor adds a feature            |
| `perf`     | A code change that improves performance                            |
| `test`     | Adding or correcting tests                                         |
| `build`    | Changes to the build system or external dependencies               |
| `ci`       | Changes to CI configuration files and scripts                      |
| `chore`    | Other changes that don't modify src or test files                  |

- `feat` and `fix` are the two types defined by the spec. The rest are recommended and permitted.
- Types MUST be lowercase nouns.

### Scope

- Optional. A noun in parentheses describing the section of the codebase affected.
- Examples: `feat(auth):`, `fix(parser):`, `docs(readme):`, `build(deps):`.
- Choose scopes that are meaningful within the specific project (e.g., module names, component names, service names).

### Description

- MUST immediately follow the colon and space after the type/scope prefix.
- Use the imperative, present tense: "add" not "added" nor "adds".
- Do NOT capitalize the first letter.
- Do NOT end with a period.
- Keep it concise — ideally under 72 characters.

- HARD LIMIT: The ENTIRE first line (type + scope + colon + space + description) MUST be under 100 characters total.  +Count every character. If it exceeds 100, shorten the description and move details to the body. Never exceed this limit 

### Body

- Optional. Separated from the description by ONE blank line.
- Use it to explain the **what** and **why** of the change, not the how (the diff shows the how).
- Free-form. May contain multiple paragraphs.

### Footer(s)

- Optional. Separated from the body (or description if no body) by ONE blank line.
- Each footer is formatted as: `<token>: <value>` or `<token> #<value>`.
- Footer tokens MUST use `-` (hyphen) in place of spaces (exception: `BREAKING CHANGE`).
- A footer's value MAY span multiple lines; the next footer token/separator pair terminates it.
- Common footers: `Refs: #123`, `Reviewed-by: Name`, `Co-Authored-By: Name <email>`.

### Breaking Changes

A breaking change (correlates with SemVer MAJOR) MUST be indicated by one or both of:

1. **A `!` immediately before the colon** in the type/scope prefix — e.g., `feat!:` or `feat(api)!:`.
2. **A `BREAKING CHANGE:` footer** — e.g., `BREAKING CHANGE: removed the X method`.

- `BREAKING CHANGE` MUST be uppercase.
- `BREAKING-CHANGE` (with hyphen) is a valid synonym.
- A breaking change can be part of ANY type.
- If the `!` is used, the `BREAKING CHANGE:` footer MAY be omitted only if the description sufficiently explains the break.

### Examples

```
feat: add user profile avatar upload
```

```
fix(auth): prevent token refresh race condition
```

```
feat(api)!: change pagination response format

BREAKING CHANGE: `next_page` field replaced with `cursor` in all list endpoints
```

```
docs: update contributing guidelines for new linter rules
```

```
refactor(cart): extract discount calculation into pure function
```

```
fix: resolve memory leak in websocket handler

Close the underlying connection when the client disconnects
instead of only removing the event listener.

Refs: #452
```

```
build(deps): upgrade react from 18.2 to 19.0

BREAKING CHANGE: drop support for Node 16
```

### What NOT to do

- Do NOT use types not listed above without a project-specific reason.
- Do NOT capitalize the type (`Feat:` is wrong — use `feat:`).
- Do NOT omit the space after the colon (`feat:add` is wrong — use `feat: add`).
- Do NOT write descriptions in past tense (`feat: added X` is wrong — use `feat: add X`).
- Do NOT put a period at the end of the description.
- Do NOT combine unrelated changes in a single commit — each commit should be atomic.
- Do NOT use `BREAKING CHANGE` in the body — it belongs in the footer section only.
