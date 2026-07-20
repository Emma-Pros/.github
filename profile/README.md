# Emma Pros — Engineering

Internal tooling for Emma Transit & Emma Logistics operations.

## Coding & Committing Best Practices

1. **Small, focused commits.** One logical change per commit; don't mix refactors with features.
2. **Write clear commit messages.** Imperative mood, present tense ("Add tracking export", not "Added"). Explain *why* in the body when it isn't obvious.
3. **Branch off `main`.** Never commit directly to `main`; open a PR for review.
4. **Keep secrets out of git.** No API keys, tokens, or credentials in code — use environment variables and `.env` (git-ignored).
5. **Pull before you push.** Rebase or merge latest `main` to avoid conflicts.
6. **Review your own diff first.** Run `git diff` before every commit to catch debug logs, stray files, and accidental changes.
7. **Test before you push.** Run the app/tests locally; don't push code you haven't run.
8. **Descriptive names.** Clear variable, function, and file names over comments explaining unclear ones.
9. **Match the existing style.** Follow the conventions already in each repo (formatting, structure, naming).
10. **Open a PR early.** Draft PRs invite feedback sooner and keep work visible.
