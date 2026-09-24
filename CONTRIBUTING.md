# Contributing

This repository is the index. It has no package and no test suite beyond the name check in GitHub Actions.

A change should keep the nine library names in the README. The license is Apache-2.0.

The pre-commit hook is `.githooks/pre-commit`. It refuses a private key, a token, or an env file, then checks that the README still names the nine libraries. Enable it once in a clone:

```bash
git config core.hooksPath .githooks
```
