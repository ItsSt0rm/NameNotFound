# Contributing to NameNotFound

This guide explains how work reaches the repository and which conventions every change follows.

## Workflow in one minute

1. Every change starts from an **issue**. Its number is the `ID` used in branch names.
2. Create a short-lived **branch** from an up-to-date `main`.
3. Write commit messages with **Conventional Commits**.
4. Open a **pull request** that closes the issue.
5. Merge into `main` when the pull request is ready. `main` is protected: direct pushes are rejected.
6. Delete the branch after merging.

Once the CI workflow exists (see #6), its checks must pass before merging.

## Branches

Format:

```text
type/ID-short-description
```

- `type`: one of `feature`, `fix` or `chore`.
- `ID`: the number of the issue the branch works on.
- `short-description`: a few lowercase words in English, separated by hyphens.

Examples:

```text
feature/12-player-login
fix/15-token-expiry
chore/4-naming-conventions
```

| Type | Use it for |
| --- | --- |
| `feature` | New functionality |
| `fix` | Bug fixes |
| `chore` | Everything else: configuration, tooling, CI, documentation |

Rules:

- One branch per issue.
- Branches are short-lived: create, merge, delete.

## Commit messages

Commits follow [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/):

```text
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

| Type | Use it for |
| --- | --- |
| `feat` | A new feature |
| `fix` | A bug fix |
| `docs` | Documentation only |
| `refactor` | Code change that neither fixes a bug nor adds a feature |
| `test` | Adding or correcting tests |
| `ci` | CI configuration |
| `build` | Build system and dependencies |
| `chore` | Maintenance that fits none of the above |

Rules:

- The description is short, in the imperative mood, lowercase and without a final period (for example, `add player login endpoint`).
- The scope names the part of the code that changes, usually a module.
- Reference the issue in a footer: `Refs: #12`.
- Mark a breaking change with `!` before the colon (`feat(api)!: ...`) or with a `BREAKING CHANGE:` footer.

Example:

```text
feat(auth): add player login endpoint

Refs: #12
```

A `feature/` branch usually produces `feat` commits and a `fix/` branch produces `fix` commits. A `chore/` branch can use `chore`, `docs`, `ci`, `build`, `test` or `refactor`.

## Versioning

Versions follow [Semantic Versioning 2.0.0](https://semver.org/): `MAJOR.MINOR.PATCH`.

| Bump | When | Commits that cause it |
| --- | --- | --- |
| `PATCH` | Backwards-compatible bug fixes | `fix` |
| `MINOR` | Backwards-compatible new functionality | `feat` |
| `MAJOR` | Incompatible changes | Any commit marked as a breaking change |

- `docs`, `ci`, `chore` and similar types do not change the version by themselves.
- While the project is in initial development, versions start with `0.` (`0.y.z`) and anything may change.
- Version tags use the form `v1.2.3`.
- How the next version is calculated automatically is defined in #8.

## .NET project names

Projects follow the pattern `Platform.Module.Layer`. The platform is `NameNotFound`.

```text
NameNotFound.Players.Api
NameNotFound.Players.Application
NameNotFound.Players.Domain
NameNotFound.Players.Infrastructure
NameNotFound.Players.Application.Tests
```

- **Module:** a business capability, in PascalCase. The examples above are illustrative: the real modules are defined later.
- **Layer:** the architectural layer, for example `Api`, `Application`, `Domain` or `Infrastructure`.
- **Tests:** a test project adds the `.Tests` suffix to the name of the project it tests.
- The root namespace of a project matches the project name.

## Pull requests

- The title follows Conventional Commits, so the history stays consistent whichever merge method is used.
- The description uses the pull request template and includes `Closes #<issue>`, so the issue closes when the pull request is merged into `main`.
- Keep each pull request small and focused on one issue.
- Never include secrets, credentials or personal data in a change.

## Code style

The `.editorconfig` at the root of the repository defines formatting and C# style rules. Let your editor apply them.
