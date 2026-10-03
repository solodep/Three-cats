# EK1 Foundation Implementation Plan

> **For agentic workers:** Use superpowers:executing-plans for inline implementation. Steps use checkbox (`- [ ]`) syntax. The user authorizes local work only; stop before any commit, tag or GitHub write.

**Goal:** Prepare a reviewable local EK1 draft and a server whose startup can be reproduced.

**Architecture:** A single ASP.NET Core Minimal API exposes a stateless health endpoint. The passport and security documents describe the future events/registration product separately from the running foundation.

**Tech Stack:** C#, .NET 10, ASP.NET Core; no third-party packages for this stage.

**Spec:** [PROJECT.md](../../../PROJECT.md).

## Global Constraints

- Implement only `GET /health` at this stage: HTTP 200, JSON `{"status":"ok","service":"three-cats-events"}`.
- Local startup binds to `127.0.0.1:5080` in the documented command.
- Authentication, event operations and SQLite are planned, not implemented or verified.
- Do not create or fill AI_USAGE.md and CONTRIBUTIONS.md until the user clarifies the seminar rules.
- Do not stage, commit, tag or push. Human review is the next handoff.

## Review Focus

- Missing .NET 10 SDK: README states the requirement and links the installer.
- Occupied port: README explains selecting a different port in both commands.
- Unknown routes and methods: must not masquerade as implemented product operations.
- Public health response: contains no configuration or credentials.
- Documentation: links and IDs resolve; no planned check is described as performed.

### Task 1: Product and security concept

**Files:** README.md, PROJECT.md, docs/security-requirements.md, docs/threat-model.md, docs/design-decisions.md.

- [x] Describe three complete scenarios, roles, states and data.
- [x] Define SR, concrete T, justified priorities and D with future checks.
- [x] Document actual foundation separately from future mechanisms; preserve pending human review, calibration and history.
- [x] Validate local links, identifiers and consistency of every priority chain.

### Task 2: Runnable foundation

**Files:** global.json, .gitignore, src/ThreeCats.Events.Api/ThreeCats.Events.Api.csproj, src/ThreeCats.Events.Api/Program.cs.

**Interface:** `GET /health` returns HTTP 200 and the exact JSON object above; no application data or state is involved.

- [x] Build a minimal Web SDK project without external packages.
- [x] Before adding the health route, confirm an actual GET receives 404.
- [x] Map the health endpoint and rebuild with zero warnings/errors.
- [x] Confirm GET returns 200 and the specified JSON; unknown paths return 404 and POST /health does not succeed.
- [x] Verify build output is ignored and the worktree contains only intended source/documents.
- [x] Stop for user review before creating any commit.

## Verification record

Local .NET SDK 10.0.401: build completed with zero warnings and zero errors. Before the route was implemented, the HTTP probe failed on GET /health = 404. After implementation: GET /health = 200 with the specified JSON; unknown path = 404; POST /health = 405. Probe processes were stopped. Ten intended files passed whitespace, Markdown-fence and local-link checks; SR/T/D IDs resolve. A separate reviewer found no material inconsistencies. No HEAD exists and no files are staged.

For this small stateless scaffold, use direct HTTP checks rather than a test project that mirrors the endpoint. Authorization and concurrency tests belong to the later domain implementation.
