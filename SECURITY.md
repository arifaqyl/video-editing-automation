# Security Policy

## Supported Scope

This repository is intended for public code and local-only configuration.

Do not open public issues for:
- API keys
- bot tokens
- chat IDs
- local file paths that expose private data
- raw media that should remain private

## Reporting

Report security issues privately to `hello@arifaqyl.me`.

Include:
- affected file or workflow
- reproduction steps
- impact
- whether any credential may need rotation

## Local Safety Rules

- keep `.env` local
- do not commit Telegram tokens or chat IDs
- rotate any token immediately if it was ever exposed
