# test-lefthook-and-pre-commit

## Using lefthook

```bash
lefthook install
time lefthook run pre-commit
```

## Using pre-commit

```bash
pre-commit install
time pre-commit run
```

## Using both

```bash
# Clean
rm .git/hooks/pre-commit
rm .git/hooks/pre-commit.legacy

# Install lefthook
lefthook install
mv .git/hooks/pre-commit .git/hooks/lefthooks-hooks

# Install pre-commit
pre-commit install
mv .git/hooks/pre-commit .git/hooks/pre-commit-hooks

# Hack to run both
echo -e '#!/usr/bin/env bash
echo "[HOOKS] Running lefthook hooks"
bash .git/hooks/lefthooks-hooks
echo "[HOOKS] Running pre-commit hooks"
bash .git/hooks/pre-commit-hooks' > .git/hooks/pre-commit
chmod +x .git/hooks/pre-commit

# Test both
echo "test" >> README.md
git commit -am"feat: test both"
```
