# CS4928 Lab 2 Evidence

## Baseline

Pinned SHA: cf437186b2ae2d9100a187e0df3cce3a163e9b4b

Upstream test suite:
- `mvn test`: PASS

Baseline tag:
- `CS4928_BASELINE`

Independent checker:
- `mvn -Dtest=CS4928Lab2CheckTest test`: PASS (5 tests, 0 failures, 0 errors, 0 skipped)

## Problem A

validateName mixes general validation with package-type-specific normalisation.

Goal: move the varying name-normalisation algorithm behind a stable policy while preserving every existing result.

## Refactoring A

Files/classes changed:
- PackageURL.java
- PackageNamePolicy.java
- PackageNamePolicies.java

Tests:
- `mvn test`: PASS
- `mvn -Dtest=CS4928Lab2CheckTest test`: PASS
- `git diff --check`: PASS

First commit SHA:
- 9b0adf2f131c5f1e1fe2b447ca0e305edafbe32d

Before → after:
Name validation previously contained both general validation and package-type-specific normalisation. The normalisation behaviour is now isolated behind reusable package-name policies, while observable behaviour remains unchanged.

## Problem B

Both qualifier parsing paths canonicalise keys to lowercase. The parsing responsibilities remain separate because the Map path filters empty values and overwrites keys, while the encoded-string path detects duplicate keys after canonicalisation.

## Refactoring B

Helper introduced:
- `PackageURL.canonicalizeQualifierKey(String)`

Tests:
- `mvn test`: PASS (143 tests, 0 failures, 0 errors, 0 skipped)
- `mvn -Dtest=CS4928Lab2CheckTest test`: PASS (5 tests, 0 failures, 0 errors, 0 skipped)
- `git diff --check`: PASS

Second commit SHA:
- 18eab46f7330b05035ca99ba71adb8f14b8b3fd0

Before → after:
The lowercase qualifier-key rule now has one source of truth. Map and encoded-string parsing remain separate to preserve their distinct filtering and duplicate-detection behaviour.

## Problem C

Package-type behaviour also occurs in namespace validation, version validation, and type-constraint verification; this wider variation is deliberately left for later because extending the policy now would make this bounded refactoring experiment larger and harder to verify.

## Final judgement

I would keep both changes in a real pull request. They make the varying name rules and shared qualifier-key rule easier to find and change; the trade-off is a small amount of additional indirection for behaviour that was previously inline.

## Repository

GitHub repository: https://github.com/OscarGR5/cs4928-lab2-packageurl-java

Refactoring B commit SHA: 18eab46f7330b05035ca99ba71adb8f14b8b3fd0
