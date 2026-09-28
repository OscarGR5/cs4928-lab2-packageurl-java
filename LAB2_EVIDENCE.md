# CS4928 Lab 2 Evidence

## Baseline

Pinned SHA: cf437186b2ae2d9100a187e0df3cce3a163e9b4b

Upstream test suite:
- `mvn test`: PASS (143 tests, 0 failures, 0 errors, 0 skipped)

Baseline tag:
- `CS4928_BASELINE`

Independent checker:
- `mvn -Dtest=CS4928Lab2CheckTest test`: PASS (5 tests, 0 failures, 0 errors, 0 skipped)

## Build Setup

- Verified with Temurin JDK 21.0.12.1. JDK 17 is only required by the project's `release` profile, not for normal test runs.

## Problem A

validateName mixes general validation with package-type-specific normalisation.

Goal: move the varying name-normalisation algorithm behind a stable policy while preserving every existing result.
