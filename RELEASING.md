# Releasing

Run this checklist before tagging. Each step is a manual check that doesn't need a script.

1. **Frontmatter:** `name` is `ui-styles` (the install folder name), the description is at most 400 characters, third person, with a "Use when" and a "Not for" clause, and **contains no hard-coded counts**. `metadata.version` matches the tag.
2. **Size:** `SKILL.md` is at most 200 lines. Every file in `references/` is linked from `SKILL.md`. Every file over 100 lines starts with a table of contents.
3. **Style index parity:** every ID in the `SKILL.md` style index has exactly one `.theme-<id>` block, in the file named in its `Tokens` column. Every style ID in `references/product-fit.md` (Primary, Secondary, Avoid columns) exists in the index.
4. **Contrast:** recompute any row you touched, using the method in `references/contrast-ledger.md`. If you changed a recipe colour or alpha in `references/styles-catalog.md` (CSS `rgba()` or a Tailwind utility such as `bg-white/12`), recompute the ledger row it cites. Update the "Verified on" date.
5. **Pointers:** search the repository for `SKILL.md §` and for "token block in". Nothing may point to a section that doesn't exist.
6. **Demo:** open `examples/cyberpunk-glass.html`. Tab to each button: the focus ring must be visible and unclipped. The glass card text must be readable over the white section.
7. **Cross-skill:** every `ux-laws #N` citation in the style index or token files matches the law numbers in `ux-laws`.
8. **Evals:** run the four functional evals by hand (`evals/README.md`) and record the result in the release notes.
9. **Tag:** `git tag -a vX.Y.Z -m vX.Y.Z` after merging, then update the README's install commands and the changelog.
