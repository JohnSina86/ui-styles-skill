# Evals

Two small data files. Neither runs automatically in this repo.

- `evals.json` follows the Anthropic skill-creator schema: `skill_name` and `evals[]`, each with `id`, `prompt`, `expected_output`, `files` and `expectations[]`.
- `trigger-eval.json` is a list of `{query, should_trigger}`. Ten queries should trigger the skill. Ten are **near-miss negatives**: they share keywords with the skill (design, theme, style, restyle) but need a different skill or no skill, such as a UX audit, a WCAG audit, matching an existing design system, or a task with no visual-style intent.

## Manual run: functional evals
1. Start a fresh session that has only this skill available.
2. Give it each `prompt` and keep the output.
3. Grade every entry in `expectations` as pass or fail against the output. Record a short reason for each failure.
4. For a baseline, repeat steps 1 to 3 in a session without the skill, and compare.

## Manual run: trigger evals
Take the queries in order. The queries alternate between positives and near-miss negatives, so each part of the split holds both labels. Use the first 12 as the tuning set and the last 8 as a held-out set: look at the held-out results only after you finish editing the description. For each query, note whether the skill loaded. A query is correct when the result equals `should_trigger`.

## Automated run (not run in this repository's release process)
Anthropic's skill-creator ships `run_eval.py` and `run_loop.py`, which run trigger queries through the `claude` CLI and split the queries themselves. They need `claude -p`. Pass them `trigger-eval.json` as the query set. The v1.2.0 release was prepared on a machine without that CLI, so the trigger set was reviewed by hand and **not** run through the automated tester.
