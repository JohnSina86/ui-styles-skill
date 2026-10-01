# Source scorecard

How the links in [related-resources.md](related-resources.md) were chosen. Read this when you need to justify a pick, or re-run the comparison.

## Contents
- [Method](#method)
- [Limits](#limits)
- [Winners and runners-up](#winners-and-runners-up)
- [Re-running a comparison](#re-running-a-comparison)

## Method
Seven categories were compared on **2026-10-01** by separate research agents. Each candidate was scored 0 to 5 on eight criteria and weighted:

| Criterion | Weight |
| :--- | :--- |
| Licence clarity and permissiveness | 3 |
| Maintenance (recent releases, open issues) | 2 |
| Accessibility evidence | 3 |
| Fit with `--ui-*` tokens | 2 |
| Delivery (copy-in, npm, self-hostable) | 1 |
| Documentation | 1 |
| Trust (named owner, track record) | 1 |
| Safety (telemetry, remote fetches, install scripts) | 1 |

The weights sum to 13, so the maximum is 65. Some agents reported out of 70 or 80 because they added a criterion or used different weights, so **compare totals only within one category**. The agent that compared companion skills used a different rubric (quality and footprint replaced safety) and scored out of 80.

Evidence came from the GitHub API (licence field, last push, releases), the npm registry, and each project's own docs pages. A score of 0 means "could not verify", not "proven bad".

## Limits
- **Reported, not verified.** Nobody installed these libraries or read most of their source. Licences, dates and star counts are as the agents read them on one day.
- **Accessibility scores are weak evidence.** Most sites document no accessibility behaviour, so scores rest on grep counts of `aria-` and reduced-motion terms in code, and on docs claims.
- **Safety scores are weak evidence.** Telemetry and install scripts were mostly not audited.
- **Some pages failed to load** (rate limits, JavaScript-only pages, 403 and 404). Those facts are marked unverified in the table below or in `related-resources.md`.
- **Self-scoring.** The companion-skills comparison included this skill's own repositories. Treat their rank as weak evidence.
- Packages and licences change. Treat a pick older than about a year as stale.

## Winners and runners-up
| Category | Winner | Runner-up | Score (max) |
| :--- | :--- | :--- | :--- |
| Unstyled primitives | Base UI | React Aria Components, Radix | 65 (65) |
| Styled kits | shadcn/ui | Mantine | 61 (65) |
| Animated copy-in components | Magic UI | Cult UI, Vengeance UI | 61 (70) |
| Icons | Lucide | Phosphor, Tabler | 65 (70) |
| Self-hosted fonts | Fontsource | google/fonts repository | 67 (70) |
| UI animation | Motion (tie with View Transitions API) | View Transitions API | 66 (70) |
| Vector animation | dotLottie | Rive | 53 (70) |
| AI thinking indicators | Thinking Orbs | prompt-kit TextShimmer | 60 (70) |
| Tables | TanStack Table | none | 63 (70) |
| Charts | Recharts | ECharts | 58 (70) |
| Illustrations | Open Peeps | Haikei | 44 (70) |
| Colour tools | Color.js | Radix Colors | 61 (70) |
| Companion skills | web-quality-skills (a complement), Impeccable (a generator) | ui-ux-pro-max | 74 and 71 (80) |

Candidates the owner asked about by name ranked as follows. Vengeance UI was third among the animated component sets. OriginKit, Skiper UI and Animmaster Lib ranked last, because of rate limits and a required key (OriginKit), no repository licence (Skiper UI) and paid delivery with unclear provenance (Animmaster Lib).

## Re-running a comparison
1. Pick a category and list candidates from search, not memory.
2. For each, read the licence file itself, the latest release or push date, and the project's accessibility notes.
3. Score with the table above. Mark anything you could not open as unverified.
4. Update the winner table, the date in `related-resources.md`, and the hazard list.
