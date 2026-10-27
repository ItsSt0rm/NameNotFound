# ADR-0001: Branching strategy

- **Status:** Accepted
- **Date:** 2026-10-26
- **Deciders:** ItsSt0rm
- **Related issue:** #3

## Context

NameNotFound is a backend platform for online services for multiplayer games. The project needs a branching strategy from day one, with these constraints:

- Work must reach the main branch only through pull requests, with continuous integration (CI) passing and no direct pushes.
- A versioned artifact is generated every time something is merged into `main` (preliminary continuous delivery, issue #8). Real deployment arrives in Phase 1.
- The project is a web backend that is continuously delivered, not software shipped in numbered releases to be installed by customers.
- There is currently a single maintainer, and only one version of the platform is expected to be in production at any time.
- Branches follow the `type/ID-short-description` naming convention, defined in [CONTRIBUTING.md](../../CONTRIBUTING.md).

Two well-known models were evaluated: GitFlow and GitHub flow.

## Decision

NameNotFound uses **GitHub flow**: a single long-lived branch, `main`, plus short-lived branches that are merged through pull requests and then deleted.

1. `main` is the only long-lived branch. We keep it in a releasable state, and the CI checks exist to enforce that.
2. All work happens on short-lived branches created from an up-to-date `main`: `feature/`, `fix/` or `chore/`, named `type/ID-short-description` (see [CONTRIBUTING.md](../../CONTRIBUTING.md)).
3. A branch reaches `main` only through a pull request. The pull request closes its issue.
4. The branch is deleted after the merge.
5. Releases are version tags on `main`, following Semantic Versioning. There are no `develop` or `release` branches.
6. A hotfix is a normal `fix/` branch merged into `main`.

### Protection of `main`

A branch ruleset is active on `main` with these rules:

- Require a pull request before merging. Required approvals are set to 0 because there is a single maintainer; the pull request itself remains mandatory.
- Block force pushes.
- Restrict deletions.
- Empty bypass list, so the rules also apply to the repository owner.
- Require the CI status check to pass. This rule is added when the CI workflow exists (issue #6).

## Alternatives considered

### GitFlow

GitFlow, as described by its author, uses two long-lived branches (`master` and `develop`) and three kinds of supporting branches: feature branches off `develop`, release branches to prepare a version, and hotfix branches off `master`.

It was rejected for these reasons:

- It is designed for explicitly versioned software, or for supporting several versions in the field. NameNotFound has neither need: there is one version in production.
- Its author states in a note added to the original article (March 2020) that it does not fit continuous delivery well, that web apps are typically continuously delivered and not rolled back, and that teams doing continuous delivery should adopt a much simpler workflow, like GitHub flow.
- It adds long-lived branches (`develop`, `release/*`) and merges to keep in sync, with no benefit for a single maintainer.
- The planned CD pipeline (a versioned artifact on every merge into `main`) maps directly onto a single main branch, and would need extra rules for a `develop` branch.

### Committing directly to `main`

Rejected. It contradicts the requirement that every change goes through a pull request with CI passing.

## Consequences

- **Positive:** a simpler model with fewer branch types to remember; a linear path from issue to branch to pull request to `main`; CI and CD hook onto a single branch.
- **Negative:** nothing in the branch structure separates unfinished work from releasable work, so `main` stays releasable only if CI is strict and changes are small. Incomplete features must be merged in a way that does not break `main`.
- **Negative:** supporting several released versions in parallel is not covered by this model.
- **Revisit when:** NameNotFound has to maintain more than one released version at the same time (for example, a public API with versions kept in parallel). In that case, maintenance branches such as `release/x.y` can be introduced for those versions, recorded in a new ADR that supersedes this one.
- **Not decided here:** the merge method (merge commit, squash or rebase) and the exact CI checks.

## References

- Vincent Driessen, [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/), including the March 2020 note.
- GitHub Docs, [GitHub flow](https://docs.github.com/en/get-started/using-github/github-flow).
- GitHub Docs, [About rulesets](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets).
