# NameNotFound

> TODO: one line saying what NameNotFound is and who it is for.

A backend platform for online services for multiplayer games, built with C# and SQL Server.

**Status:** Phase 0 — base repository and foundations. _(Update this line at every phase.)_

## Why this project exists

<!-- Write this in your own words: which problem it solves, what you want to
     demonstrate, what you learned while building it. It is the first thing a
     reviewer reads. -->

TODO

## Scope

<!-- What the project includes and, just as important, what it does NOT include. -->

- TODO

## Stack

<!-- Fill this in with what you actually use; do not list technologies "just in case". -->

| Layer | Technology |
| --- | --- |
| Language | C# / .NET _(version: TODO)_ |
| Database | SQL Server |
| TODO | TODO |

## Prerequisites

- [Git](https://git-scm.com/)
- [.NET SDK 10](https://dotnet.microsoft.com/download/dotnet/10.0) (the exact rule is in `global.json`)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/) with Docker Compose
- At least 2 GB of free RAM and 2 GB of disk space for SQL Server
Check your setup:
 
```bash
git --version
dotnet --list-sdks     # must list a 10.0.x SDK
docker compose version
```

## Getting started

1. Clone the repository:
```bash
   git clone https://github.com/ItsSt0rm/NameNotFound.git
   cd NameNotFound
```
 
2. Create your local environment file and set a strong password in it:
```bash
   cp .env.example .env
```
 
3. Start SQL Server:
```bash
   docker compose up -d
```
 
4. Wait until the service shows `healthy`:
```bash
   docker compose ps
```
 
5. Connect with any SQL Server client to `localhost,1433` (or the port set in `MSSQL_HOST_PORT`), user `sa` and the password from `.env`.
### Stop and clean up
 
| Command | Effect |
| --- | --- |
| `docker compose stop` | Stops the container and keeps the data |
| `docker compose down` | Removes the container and keeps the data volume |
| `docker compose down -v` | Removes the container **and deletes all local databases** |

### Configuration and secrets

This repository **contains no secrets**. Sensitive configuration is managed outside version control (User Secrets in development, a secret store in deployment). Local files such as `appsettings.Development.json` and `.env` are listed in `.gitignore`.

## Repository structure

```text
.
├── README.md
├── LICENSE
├── .gitignore
├── .editorconfig
└── TODO   # code, documentation and test folders
```

## Architecture decisions

<!-- One short entry per decision: context, chosen option, discarded alternatives. -->

TODO

## Roadmap

- [x] Phase 0: base repository (README, license, `.gitignore`, `.editorconfig`)
- [ ] TODO

## License

Released under the MIT License. See the [LICENSE](LICENSE) file.
