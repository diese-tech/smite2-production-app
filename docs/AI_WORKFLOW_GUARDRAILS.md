# AI Workflow Guardrails

Review this document before implementation, debugging, refactoring, migrations, or production fixes in this repository.

## Core Rule

Move fast, but move surgically. Prefer the smallest safe change that solves the measured problem. Avoid broad rewrites, speculative refactors, or unrelated cleanup.

## Repo-Specific Focus

- Protect realtime production overlay behavior.
- Keep state synchronization explicit and observable.
- Minimize startup and module load costs.
- Bound event fan-out and retry behavior.
- Prefer queue-based processing where slow work can grow.
- Avoid broad rewrites in production tooling.
- Minimize blast radius during overlay and state changes.

## Required Before Changing Code

- Identify the specific problem and files likely involved.
- Name the expected impact and rollback path.
- Check whether the change affects live production usage, overlay state, background jobs, data integrity, or production operations.
- Avoid touching unrelated files.

## Architecture Defaults

- Prefer queue-based async processing over synchronous fan-out.
- Prefer append-only events or buffers over hot shared state.
- Prefer bounded event fan-out and explicit backpressure.
- Prefer indexed or projected reads over repeated raw scans.
- Prefer idempotent and retry-safe jobs.

## Change Review Checklist

Before finalizing a change, answer what changed, why it is safe, what could break, how to roll back, and what validation proves the change.
