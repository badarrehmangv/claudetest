# Poki design-trait analysis: which features correlate with traction

Analyst output, 2026-09-29. Inputs: `poki/games.jsonl` (1,503 live games), `poki/homepage.json`, plus Poki blog/docs pages quoted below. Reproduce every number with `python3 analysis/features_analysis.py` (the controls classifier is in `analysis/features_common.py`).

**How to read this.** Votes (up + down) are a proxy for player volume. They are **not plays**. Votes/day = votes / max(days since release, 7) is the traction proxy. **RTI** (cohort-relative traction index) = votes/day divided by the median votes/day of games released in the same quarter; 1.0 is typical. "Top quartile" = the best 25% of the 643 games released 2024-01-01 or later, ranked by RTI (160 games, RTI >= 2.79). "Lift" = a trait's share among the top quartile divided by its share of all 2024+ releases. All-time top-100 = the 100 most-voted games. Everything here is correlation from surviving games only. Section 0 below has the full caveats.

## Key findings (most decision-relevant first)

1. **Online and social play is the strongest positive signal, and supply is still thin.** Games with any social tag (2 Player / Multiplayer / .io / Co-op / 1v1) are 15% of 2024+ releases but 28% of the top quartile: median 198 votes/day vs 80.5 for games without one, median RTI 2.24 vs 0.90, lift 1.82. The individual tags: `.io Games` n=17, median RTI 5.85, lift 2.84; `Multiplayer Games` n=61, RTI 2.40, lift 1.78; `2 Player Games` n=36, RTI 1.67, lift 1.67. They also over-index all-time: Multiplayer has 33 of the top-100 against 10% of the catalogue, and 2 Player has 25 against 9% (dataset, section 3). After the regression controls, `.io` stays significant (x3.38, t=3.3), while Multiplayer and 2 Player stay positive but are not significant (x1.30 and x1.36) because they overlap with 3D and .io (dataset, 5c). Poki's 2026 report: "web games are highly social" and "54% of surveyed consumers play web games with a friend or family member 'very often'" (https://poki.com/blog/state-of-web-gaming-report-2026).
2. **3D over-performs, but the 3D share of new releases is rising fast.** Tagged `3D Games`: 24% of 2024+ supply and 37% of the top quartile; median 187 votes/day vs 76.6 for untagged; RTI 1.85 vs 0.87; lift 1.56. It is still x1.35 after controls (t=2.1). The 3D share of releases grew from 17% (2024) to 24% (2025) to 30% (2026) (dataset, sections 4 and 5c). Inference: the 3D premium is real but shrinking as competition grows.
3. **Keyboard-movement and "rich" controls correlate with traction, mostly because of genre.** Keyboard-movement games (WASD/arrows) are 46% of 2024+ supply and 58% of the top quartile (lift 1.24). Traction climbs with the number of extra inputs: median RTI 0.93 with none, 1.03 with 1, 1.84 with 2, and 2.64 with 3 or more (complex). Complex controls take 25 of the all-time top-100 against 8% of the catalogue (lift 3.24). Keyboard movement plus mouse look/aim has median 348 votes/day (dataset, section 1). But in the regression, complex is only x1.62 (not significant, t=1.8) and few-keys is x1.01. 16 of the 37 complex 2024+ games are 3D and 16 are Multiplayer, so the effect is mostly genre (3D shooters, driving, multiplayer), not the key count itself (dataset, 5c). Poki's guidance still asks for "simple controls ... interacted with through keyboard or mouse or touch" (https://poki.com/blog/what-makes-high-quality-browser-game).
4. **Mouse/tap-only is the crowded default and under-indexes. One-button is hit-or-miss.** Mouse/point-click-drag is 49% of 2024+ supply, with median RTI 0.91, lift 0.76 and all-time top-100 lift 0.49. One-button/tap/hold is only 30 games: median RTI 0.60 (weak typical outcome) but lift 1.07, carried by outliers. Slice Master has 2,622 votes/day and holds homepage #5; Neon Challenge Legends has 2,547/day; Blumgi Bounce holds homepage #15 (dataset, sections 1 and 7).
5. **Support both mobile orientations: this is table stakes now.** "Both" rose from 60% of 2024 releases to 76% (2025) and 88% (2026). Landscape-only fell from 23% to 14% to 5%. Of the 643 games released 2024+, **93 are landscape-only on mobile** (54 in 2024, 29 in 2025, 10 in 2026), and 24 are desktop-only (dataset, section 2). Poki: "Every game submitted to Poki needs to work in portrait, and our QA team tests for it" and asking players to rotate is "a conversion killer" (https://poki.com/blog/building-web-browser-games-2026). In votes, landscape-only is neutral (median RTI 1.00, lift 0.95) and portrait-only is below par (RTI 0.82, lift 0.83). Inference: the landscape penalty is a platform-acceptance issue rather than a vote issue, so build for both orientations.
6. **Desktop-only is the single worst trait.** Median RTI 0.23, regression x0.30 (t=-3.9). A few desktop-only hits exist, such as Blockpost at 4,222 votes/day, but the typical desktop-only game is weak (dataset, sections 2 and 5c).
7. **Themes that over-perform relative to supply (2024+, lift / median RTI):** Stickman (n=21) 2.49 / 3.46; Obby (n=17) 2.36 / 4.11, with 8 in the all-time top-100 against 2% of the catalogue; Parkour (n=19) 1.69 / 2.07; Horror/scary (n=32) 1.63 / 1.95; Sports (n=60) 1.54 / 1.81; Cars/driving/racing (n=100) 1.53 / 1.83; Shooting (n=135) 1.46 / 1.41; Ragdoll/physics (n=48) 1.42 / 1.29 (dataset, 5a). Every one of these tested in 5d keeps lift above 1.2 in both the indie-only and the 90+-days subsets.
8. **Dress-up/makeover/decorating has the strongest theme effect after controls.** n=86, median RTI 1.62, lift 1.17, and x2.06 in the regression (t=4.1). Indie examples: SnapStyle Dress Up at 1,999 votes/day and Vortella's Dress Up at 1,239,199 votes (dataset, sections 5 and 6c). Inference: this audience may vote more readily, so treat the size of the effect with some caution.
9. **Themes that clearly under-perform despite heavy supply:** Merge is 10% of 2024+ supply with median RTI 0.28, lift 0.30, regression x0.48 (t=-3.7), and only 1 game in the all-time top-100. Puzzle/brain is 28% of supply with RTI 0.51, lift 0.58, regression x0.62 (t=-3.1). Sorting/organizing (n=21) has RTI 0.29 and lift 0.19. Idle/clicker is 15% of supply with lift 0.60. Tycoon/management has lift 0.74; story/narrative (n=13) has lift 0.31; animals/pets has lift 0.79 (dataset, 5a and 5c). Merge Rot (1,151 votes/day, brainrot theme) and Blumgi Merge (RTI 3.04) are the exceptions.
10. **Generic structure words do not separate winners from losers.** Level-based (lift 0.88), endless/high-score (1.14), upgrades (0.94), collect/unlock (0.97) and customization/skins (1.23) all sit near neutral; where tested in the regression, their multipliers fall between 0.83 and 1.10 and none is significant (dataset, 5 and 5c). Inference: the core fantasy and genre matter more than the meta-loop label.
11. **Brainrot/meme is modestly positive and trend-dependent.** n=33, median RTI 1.30, lift 1.10, regression x1.47 (not significant). The biggest one, Steal a Brainrot, is "the official browser version of the hit multiplayer action game", an external IP (dataset).
12. **Developer portfolio: the sweet spot is 2-9 games; single-game developers and 10+ game "factories" both under-index.** For 2024+ games by portfolio size, lift and median RTI are: 1 game 0.78 / 0.80; 2-4 games 1.18 / 0.98; 5-9 games 1.17 / 1.28; 10+ games 0.78 / 0.99, with 10+ at x0.73 in the regression (t=-2.1) (dataset, 6 and 5c). Developers with 3+ games hold 82% of all votes (co-credits can double count).
13. **Later games do NOT reliably beat earlier ones.** Across 147 developers with 3+ dated games, the median Spearman correlation between release order and RTI is -0.20. The later half beats the earlier half for only 40% of developers, and 48% among the 52 developers whose catalogue starts in 2023 or later. Games numbered 11th and beyond have median RTI 0.55 (dataset, 6a). Inference: shipping more does not by itself raise hit odds; each game needs a strong hook.
14. **Blumgi vs AJ Ordaz is the clearest contrast.** Blumgi: 13 games (including 3 co-developed), 4,120,843 votes, median 225,455 votes per game, median RTI 3.02, rank #23 of 434 developers. 9 of Blumgi's 13 games are one-button or mouse, and every release since 2024 is mobile "both" or portrait. The latest, Blumgi Splash, has RTI 0.48, so even Blumgi misses. AJ Ordaz: 8 games, 218,296 votes, median 15,578 per game, median RTI 0.44, rank #191. Of his five keyboard-movement titles, the A Pretty Odd Bunny pair reached RTI 1.00-1.30 and the other three only 0.17-0.37. His newest, Trapped in the Dollhouse (mouse, both orientations, 352 votes/day, RTI 2.05), is his best by traction (dataset, 6b).
15. **Poki promotes fresh games heavily.** 108 of the 145 desktop homepage slots are 2024+ releases, and 54 of them are from 2026. 22 of the top-30 2025-26 indie performers are on today's homepage (dataset, section 7).
16. **Profile of the top-30 2025-26 indie/web-first performers:** 27 of 30 support both mobile orientations, 15 are 3D-tagged, and 5 are Multiplayer-tagged. Controls: 14 mouse/tap, 9 keyboard-move with few keys, 5 complex, 2 one-button. 17 of the 30 come from developers with 4 or fewer games (dataset, section 7). The winning clusters are: online 3D multiplayer (Blockpost, Hide and Paint, Monkey Tag IO); one-tap skill (Slice Master, Neon Challenge Legends); crowd runners (Count Control Legends); dress-up and makeover (SnapStyle, Beauty Salon, Super Dress); sports with aim-and-release (Soccer REAL, World Soccer Champions); and physics toys (Planet Destruction, Ragdoll Chaos).
17. **Brands and external IP get a large premium, which indies compete against.** 63 flagged 2024+ games have regression x2.51 (t=4.6). 11 flagged titles would otherwise sit inside the top-30 range, such as Hole.io, Talking Tom Gold Run and Kick The Buddy (dataset, 5c and 7; the flag list is analyst Inference).

**Implied design brief (Inference):** Build a 3D or physics-driven game that supports both mobile orientations. Use WASD plus at most 2 extra inputs on desktop, with a thumb-friendly equivalent on mobile. Give it a social hook: an async or online multiplayer, .io, or local 2-player mode. Pick a theme from the over-performing set (obby/parkour, stickman, sports, driving, horror-lite, ragdoll, or dress-up if targeting that audience). Avoid merge, sorting, idle and pure puzzle unless the theme itself is the hook (as with Merge Rot).

---

# Detailed analysis

## 0. Method, definitions and caveats

- **Votes are not plays.** `votes = up + down` (thumbs votes) is the best available proxy for cumulative player volume; `votes/day = votes / max(days since release_date, 7)` is the proxy for current traction. Only a small, unknown fraction of players vote, and that fraction may vary by genre, audience age and device. Every "traction" statement below is about votes (dataset).
- **Recent cohort ("2024+")**: games with release_date >= 2024-01-01. n = 643 (dataset: count of rows with non-null release_date >= 2024-01-01). The 32 null-release rows (likely soft launches) are excluded from all dated analysis.
- **Age bias.** Median votes/day rises for newer cohorts (dataset: median votes/day by release quarter was 60.7 for 2024Q1, 88.5 for 2025Q1, 131 for 2026Q1 and 172 for 2026Q3), probably because of launch promotion and the 7-day floor. To compare games of different ages fairly, this report also uses a **cohort-relative traction index (RTI)** = a game's votes/day divided by the median votes/day of all games released in the same calendar quarter (dataset). RTI 1.0 = a typical game of its launch quarter; 2.0 = twice the typical traction. Games on the 2019-03-11 bulk migration date form one "legacy" cohort.
- **Recent top performers** = top quartile of the 2024+ cohort by RTI (n = 160). A second cut, **top-50 by raw votes/day**, is shown too. **Lift** = (share of the group among top performers) / (share of the group among all 2024+ games). Lift above 1 means the trait is over-represented among winners compared with its supply.
- **All-time top-100** = the 100 games with the most votes across all 1,503 games. "Lift top-100" = (share among top-100) / (share among all 1,503).
- **Survivorship**: the dataset holds only games still live today. Removed or failed games are invisible, so older cohorts look stronger than they were. Read differences as correlations, not causes.
- Medians are used everywhere because votes are extremely skewed.

## 1. Controls complexity

Controls text = the `controls` field. When it was empty (70 rows), the "How to play X? ..." passage of `description` was used instead, and 1 row had neither (dataset). Rules, applied in order (implemented in `features_common.py::classify_controls`):

1. **Movement present** if the text has `WASD`, `W, A, S, D`, `arrow keys`, `A/D` or `A or D`, `joystick`, `left/right`, or names at least two different directions with arrow/key. A single "Up arrow" used as a button counts as a key, not as movement.
2. Clauses used only for restart, reset, respawn, pause, go back, menu, fullscreen or mute are dropped before keys are counted, and Esc is ignored. These are not gameplay inputs.
3. **Extra inputs** are counted as distinct items: Spacebar, Shift, Ctrl, Enter, Tab, number keys, a single arrow key, and any stand-alone capital letter used as a key (Z, X, E, F ...). W/A/S/D are not counted when movement is present, and "A" counts only when used like a key. For movement games, a mouse action (shoot, attack, aim, look, camera, right-click) counts as one more input.
4. **Complex**: movement plus 3 or more extra inputs; or, with no movement, 4 or more distinct keys that are not alternatives for a single action; or mouse plus 3 or more keys.
5. **Keyboard movement + few keys**: movement plus at most 2 extra inputs (typically Spacebar and/or one action key, or mouse camera).
6. **One-button / tap / hold-release**: no movement and no pointing words (drag, select, choose, aim, cursor, match, merge, paint, tiles, items, buy, upgrade ...), and either (a) 1-3 keys that are alternatives for one action verb ("Spacebar, Up arrow, or Mouse click to jump"; per-player versions such as "A for Player 1. L for Player 2." are allowed up to 5 keys), or (b) at most Spacebar plus a hold/release or tap-to-verb pattern ("tap to jump/flip/shoot/launch ...").
7. **Mouse-only / point-click-drag**: no movement keys, mentions mouse/click/tap/drag/cursor/finger/swipe, and at most 2 keys. Generic "Click or tap to play" text falls here because it is ambiguous.
8. Other keyboard (typing games, 2+ action keys without movement) / no controls text.

Limitations: this is a keyword classifier. Local 2-player games that list both players' keys can count as "complex" even when each player uses only 3 keys, and a few pointer games whose text has no pointing words can land in one-button. Many "mouse-only" games are also tap-only on mobile, and Poki's standard text "Click or tap to make the choice" hides the real mechanic. The classifier was spot-checked on about 150 random rows.

| Group | n (2024+) | share of 2024+ | median votes/day | median RTI | in 2024+ top-quartile (n, share) | lift vs supply | in 2024+ top-50 by votes/day | n all-time (share of 1,503) | in all-time top-100 | lift top-100 vs catalogue | on homepage (2024+ games) |
|---|---|---|---|---|---|---|---|---|---|---|---|
| One-button / tap / hold-release | 30 | 5% | 65.3 | 0.60 | 8 (5%) | 1.07 | 3 | 106 (7%) | 8 | 1.13 | 7 |
| Mouse-only / point-click-drag | 313 | 49% | 80.5 | 0.91 | 59 (37%) | 0.76 | 17 | 706 (47%) | 23 | 0.49 | 40 |
| Keyboard movement (WASD/arrows) + <=2 keys | 260 | 40% | 107 | 1.05 | 75 (47%) | 1.16 | 22 | 557 (37%) | 43 | 1.16 | 47 |
| Complex (many keys / mouse-aim + keys) | 37 | 6% | 234 | 2.64 | 17 (11%) | 1.85 | 8 | 116 (8%) | 25 | 3.24 | 14 |
| Other keyboard (typing / 2+ action keys, no movement) | 1 | 0% | 35.7 | 0.62 | 0 (0%) | 0.00 | 0 | 10 (1%) | 0 | 0.00 | 0 |
| No controls text | 2 | 0% | 192 | 1.99 | 1 (1%) | 2.01 | 0 | 8 (1%) | 1 | 1.88 | 0 |
| (overlap) any keyboard-movement game that also uses a mouse action/look/aim | 48 | 7% | 348 | 2.84 | 25 (16%) | 2.09 | 6 | 86 (6%) | 12 | 2.10 | 17 |
| (overlap) simple input = one-button + mouse-only | 343 | 53% | 79.1 | 0.90 | 67 (42%) | 0.79 | 20 | 812 (54%) | 31 | 0.57 | 47 |
| (overlap) keyboard movement, any = few keys + complex | 297 | 46% | 115 | 1.13 | 92 (58%) | 1.24 | 30 | 673 (45%) | 68 | 1.52 | 61 |

Examples of each class among the 2024+ top-quartile (dataset):

- **One-button / tap / hold-release**: Slice Master ("Mouse click to launch the knife. Tap to launch the knife."); Bullet Bros ("Hold mouse click or Spacebar to jump and rotate. Release to shoot."); Neon Challenge Legends ("Hold W, Up arrow, Spacebar, or Mouse click to move up. Release to move..."); 12 Mini Battles 2 ("A for Player 1. L for Player 2.")
- **Mouse-only / point-click-drag**: SnapStyle Dress Up ("Click or Tap to make a choice."); World Soccer Champions ("Use the mouse to aim. Swipe and release to shoot."); Blocky Blast Puzzle ("Drag blocks onto the board using the mouse. On mobile, tap and drag bl..."); Nails DIY: Manicure Master ("Tap or mouse click to choose nail polish or stickers. Hold and drag to...")
- **Keyboard movement (WASD/arrows) + <=2 keys**: Crossy Road ("Use the Up arrow, Down arrow, Left arrow, and Right arrow to move side..."); My Perfect Hotel ("Use W, A, S, D or the Up arrow, Down arrow, Left arrow, Right arrow to..."); Stunt Bike Extreme ("Up arrow to move forward. Down arrow to stop. Left arrow and Right arr..."); MR RACER - Car Racing ("W or Up arrow key to accelerate. S or Down arrow key to brake. A or Le...")
- **Complex (many keys / mouse-aim + keys)**: Blockpost ("W, A, S, D or Up arrow, Down arrow, Left arrow, Right arrow to move. M..."); Karate Fighter ("Mouse click on menu buttons. W, A, S, D to move. J, K, L, I to attack...."); Stickman Battle ("Player 1: W, A, S, D to move. Hold W to jump. E for skill. Spacebar fo..."); Magic Battleground ("Use W, A, S, D or the Up arrow, Down arrow, Left arrow, Right arrow to...")

Extra-input count among keyboard-movement games (2024+; dataset):

| Keyboard movement games, 2024+ | n | median votes/day | median RTI | top-quartile count (rate) |
|---|---|---|---|---|
| 0 extra inputs (move only) | 153 | 87.5 | 0.93 | 40 (26% of group in top quartile) |
| 1 extra input | 63 | 109 | 1.03 | 19 (30% of group in top quartile) |
| 2 extra inputs | 44 | 201 | 1.84 | 16 (36% of group in top quartile) |
| 3+ extra inputs (complex) | 37 | 234 | 2.64 | 17 (46% of group in top quartile) |

## 2. Mobile availability and mobile orientation

`mobile` = available on mobile. `mobile_orientation` is one of portrait, landscape or both; it is null when the game is not available on mobile (dataset: 211 null = 211 mobile:false).

| Group | n (2024+) | share of 2024+ | median votes/day | median RTI | in 2024+ top-quartile (n, share) | lift vs supply | in 2024+ top-50 by votes/day | n all-time (share of 1,503) | in all-time top-100 | lift top-100 vs catalogue | on homepage (2024+ games) |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Mobile: both orientations | 473 | 74% | 106 | 1.04 | 122 (76%) | 1.04 | 40 | 735 (49%) | 30 | 0.61 | 94 |
| Mobile: portrait-only | 53 | 8% | 66.1 | 0.82 | 11 (7%) | 0.83 | 5 | 145 (10%) | 7 | 0.73 | 6 |
| Mobile: landscape-only | 93 | 14% | 74.7 | 1.00 | 22 (14%) | 0.95 | 2 | 412 (27%) | 42 | 1.53 | 8 |
| Desktop-only (no mobile) | 24 | 4% | 20.5 | 0.23 | 5 (3%) | 0.84 | 3 | 211 (14%) | 21 | 1.50 | 0 |
| Any mobile (all of the above except desktop-only) | 619 | 96% | 94.9 | 1.00 | 155 (97%) | 1.01 | 47 | 1292 (86%) | 79 | 0.92 | 108 |

Trend by release year (dataset: share of that year's dated releases):

| Release year | n | both | portrait-only | landscape-only | desktop-only |
|---|---|---|---|---|---|
| 2021 | 157 | 20% | 18% | 41% | 20% |
| 2022 | 131 | 20% | 8% | 47% | 26% |
| 2023 | 128 | 37% | 12% | 47% | 5% |
| 2024 | 235 | 60% | 12% | 23% | 6% |
| 2025 | 211 | 76% | 8% | 14% | 3% |
| 2026 | 197 | 88% | 5% | 5% | 3% |

- **Landscape-only on mobile, 2024+ releases: 93 of 643 (14%)**; by year: 2024: 54, 2025: 29, 2026: 10 (dataset).
- Desktop-only 2024+ releases: 24 (dataset).
- Of the 93 landscape-only recent games, 10 are tagged 3D Games and 45 use keyboard movement controls (dataset).
- Best landscape-only 2024+ games by RTI: Stunt Bike Extreme (RTI 36.3, 2285 votes/day); Karate Fighter (RTI 31.7, 1551 votes/day); Cryzen.io (RTI 12.5, 788 votes/day); Ragdoll Hit (RTI 12.2, 697 votes/day); Stickman Archero Fight (RTI 11.4, 653 votes/day); 12 Mini Battles 2 (RTI 10.1, 611 votes/day); Ant Art Tycoon (RTI 7.4, 688 votes/day); Tear Blocks Down (RTI 7.1, 673 votes/day) (dataset).
- Poki guidance on orientation: "Every game submitted to Poki needs to work in portrait, and our QA team tests for it." and "Asking them to rotate their phone is a conversion killer when the next game is one tap away." (https://poki.com/blog/building-web-browser-games-2026). The developer requirements page is softer: "On mobile, cover the full screen in portrait or landscape, or both for the best experience." (https://developers.poki.com/guide/requirements-quality).

Controls class x mobile orientation, 2024+ (n / median RTI; dataset):

| Controls | both | portrait-only | landscape-only | desktop-only |
|---|---|---|---|---|
| One-button / tap / hold-release | 24 / 0.64 | 3 / 0.60 | 3 / 0.58 | 0 |
| Mouse-only / point-click-drag | 224 / 0.99 | 38 / 0.58 | 44 / 1.00 | 7 / 0.05 |
| Keyboard movement (WASD/arrows) + <=2 keys | 199 / 1.04 | 11 / 2.97 | 36 / 1.30 | 14 / 0.31 |
| Complex (many keys / mouse-aim + keys) | 24 / 3.00 | 1 / 0.25 | 9 / 0.90 | 3 / 6.63 |

## 3. Social: 2-player, multiplayer, .io

| Group | n (2024+) | share of 2024+ | median votes/day | median RTI | in 2024+ top-quartile (n, share) | lift vs supply | in 2024+ top-50 by votes/day | n all-time (share of 1,503) | in all-time top-100 | lift top-100 vs catalogue | on homepage (2024+ games) |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 2 Player Games | 36 | 6% | 143 | 1.67 | 15 (9%) | 1.67 | 2 | 136 (9%) | 25 | 2.76 | 10 |
| Multiplayer Games | 61 | 9% | 198 | 2.40 | 27 (17%) | 1.78 | 7 | 152 (10%) | 33 | 3.26 | 24 |
| .io Games | 17 | 3% | 788 | 5.85 | 12 (8%) | 2.84 | 6 | 40 (3%) | 11 | 4.13 | 8 |
| Co-op Games | 8 | 1% | 101 | 0.69 | 2 (1%) | 1.00 | 0 | 32 (2%) | 6 | 2.82 | 1 |
| 1v1 Games | 10 | 2% | 288 | 4.38 | 6 (4%) | 2.41 | 0 | 60 (4%) | 20 | 5.01 | 0 |
| Any social tag (2P / Multiplayer / .io / Co-op / 1v1) | 97 | 15% | 198 | 2.24 | 44 (28%) | 1.82 | 11 | 245 (16%) | 43 | 2.64 | 33 |
| Online multiplayer wording in text ("online", "real players", "other players") | 48 | 7% | 295 | 3.63 | 28 (18%) | 2.34 | 11 | 131 (9%) | 27 | 3.10 | 15 |
| No social tag | 546 | 85% | 80.5 | 0.90 | 116 (72%) | 0.85 | 39 | 1258 (84%) | 57 | 0.68 | 75 |

## 4. 3D vs 2D

"3D" = tagged with the `3D Games` category. Everything else is treated as 2D, which is an approximation because not every 3D game carries the tag (dataset).

| Group | n (2024+) | share of 2024+ | median votes/day | median RTI | in 2024+ top-quartile (n, share) | lift vs supply | in 2024+ top-50 by votes/day | n all-time (share of 1,503) | in all-time top-100 | lift top-100 vs catalogue | on homepage (2024+ games) |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 3D Games | 152 | 24% | 187 | 1.85 | 59 (37%) | 1.56 | 24 | 277 (18%) | 29 | 1.57 | 44 |
| Not tagged 3D | 491 | 76% | 76.6 | 0.87 | 101 (63%) | 0.83 | 26 | 1226 (82%) | 71 | 0.87 | 64 |

3D x controls, 2024+ (n / median RTI; dataset):

|  | One-button / tap / hold-release | Mouse-only / point-click-drag | Keyboard movement (WASD/arrows) + <=2 keys | Complex (many keys / mouse-aim + keys) |
|---|---|---|---|---|
| 3D | 4 / 0.72 | 28 / 2.07 | 104 / 1.72 | 16 / 3.97 |
| not 3D | 26 / 0.60 | 285 / 0.84 | 156 / 0.92 | 21 / 1.66 |

## 5. Structure and theme signals from the text

Text = `intro` + `description`, cut at "Who created" so that the boilerplate list of the developer's other game titles is not matched. Some themes also count as matched when the game carries the corresponding Poki category (shown in brackets). Matching is case-insensitive regex (dataset).

| Group | n (2024+) | share of 2024+ | median votes/day | median RTI | in 2024+ top-quartile (n, share) | lift vs supply | in 2024+ top-50 by votes/day | n all-time (share of 1,503) | in all-time top-100 | lift top-100 vs catalogue | on homepage (2024+ games) |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Level-based (mentions levels/stages) | 156 | 24% | 84.4 | 0.90 | 34 (21%) | 0.88 | 8 | 402 (27%) | 29 | 1.08 | 24 |
| Explicit level count (e.g. "100 levels") | 24 | 4% | 86.0 | 0.94 | 8 (5%) | 1.34 | 1 | 77 (5%) | 11 | 2.15 | 3 |
| Endless / high-score / survive as long as | 74 | 12% | 93.7 | 0.79 | 21 (13%) | 1.14 | 8 | 165 (11%) | 9 | 0.82 | 15 |
| Idle / clicker / incremental | 94 | 15% | 57.2 | 0.77 | 14 (9%) | 0.60 | 4 | 145 (10%) | 6 | 0.62 | 11 |
| Upgrades (mentions upgrade) | 154 | 24% | 76.9 | 0.86 | 36 (22%) | 0.94 | 10 | 304 (20%) | 25 | 1.24 | 18 |
| Merge | 66 | 10% | 26.2 | 0.28 | 5 (3%) | 0.30 | 2 | 114 (8%) | 1 | 0.13 | 7 |
| Story / narrative / chapters | 13 | 2% | 22.9 | 0.40 | 1 (1%) | 0.31 | 0 | 48 (3%) | 3 | 0.94 | 1 |
| Customization / skins / unlockable characters | 98 | 15% | 130 | 1.30 | 30 (19%) | 1.23 | 10 | 190 (13%) | 15 | 1.19 | 23 |
| Ragdoll / physics | 48 | 7% | 140 | 1.29 | 17 (11%) | 1.42 | 5 | 93 (6%) | 6 | 0.97 | 14 |
| Horror / scary | 32 | 5% | 209 | 1.95 | 13 (8%) | 1.63 | 4 | 70 (5%) | 8 | 1.72 | 10 |
| Brainrot / meme | 33 | 5% | 128 | 1.30 | 9 (6%) | 1.10 | 3 | 46 (3%) | 3 | 0.98 | 7 |
| Obby | 17 | 3% | 518 | 4.11 | 10 (6%) | 2.36 | 4 | 36 (2%) | 8 | 3.34 | 8 |
| Parkour / obstacle course | 19 | 3% | 196 | 2.07 | 8 (5%) | 1.69 | 2 | 42 (3%) | 8 | 2.86 | 7 |
| Dress-up / makeover / fashion / decorating | 86 | 13% | 132 | 1.62 | 25 (16%) | 1.17 | 10 | 151 (10%) | 8 | 0.80 | 18 |
| Cleaning / satisfying / ASMR | 71 | 11% | 105 | 0.83 | 16 (10%) | 0.91 | 10 | 143 (10%) | 6 | 0.63 | 19 |
| Sorting / organizing | 21 | 3% | 32.4 | 0.29 | 1 (1%) | 0.19 | 1 | 48 (3%) | 2 | 0.63 | 2 |
| Cozy / relaxing | 55 | 9% | 82.6 | 0.94 | 12 (8%) | 0.88 | 3 | 138 (9%) | 5 | 0.54 | 13 |
| Simulation / simulator | 144 | 22% | 110 | 1.14 | 35 (22%) | 0.98 | 11 | 294 (20%) | 16 | 0.82 | 23 |
| Tycoon / management / business | 87 | 14% | 64.7 | 0.61 | 16 (10%) | 0.74 | 3 | 189 (13%) | 8 | 0.64 | 10 |
| Sports | 60 | 9% | 176 | 1.81 | 23 (14%) | 1.54 | 5 | 218 (15%) | 26 | 1.79 | 11 |
| Cars / driving / racing | 100 | 16% | 159 | 1.83 | 38 (24%) | 1.53 | 13 | 278 (18%) | 34 | 1.84 | 22 |
| Shooting / guns | 135 | 21% | 156 | 1.41 | 49 (31%) | 1.46 | 13 | 299 (20%) | 28 | 1.41 | 31 |
| Animals / pets | 112 | 17% | 56.0 | 0.75 | 22 (14%) | 0.79 | 3 | 272 (18%) | 12 | 0.66 | 14 |
| Stickman | 21 | 3% | 266 | 3.46 | 13 (8%) | 2.49 | 3 | 64 (4%) | 11 | 2.58 | 7 |
| Bosses / waves | 54 | 8% | 64.9 | 0.76 | 13 (8%) | 0.97 | 2 | 109 (7%) | 0 | 0.00 | 10 |
| Collect / unlock (collection loop) | 252 | 39% | 87.9 | 0.91 | 61 (38%) | 0.97 | 16 | 531 (35%) | 31 | 0.88 | 40 |
| Puzzle / brain (primary genre Puzzle or tag Brain Games) | 181 | 28% | 48.5 | 0.51 | 26 (16%) | 0.58 | 8 | 433 (29%) | 15 | 0.52 | 20 |

Rules: **Level-based (mentions levels/stages)** = /\blevels\b|\blevel \d|\bstages?\b|\bnext level\b|\beach level\b/; **Explicit level count (e.g. "100 levels")** = /\b\d[\d,]*\+?\s+(\w+\s+){0,2}(levels|stages|puzzles|missions)\b/; **Endless / high-score / survive as long as** = /\bendless|\binfinite|as far as (you )?can|high ?score|how long can you|beat your (best|record|own)|personal best|never-ending|best score/; **Idle / clicker / incremental** = /\bidle\b|\bclicker\b|incremental|offline (earnings|income|progress)|passive income|earn money while/ or category in ['Clicker Games', 'Idle Games']; **Upgrades (mentions upgrade)** = /\bupgrad/; **Merge** = /\bmerg/ or category in ['Merge Games']; **Story / narrative / chapters** = /\bstory\b|\bstoryline|\bnarrative|\bchapters?\b|\bplot\b|\bepisodes?\b/; **Customization / skins / unlockable characters** = /\bskins?\b|\bcustomi[sz]|\bcosmetic|\bpersonali[sz]|unlock (\w+ ){0,2}(characters|cars|outfits|hats|heroes|vehicles|skins|looks|styles|pets|weapons)/; **Ragdoll / physics** = /ragdoll|physics|wobbl|floppy|jiggl/ or category in ['Ragdoll Games']; **Horror / scary** = /horror|scary|creepy|spooky|terrif|jump ?scare|haunted|nightmare|backrooms/ or category in ['Backrooms Games', 'Horror Games']; **Brainrot / meme** = /brainrot|\bmemes?\b|skibidi|tralalero|tung tung|sahur|\bsigma\b|\brizz|sprunki|\b67\b|bombardiro|cappuccin/ or category in ['Brainrot Games', 'Meme Games']; **Obby** = /\bobby\b|\bobbies\b/ or category in ['Obby Games']; **Parkour / obstacle course** = /parkour|obstacle course/ or category in ['Parkour Games']; **Dress-up / makeover / fashion / decorating** = /dress[- ]?up|makeover|make[- ]?up\b|fashion|\boutfits?\b|decorat|interior design|design your (own )?(room|home|house)|hairstyl|\bnails?\b|\bsalon/ or category in ['Beauty Games', 'Decoration Games', 'Dress Up Games', 'Fashion Games', 'Hair Games', 'Make Up Games']; **Cleaning / satisfying / ASMR** = /\bclean|\bwash|satisf|\basmr|\btidy|\bscrub|\bpolish/; **Sorting / organizing** = /\bsort|\borgani[sz]/; **Cozy / relaxing** = /\bcozy|\bcosy|relax|\bcalm\b|\bchill/ or category in ['Cozy Games']; **Simulation / simulator** = /simulat/ or category in ['Simulation Games']; **Tycoon / management / business** = /tycoon|\bmanag|business|run your own|\bempire\b|\bprofits?\b|\bcustomers?\b/ or category in ['Restaurant Games', 'Tycoon Games']; **Sports** = /soccer|football|basketball|tennis|\bgolf|hockey|baseball|cricket|volleyball|bowling|\bpool\b|billiard|boxing|wrestl|penalty|world cup|\bsports?\b/ or category in ['Basketball Games', 'Football Games', 'Soccer Games', 'Sports Games']; **Cars / driving / racing** = /\bcars?\b|\bdriv|\bracing|\brace\b|\bdrift/ or category in ['Car Games', 'Driving Games', 'Racing Games']; **Shooting / guns** = /\bshoot|\bguns?\b|\bsniper|\bweapons?\b/ or category in ['Gun Games', 'Shooting Games']; **Animals / pets** = /\bpets?\b|\banimals?\b|\bcats?\b|\bdogs?\b|\bpupp|\bkitt/ or category in ['Animal Games', 'Cat Games', 'Dog Games']; **Stickman** = /stickman|stick figure/ or category in ['Stickman Games']; **Bosses / waves** = /\bboss|\bwaves?\b/; **Collect / unlock (collection loop)** = /\bcollect|\bunlock/; **Puzzle / brain (primary genre Puzzle or tag Brain Games)** = category in ['Brain Games', 'Puzzle Games']

### 5a. Themes ranked by lift among 2024+ top-quartile (only themes with n >= 15 in 2024+)

| Theme | n 2024+ | top-quartile n | lift | median RTI | median votes/day |
|---|---|---|---|---|---|
| Stickman | 21 | 13 | 2.49 | 3.46 | 266 |
| Obby | 17 | 10 | 2.36 | 4.11 | 518 |
| Parkour / obstacle course | 19 | 8 | 1.69 | 2.07 | 196 |
| Horror / scary | 32 | 13 | 1.63 | 1.95 | 209 |
| Sports | 60 | 23 | 1.54 | 1.81 | 176 |
| Cars / driving / racing | 100 | 38 | 1.53 | 1.83 | 159 |
| Shooting / guns | 135 | 49 | 1.46 | 1.41 | 156 |
| Ragdoll / physics | 48 | 17 | 1.42 | 1.29 | 140 |
| Explicit level count (e.g. "100 levels") | 24 | 8 | 1.34 | 0.94 | 86.0 |
| Customization / skins / unlockable characters | 98 | 30 | 1.23 | 1.30 | 130 |
| Dress-up / makeover / fashion / decorating | 86 | 25 | 1.17 | 1.62 | 132 |
| Endless / high-score / survive as long as | 74 | 21 | 1.14 | 0.79 | 93.7 |
| Brainrot / meme | 33 | 9 | 1.10 | 1.30 | 128 |
| Simulation / simulator | 144 | 35 | 0.98 | 1.14 | 110 |
| Collect / unlock (collection loop) | 252 | 61 | 0.97 | 0.91 | 87.9 |
| Bosses / waves | 54 | 13 | 0.97 | 0.76 | 64.9 |
| Upgrades (mentions upgrade) | 154 | 36 | 0.94 | 0.86 | 76.9 |
| Cleaning / satisfying / ASMR | 71 | 16 | 0.91 | 0.83 | 105 |
| Cozy / relaxing | 55 | 12 | 0.88 | 0.94 | 82.6 |
| Level-based (mentions levels/stages) | 156 | 34 | 0.88 | 0.90 | 84.4 |
| Animals / pets | 112 | 22 | 0.79 | 0.75 | 56.0 |
| Tycoon / management / business | 87 | 16 | 0.74 | 0.61 | 64.7 |
| Idle / clicker / incremental | 94 | 14 | 0.60 | 0.77 | 57.2 |
| Puzzle / brain (primary genre Puzzle or tag Brain Games) | 181 | 26 | 0.58 | 0.51 | 48.5 |
| Merge | 66 | 5 | 0.30 | 0.28 | 26.2 |
| Sorting / organizing | 21 | 1 | 0.19 | 0.29 | 32.4 |

### 5b. Primary genre (field `genre`), 2024+ games

| Primary genre | n 2024+ | share | median votes/day | median RTI | top-quartile n (lift) | in all-time top-100 |
|---|---|---|---|---|---|---|
| Simulation Games | 99 | 15% | 111 | 1.17 | 24 (0.97) | 7 |
| Puzzle Games | 85 | 13% | 29.1 | 0.36 | 9 (0.43) | 2 |
| Skill Games | 64 | 10% | 81.1 | 0.87 | 17 (1.07) | 14 |
| Brain Games | 44 | 7% | 64.8 | 0.69 | 6 (0.55) | 3 |
| Platform Games | 41 | 6% | 85.3 | 1.10 | 8 (0.78) | 8 |
| Sports Games | 40 | 6% | 184 | 1.91 | 16 (1.61) | 11 |
| Action Games | 35 | 5% | 140 | 0.88 | 12 (1.38) | 10 |
| Shooting Games | 33 | 5% | 252 | 2.85 | 17 (2.07) | 8 |
| Beauty Games | 30 | 5% | 220 | 2.27 | 12 (1.61) | 3 |
| Driving Games | 25 | 4% | 109 | 1.10 | 6 (0.96) | 11 |
| Adventure Games | 25 | 4% | 68.4 | 0.77 | 6 (0.96) | 1 |
| Racing Games | 23 | 4% | 227 | 1.97 | 10 (1.75) | 8 |
| Idle Games | 23 | 4% | 56.0 | 0.62 | 2 (0.35) | 1 |
| Decoration Games | 18 | 3% | 124 | 1.50 | 4 (0.89) | 0 |
| Arcade Games | 16 | 2% | 22.3 | 0.26 | 2 (0.50) | 3 |
| Fighting Games | 10 | 2% | 225 | 1.97 | 4 (1.61) | 3 |
| Strategy Games | 10 | 2% | 75.6 | 1.07 | 1 (0.40) | 1 |
| Escape Games | 9 | 1% | 204 | 2.18 | 4 (1.79) | 1 |

### 5c. Multivariate check (OLS on ln votes/day, 2024+ games, controlling for release quarter)

n = 643, predictors = 31 traits + 10 release-quarter dummies, R^2 = 0.34 (dataset). The multiplier is exp(coefficient): 1.50 means about 50% more votes/day than the baseline with everything else held equal. |t| >= 2 is roughly significant at 5%. This is a rough check on confounding (for example 3D games tending to also be multiplayer), not a causal model.

| Trait | n with trait | votes/day multiplier | 95% CI | t |
|---|---|---|---|---|
| big publisher / external IP flag | 63 | 2.51 | 1.70-3.72 | 4.6 |
| dress-up/makeover/decorating | 86 | 2.06 | 1.46-2.92 | 4.1 |
| .io Games tag | 17 | 3.38 | 1.64-6.97 | 3.3 |
| cars/driving | 100 | 1.56 | 1.13-2.16 | 2.7 |
| 3D Games tag | 152 | 1.35 | 1.01-1.80 | 2.1 |
| controls: complex (vs mouse/point) | 37 | 1.62 | 0.96-2.73 | 1.8 |
| horror/scary | 32 | 1.60 | 0.95-2.68 | 1.8 |
| sports | 60 | 1.42 | 0.96-2.09 | 1.7 |
| brainrot/meme | 33 | 1.47 | 0.90-2.41 | 1.5 |
| 2 Player Games tag | 36 | 1.36 | 0.83-2.22 | 1.2 |
| developer has 5-9 games (vs 2-4) | 151 | 1.20 | 0.89-1.62 | 1.2 |
| Multiplayer Games tag | 61 | 1.30 | 0.84-2.00 | 1.2 |
| ragdoll/physics | 48 | 1.24 | 0.81-1.88 | 1.0 |
| obby | 17 | 1.39 | 0.66-2.91 | 0.9 |
| simulation | 144 | 1.13 | 0.82-1.55 | 0.7 |
| text: endless/high-score | 74 | 1.10 | 0.78-1.55 | 0.5 |
| mobile portrait-only (vs both) | 53 | 1.04 | 0.70-1.57 | 0.2 |
| text: level-based | 156 | 1.02 | 0.78-1.33 | 0.1 |
| customization/skins | 98 | 1.02 | 0.75-1.40 | 0.1 |
| controls: keyboard move + few keys (vs mouse/point) | 260 | 1.01 | 0.76-1.33 | 0.1 |
| controls: one-button (vs mouse/point) | 30 | 0.93 | 0.55-1.57 | -0.3 |
| developer has 1 game on Poki (vs 2-4) | 118 | 0.93 | 0.68-1.28 | -0.4 |
| mobile landscape-only (vs both) | 93 | 0.87 | 0.63-1.21 | -0.8 |
| tycoon/management | 87 | 0.86 | 0.59-1.23 | -0.8 |
| idle/clicker | 94 | 0.83 | 0.59-1.16 | -1.1 |
| cleaning/satisfying | 71 | 0.82 | 0.57-1.17 | -1.1 |
| text: upgrades | 154 | 0.83 | 0.63-1.10 | -1.3 |
| developer has 10+ games (vs 2-4) | 170 | 0.73 | 0.54-0.98 | -2.1 |
| puzzle/brain | 181 | 0.62 | 0.46-0.84 | -3.1 |
| merge | 66 | 0.48 | 0.32-0.71 | -3.7 |
| desktop-only (vs both) | 24 | 0.30 | 0.17-0.55 | -3.9 |

### 5d. Robustness: same traits in the indie-only subset and in games live 90+ days

For each subset the top quartile is recomputed inside that subset. "Indie-only" drops the big-publisher/external-IP list (Inference, see 6c). "90+ days" drops games in their launch window (dataset).

| Trait | all 2024+ (n=643): n / median RTI / lift | indie-only (n=580) | live 90+ days (n=565) |
|---|---|---|---|
| One-button / tap / hold-release | 30 / 0.60 / 1.07 | 27 / 0.58 / 0.89 | 27 / 0.61 / 1.19 |
| Mouse-only / point-click-drag | 313 / 0.91 / 0.76 | 278 / 0.89 / 0.75 | 276 / 0.90 / 0.75 |
| Keyboard movement (WASD/arrows) + <=2 keys | 260 / 1.05 / 1.16 | 236 / 1.00 / 1.15 | 230 / 1.06 / 1.18 |
| Complex (many keys / mouse-aim + keys) | 37 / 2.64 / 1.85 | 36 / 2.45 / 2.00 | 29 / 2.07 / 1.66 |
| Mobile both orientations | 473 / 1.04 / 1.04 | 420 / 1.01 / 1.08 | 398 / 1.04 / 1.04 |
| Mobile portrait-only | 53 / 0.82 / 0.83 | 45 / 0.60 / 0.62 | 52 / 0.81 / 0.85 |
| Mobile landscape-only | 93 / 1.00 / 0.95 | 92 / 1.00 / 0.91 | 91 / 1.00 / 0.97 |
| Desktop-only | 24 / 0.23 / 0.84 | 23 / 0.15 / 0.70 | 24 / 0.23 / 0.83 |
| 3D Games | 152 / 1.85 / 1.56 | 132 / 1.88 / 1.58 | 127 / 1.69 / 1.48 |
| Multiplayer Games | 61 / 2.40 / 1.78 | 59 / 2.24 / 1.90 | 55 / 2.24 / 1.75 |
| 2 Player Games | 36 / 1.67 / 1.67 | 35 / 1.48 / 1.60 | 35 / 1.86 / 1.72 |
| .io Games | 17 / 5.85 / 2.84 | 14 / 4.82 / 2.86 | 14 / 4.82 / 2.58 |
| Merge | 66 / 0.28 / 0.30 | 63 / 0.27 / 0.32 | 57 / 0.25 / 0.35 |
| Idle / clicker / incremental | 94 / 0.77 / 0.60 | 88 / 0.76 / 0.59 | 86 / 0.75 / 0.56 |
| Puzzle / brain (primary genre Puzzle or tag Brain Games) | 181 / 0.51 / 0.58 | 152 / 0.44 / 0.50 | 164 / 0.52 / 0.64 |
| Dress-up / makeover / fashion / decorating | 86 / 1.62 / 1.17 | 80 / 1.55 / 1.15 | 72 / 1.72 / 1.34 |
| Horror / scary | 32 / 1.95 / 1.63 | 19 / 2.26 / 1.89 | 26 / 1.76 / 1.70 |
| Obby | 17 / 4.11 / 2.36 | 16 / 4.98 / 2.50 | 13 / 2.83 / 2.16 |
| Cars / driving / racing | 100 / 1.83 / 1.53 | 93 / 1.77 / 1.46 | 90 / 1.88 / 1.51 |
| Sports | 60 / 1.81 / 1.54 | 58 / 1.65 / 1.66 | 55 / 1.80 / 1.53 |
| Shooting / guns | 135 / 1.41 / 1.46 | 123 / 1.17 / 1.40 | 116 / 1.55 / 1.52 |
| Ragdoll / physics | 48 / 1.29 / 1.42 | 41 / 1.04 / 1.27 | 43 / 1.30 / 1.40 |
| Brainrot / meme | 33 / 1.30 / 1.10 | 30 / 1.24 / 1.33 | 32 / 1.24 / 1.13 |
| Tycoon / management / business | 87 / 0.61 / 0.74 | 81 / 0.59 / 0.74 | 77 / 0.61 / 0.62 |
| Cleaning / satisfying / ASMR | 71 / 0.83 / 0.91 | 62 / 0.79 / 0.97 | 53 / 0.61 / 1.06 |
| Stickman | 21 / 3.46 / 2.49 | 19 / 4.35 / 2.74 | 17 / 4.35 / 2.83 |

## 6. Developer portfolio effects

Credit: a game counts for every developer in its `developers` list, so co-developed titles (for example "Blumgi × Puya") count fully for each partner. Names were normalised by case and punctuation (for example "Code This Lab" = "Codethislab", "Happylander" = "Happylander Ltd"). Portfolio = games live on Poki today (dataset).

- Developers in the dataset: 434. With 3+ games: 165, holding 1173 game-credits and 82% of all votes, where co-credits can double count (dataset).
- Single-game developers: 202 (47% of developers); median votes of their game = 40,374, versus a median of 84,497 per game for developers with 3+ games (dataset).

Traction of 2024+ games by the developer's current Poki portfolio size (dataset):

| Developer portfolio | n 2024+ games | median votes/day | median RTI | top-quartile count (rate) | lift |
|---|---|---|---|---|---|
| 1 game (only this one) | 118 | 78.1 | 0.80 | 23 (19% of group) | 0.78 |
| 2-4 games | 204 | 97.6 | 0.98 | 60 (29% of group) | 1.18 |
| 5-9 games | 151 | 103 | 1.28 | 44 (29% of group) | 1.17 |
| 10+ games | 170 | 98.1 | 0.99 | 33 (19% of group) | 0.78 |

### 6a. Do later games outperform earlier ones? (developers with 3+ dated, non-legacy games)

RTI is used, not raw votes, because RTI controls for launch quarter. Raw lifetime votes favour older games, and raw votes/day favours newer ones (dataset).

- Developers analysed: 147. Median Spearman correlation between release order and RTI = -0.20; 55 of 147 are positive (dataset).
- Later half of the catalogue beats the earlier half on median RTI for 59 of 147 developers (40%); the newest game beats the first game for 64 of 147 (44%) (dataset).

- Robustness, developers whose live catalogue starts in 2023 or later (n = 52): median Spearman = -0.14; later half beats earlier half for 25 of 52 (48%) (dataset).

| Release index within developer | n games | median RTI | share with RTI > 1 |
|---|---|---|---|
| 1st | 147 | 1.49 | 62% |
| 2nd | 147 | 1.16 | 55% |
| 3rd | 147 | 1.66 | 59% |
| 4th-5th | 186 | 1.10 | 52% |
| 6th-10th | 216 | 1.04 | 52% |
| 11th+ | 195 | 0.55 | 31% |

Caveat: the index counts only games still live, so a developer's real first game may have been removed. Games that survive are more likely to be the good ones, and that effect is strongest for the oldest games.

### 6b. Top 25 developers by total votes (all games)

| # | Developer | games | total votes | median votes/game | median votes/day | median RTI | top game (votes) | earliest release yr | 2024+ games | votes from 2024+ games | games on homepage |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Sybo | 3 | 21,415,921 | 16,264 | 50.7 | 0.54 | Subway Surfers (21,396,026) | 2019 | 2 | 19,895 | 1 |
| 2 | Madpuffers | 9 | 16,153,473 | 1,297,887 | 561 | 8.39 | Moto X3M (5,304,251) | 2019 | 0 | 0 | 0 |
| 3 | Madbox | 6 | 11,180,290 | 766,736 | 452 | 5.33 | Stickman Hook (7,894,266) | 2018 | 0 | 0 | 1 |
| 4 | No Pressure Studios | 11 | 9,544,538 | 489,161 | 446 | 5.37 | Rocket Soccer Derby (3,963,308) | 2019 | 3 | 581,878 | 3 |
| 5 | Studio Seufz | 2 | 9,425,847 | 4,712,924 | 1,734 | 15.28 | Murder (9,048,862) | 2019 | 0 | 0 | 1 |
| 6 | Gametornado | 18 | 9,069,345 | 335,272 | 221 | 2.71 | Rio Rex (1,295,206) | 2019 | 4 | 1,512,028 | 1 |
| 7 | PuffballsUnited | 5 | 8,150,791 | 1,006,403 | 398 | 5.48 | Escaping the Prison (3,257,376) | 2019 | 0 | 0 | 0 |
| 8 | Playtouch | 32 | 7,896,567 | 138,666 | 52.8 | 0.90 | TicTacToe (1,503,023) | 2019 | 0 | 0 | 0 |
| 9 | Faramel games | 8 | 7,695,771 | 816,402 | 296 | 2.22 | 3D Moto Simulator 2 (2,167,342) | 2019 | 0 | 0 | 3 |
| 10 | TinyDobbins | 7 | 7,460,283 | 413,615 | 189 | 4.36 | Monkey Mart (3,809,241) | 2020 | 0 | 0 | 0 |
| 11 | Unico Studio | 23 | 6,723,673 | 25,037 | 67.8 | 0.63 | Brain Test: Tricky Puzzles (2,659,211) | 2020 | 14 | 692,774 | 3 |
| 12 | Fancade | 15 | 5,908,829 | 67,924 | 90.5 | 1.13 | Drive Mad (3,869,379) | 2022 | 6 | 626,467 | 2 |
| 13 | Brain Software | 16 | 5,754,723 | 324,378 | 128 | 1.44 | Off-Road Rain Cargo Simulator (1,060,526) | 2019 | 0 | 0 | 0 |
| 14 | Colin Lane Games AB | 9 | 5,583,031 | 254,163 | 110 | 1.00 | Temple of Boom (2,882,921) | 2019 | 0 | 0 | 1 |
| 15 | Codethislab | 28 | 5,034,352 | 43,442 | 18.7 | 0.25 | Master Chess (1,949,441) | 2019 | 0 | 0 | 2 |
| 16 | Go Panda Games Studio | 38 | 5,024,033 | 89,156 | 91.8 | 1.16 | Funny Haircut (580,764) | 2020 | 11 | 124,864 | 0 |
| 17 | 10x10Games | 7 | 4,878,006 | 269,974 | 184 | 1.38 | Penalty Shooters 2 (3,600,851) | 2019 | 4 | 642,635 | 1 |
| 18 | 7Spot Games | 17 | 4,769,762 | 165,138 | 98.0 | 1.28 | Duo Survival (1,450,028) | 2020 | 2 | 31,615 | 0 |
| 19 | Unept | 4 | 4,609,694 | 223,477 | 92.6 | 1.62 | Level Devil (4,142,008) | 2019 | 0 | 0 | 1 |
| 20 | OnRush Studio | 14 | 4,562,066 | 72,257 | 158 | 2.00 | Venge.io (2,319,969) | 2020 | 9 | 1,180,009 | 3 |
| 21 | CyberGoldFinch | 9 | 4,428,872 | 343,748 | 125 | 0.93 | Dragon Simulator 3D (1,419,036) | 2019 | 1 | 38,000 | 0 |
| 22 | Imangi Studios | 6 | 4,227,440 | 352,627 | 190 | 3.15 | Temple Run 2 (2,874,562) | 2020 | 1 | 70,676 | 0 |
| 23 | Blumgi | 13 | 4,120,843 | 225,455 | 246 | 3.02 | Blumgi Slime (1,032,676) | 2021 | 6 | 672,792 | 3 |
| 24 | Radical Play | 7 | 4,006,145 | 208,341 | 762 | 5.30 | Soccer Skills World Cup (1,421,178) | 2021 | 3 | 247,316 | 1 |
| 25 | WeLoPlay | 18 | 3,866,043 | 125,894 | 266 | 2.65 | Nails DIY: Manicure Master (708,804) | 2023 | 14 | 3,023,662 | 3 |

Reference rows (explicit comparison):

| # | Developer | games | total votes | median votes/game | median votes/day | median RTI | top game (votes) | earliest release yr | 2024+ games | votes from 2024+ games | games on homepage |
|---|---|---|---|---|---|---|---|---|---|---|---|
| ref | AJ Ordaz | 8 | 218,296 | 15,578 | 35.7 | 0.44 | A Pretty Odd Bunny (71,210) | 2022 | 7 | 147,086 | 1 |
| ref | Blumgi | 13 | 4,120,843 | 225,455 | 246 | 3.02 | Blumgi Slime (1,032,676) | 2021 | 6 | 672,792 | 3 |

- **Blumgi** game-by-game (release date, votes, votes/day, RTI, controls class, mobile orientation): Blumgi Rocket (2021-11-05, 910,865, 509/day, RTI 6.73, kb_move_fewkeys, landscape); Blumgi Ball (2022-02-23, 412,425, 246/day, RTI 7.23, mouse_point_drag, landscape); Blumgi Castle (2022-08-18, 425,863, 283/day, RTI 3.02, complex, landscape); Swingo (2022-12-05, 316,292, 227/day, RTI 4.60, mouse_point_drag, landscape); Blumgi Slime (2023-02-16, 1,032,676, 782/day, RTI 9.74, one_button, portrait); Blumgi Bloom (2023-08-03, 120,798, 105/day, RTI 1.27, mouse_point_drag, landscape); Blumgi Dragon (2023-12-04, 229,132, 222/day, RTI 2.10, one_button, portrait); Blumgi Soccer (2024-03-25, 225,455, 246/day, RTI 4.04, mouse_point_drag, portrait); Blumgi Racers (2024-08-30, 84,708, 111/day, RTI 1.77, kb_move_fewkeys, both); Blumgi Paintball (2024-10-17, 103,722, 146/day, RTI 2.97, kb_move_fewkeys, portrait); Blumgi Merge (2025-04-14, 163,161, 306/day, RTI 3.04, mouse_point_drag, both); Blumgi Bounce (2025-12-02, 84,748, 282/day, RTI 2.98, one_button, both); Blumgi Splash (2026-05-22, 10,998, 85/day, RTI 0.48, mouse_point_drag, both) (dataset).
- **AJ Ordaz** game-by-game (release date, votes, votes/day, RTI, controls class, mobile orientation): A Pretty Odd Bunny (2022-10-17, 71,210, 49/day, RTI 1.00, kb_move_fewkeys, landscape); A Pretty Odd Bunny: Roast it! (2024-05-08, 65,288, 75/day, RTI 1.30, kb_move_fewkeys, landscape); Lidle Legend (2024-10-09, 13,032, 18/day, RTI 0.37, kb_move_fewkeys, both); Ranch UFO (2025-05-21, 12,049, 24/day, RTI 0.24, kb_move_fewkeys, both); Nekopirate: Quest for Gold! (2025-06-24, 8,110, 18/day, RTI 0.17, kb_move_fewkeys, both); A Cleaning Story (2025-09-09, 18,123, 47/day, RTI 0.51, mouse_point_drag, both); Veggie Merge (2026-06-05, 1,599, 14/day, RTI 0.08, mouse_point_drag, both); Trapped in the Dollhouse (2026-07-09, 28,885, 352/day, RTI 2.05, mouse_point_drag, both) (dataset).

- Rank by total votes: Blumgi #23, AJ Ordaz #191 of 434 developers (dataset).

### 6c. Top 15 small/indie developers by votes from 2024+ releases

Small/indie = 5 or fewer games on Poki in total, and not on the big-publisher/external-IP list (Inference: list compiled by the analyst from developer names and description wording: Voodoo = hyper-casual mobile publisher (Hole.io, Paper.io 2); Outfit7 = Talking Tom mobile IP owner; ZnK Games = Scary Teacher mobile IP; Lion Studios = mobile publisher; Fingersoft = Hill Climb Racing mobile IP ("HTML5 version of the classic game"); SayGames = mobile publisher; StoreRider = ports of established mobile IP (Kick the Buddy, Tank Stars); Gametion Global = Ludo King mobile IP ("the official, smash-hit Ludo game"); Yes2Games = Dan The Man mobile IP port; Sybo = Subway Surfers IP owner; Unico Studio = mobile-first studio (Poki blog: "Beyond the app stores"); BoneCracker Games = Drift Hunters, long-established web hit newly dated (Inference)).

| # | Developer | games total | 2024+ games | votes from 2024+ games | best 2024+ game | note |
|---|---|---|---|---|---|---|
| 1 | Skullcap Studios | 5 | 4 | 2,311,692 | Blockpost (2025-07-17, 1,853,339 votes, 4222/day, complex, mobile n/a (desktop-only)) |  |
| 2 | Hyperkani | 4 | 3 | 2,120,527 | Stunt Bike Extreme (2024-08-19, 1,761,913 votes, 2285/day, kb_move_fewkeys, mobile landscape) | Inference: port of an existing mobile game |
| 3 | Hipster Whale | 1 | 1 | 1,956,143 | Crossy Road (2024-12-02, 1,956,143 votes, 2937/day, kb_move_fewkeys, mobile n/a (desktop-only)) | Inference: pre-existing mobile hit (2014), not a new web-first design |
| 4 | Vectaria | 4 | 3 | 1,865,628 | MineFun.io (2024-09-30, 1,222,423 votes, 1677/day, kb_move_fewkeys, mobile both) |  |
| 5 | Jungle Tavern | 4 | 4 | 1,735,703 | Count Control Legends (2025-11-10, 755,115 votes, 2338/day, kb_move_fewkeys, mobile portrait) |  |
| 6 | ChennaiGames | 1 | 1 | 1,369,190 | MR RACER - Car Racing (2024-04-10, 1,369,190 votes, 1518/day, kb_move_fewkeys, mobile both) | Inference: port of an existing mobile game |
| 7 | Devortel | 4 | 2 | 1,271,050 | Vortella's Dress Up (2024-12-13, 1,239,199 votes, 1892/day, kb_move_fewkeys, mobile both) |  |
| 8 | PlayCap | 4 | 3 | 1,051,235 | SnapStyle Dress Up (2025-06-10, 951,542 votes, 1999/day, mouse_point_drag, mobile both) |  |
| 9 | OPlay Games | 2 | 2 | 989,475 | Blocky Blast Puzzle (2024-04-02, 749,961 votes, 824/day, mouse_point_drag, mobile portrait) |  |
| 10 | PlayCalm | 1 | 1 | 791,813 | Slice Master (2025-12-01, 791,813 votes, 2622/day, one_button, mobile both) |  |
| 11 | Ericetto | 2 | 2 | 791,750 | Ragdoll Hit (2024-05-16, 603,752 votes, 697/day, kb_move_fewkeys, mobile landscape) |  |
| 12 | d954mas | 4 | 2 | 598,967 | Punch Legend Simulator (2024-06-21, 565,975 votes, 682/day, kb_move_fewkeys, mobile both) |  |
| 13 | Shared Dreams Studio | 4 | 1 | 593,567 | 12 Mini Battles 2 (2024-01-31, 593,567 votes, 611/day, one_button, mobile landscape) |  |
| 14 | TapMen | 1 | 1 | 562,775 | Merge Rot (2025-05-28, 562,775 votes, 1151/day, mouse_point_drag, mobile both) | dataset text: "Originally released under the name Merge Fellas" |
| 15 | Joseph Cloutier | 1 | 1 | 538,704 | Run 3 (2024-12-06, 538,704 votes, 814/day, kb_move_fewkeys, mobile n/a (desktop-only)) | Inference: Flash-era web classic, newly dated on Poki |

## 7. Top 30 recent (2025-2026) indie/web-first performers

Ranking: votes/day, among games released 2025-01-01 or later that have been live at least 14 days (launch-week counts are noisy). Excluded: games from the big-publisher/external-IP list in 6c (Inference), shown after the table. The "core mechanic" is the first sentence of the dataset description; controls are the dataset controls text, trimmed (dataset).

| # | Game | Developer | dev games | released | votes | votes/day | RTI | homepage pos | controls class | mobile orient. | social/3D tags | core mechanic (dataset description, 1st sentence) | controls (dataset) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Blockpost | Skullcap Studios | 5 | 2025-07-17 | 1,853,339 | 4222 | 45.6 | - | complex | desktop-only | Multiplayer, 3D | Blockpost is a 3D first person shooting game created by Skullcap Studios. | W, A, S, D or Up arrow, Down arrow, Left arrow, Right arrow to move. Mouse click to shoot. Right mouse click t... |
| 2 | Hide and Paint | OnRush Studio | 14 | 2026-07-07 | 249,934 | 2975 | 17.3 | 61 | kb_move_fewkeys | both | Multiplayer, 3D, .io | Hide and Paint is a multiplayer game that takes hide and seek to a whole new level. | Use WASD or the Arrow Keys to move. Move the mouse to look around and press F to paint yourself. On mobile, us... |
| 3 | Slice Master | PlayCalm | 1 | 2025-12-01 | 791,813 | 2622 | 27.8 | 5 | one_button | both | - | Slice Master is a skill game where you click to control a knife as it flies through the air. | Mouse click to launch the knife. Tap to launch the knife. |
| 4 | Neon Challenge Legends | Jungle Tavern | 4 | 2026-02-06 | 598,541 | 2547 | 19.4 | 25 | one_button | both | - | Neon Challenge Legends is a skill game where you dash through glowing maze-like tracks. | Hold W, Up arrow, Spacebar, or Mouse click to move up. Release to move down. R to restart. |
| 5 | Count Control Legends | Jungle Tavern | 4 | 2025-11-10 | 755,115 | 2338 | 24.7 | 7 | kb_move_fewkeys | portrait | 3D | Count Control Legends is a skill game where you lead an army of stickmen through levels that will test your math skills. | Swipe or drag left/right to move. Use A, D, Left arrow, or Right arrow to move. |
| 6 | Soccer REAL | splax.net | 4 | 2026-07-08 | 184,076 | 2218 | 12.9 | 67 | mouse_point_drag | both | 3D | Soccer REAL is a sports game where you take full control of an exciting online soccer match from kickoff to final whistle. | Click and hold to aim, release to shoot. |
| 7 | SnapStyle Dress Up | PlayCap | 4 | 2025-06-10 | 951,542 | 1999 | 19.9 | 27 | mouse_point_drag | both | - | Snapstyle Dress Up is a dress up game where you can choose cute outfits for your character. | Click or Tap to make a choice. |
| 8 | Phone CASE DIY | WeLoPlay | 18 | 2026-06-12 | 187,128 | 1717 | 9.7 | 69 | mouse_point_drag | both | 3D | Phone CASE DIY is a decoration game about customizing mobile covers with creative styles. | Click or tap to choose an item. |
| 9 | Backrooms Recovery | Sleepless Games | 4 | 2026-08-27 | 55,914 | 1694 | 9.8 | 83 | kb_move_fewkeys | both | 3D | backrooms Recovery is an adventure game set in the eerie, yellow corridors of a strange facility. | Click or tap to make the choice. Use WASD or the joystick to move. |
| 10 | Plonky | Gametornado | 18 | 2025-07-01 | 766,030 | 1684 | 18.2 | 41 | kb_move_fewkeys | both | - | Plonky is a platform game filled with dangerous traps. | A/D or Left/Right arrow keys to move. W, Up arrow, or Spacebar to jump. S or Down arrow to climb down. |
| 11 | World Soccer Champions | Finz Games | 7 | 2025-04-23 | 807,203 | 1540 | 15.3 | - | mouse_point_drag | both | - | Indoor Soccer is a soccer game where you try to score penalties. | Use the mouse to aim. Swipe and release to shoot. |
| 12 | Rail in the Air | OPlay Games | 2 | 2026-04-21 | 239,514 | 1488 | 8.4 | 77 | kb_move_fewkeys | both | 3D | Rail in the Air is a driving game that puts you in the train conductor seat high up in the sky. | Move: W or the up arrow key; Brake: S or the down arrow key; Cart: C; Maps: M; Exit: Esc; Respawn: R. |
| 13 | Planet Destruction | Boop Games | 3 | 2025-12-31 | 400,699 | 1473 | 15.6 | 13 | mouse_point_drag | both | 3D | Planet Destruction is a simulation game where you blow up planets using weapons like giant lasers, rockets, space ships and even alien monsters. | Mouse click or tap to play. |
| 14 | Slime Keyboard Escape | Blasters | 3 | 2026-08-12 | 69,849 | 1455 | 8.5 | 60 | complex | both | Multiplayer, 3D | Slime Keyboard Race is a simulation game where every step you take builds your speed across a wild world made entirely of keyboard keys. | Move: WASD or the arrow keys Camera: Use your mouse to change the camera angle Jump: the space bar Restart: R ... |
| 15 | Magic Battleground | vessel | 1 | 2026-03-18 | 267,497 | 1372 | 10.4 | 48 | complex | both | - | Magic Battleground is a fighting game that controls a ragdoll warrior in mystical arenas. | Use W, A, S, D or the Up arrow, Down arrow, Left arrow, Right arrow to move. Use X, Y, Z, Mouse click, or Righ... |
| 16 | Beauty Salon | WeLoPlay | 18 | 2025-08-01 | 572,095 | 1349 | 14.6 | 6 | mouse_point_drag | both | - | Beauty Salon is a dress up game where you give a poor girl a glow up by washing her hair, giving her a facial and applying a wonderful selection of makeup and beauty products. | Mouse click or Tap to make a choice. Mouse click and hold to apply actions. |
| 17 | Fashion Legends | Jungle Tavern | 4 | 2026-02-27 | 275,409 | 1287 | 9.8 | - | kb_move_fewkeys | portrait | 3D | Fashion Legends is a stylish beauty game where you showcase your runway flair. | Drag left/right to move. Use A, D or Left arrow, Right arrow to move. |
| 18 | Stickman Battle | EasyCats | 7 | 2025-11-24 | 397,584 | 1287 | 13.6 | 58 | complex | both | 2 Player | Stickman Battle is a fighting game where you can play solo, against a friend or fight other online players to climb the leaderboard. | Player 1: W, A, S, D to move. Hold W to jump. E for skill. Spacebar for super. Player 2: Up arrow, Down arrow,... |
| 19 | Sprunki | NyankoBfLol | 1 | 2026-03-20 | 232,149 | 1203 | 9.2 | - | mouse_point_drag | both | - | Sprunki is a music game that lets you create your own songs by combining different types of instruments and vocals. | Drag and drop musical icons from the bottom of the screen onto the gray character avatars to build your own cu... |
| 20 | Merge Rot | TapMen | 1 | 2025-05-28 | 562,775 | 1151 | 11.4 | - | mouse_point_drag | both | - | Merge matching brainrot characters together to unlock new and stranger ones. | Move your item with the mouse. Click to drop it. |
| 21 | Car Circle | Shoom Games | 4 | 2026-06-19 | 114,077 | 1118 | 6.3 | 9 | mouse_point_drag | both | - | Car Circle is a skill game that requires careful timing as you merge vehicles onto a busy roundabout. | Click or tap to play. |
| 22 | Super Dress | WeLoPlay | 18 | 2026-08-26 | 37,792 | 1112 | 6.5 | 11 | mouse_point_drag | both | - | Super Dress is a fashion game where you style stunning characters from head to toe with complete creative freedom. | Click or tap to make the choice. |
| 23 | Robo Cleaner Simulator | Camu | 7 | 2026-09-02 | 29,845 | 1105 | 6.4 | 2 | kb_move_fewkeys | both | 3D | Robo Cleaner Simulator is a simulation game where you take control of a robot vacuum and get to work on a messy living room. | Click or tap to make the choice. Use WASD, the arrow keys or the joystick to move. |
| 24 | Speed Stars | Luke | 1 | 2026-02-06 | 233,781 | 995 | 7.6 | 28 | kb_move_fewkeys | both | - | Speed Stars is a running game where you race real players in the 100m dash. | Use A and D or the Left and Right arrow keys to run. |
| 25 | Perfect Shape | Sunday Monday | 2 | 2026-08-20 | 38,379 | 959 | 5.6 | - | mouse_point_drag | both | 3D | Perfect Shape is a skill game about tracing outlines with high precision. | Click or tap or use keyboards to make the choice. |
| 26 | Ragdoll Chaos | OSA Studio | 7 | 2026-09-01 | 26,167 | 935 | 5.4 | 94 | mouse_point_drag | both | 3D | Ragdoll Chaos is an action game about turning lab experiments into pure physics havoc. | Click and hold to drag the ragdoll around. |
| 27 | Soccer Skills 2 World Cup | Radical Play | 7 | 2026-04-20 | 151,198 | 933 | 5.3 | 71 | mouse_point_drag | both | Multiplayer, 3D | Soccer Skills 2 World Cup is an immersive sports game that delivers an authentic 3D football tournament experience. | Click and hold to aim, release to shoot. |
| 28 | Soccer League | OnRush Studio | 14 | 2026-07-16 | 69,327 | 924 | 5.4 | - | complex | both | - | Soccer League is an action-packed sports game that brings 3v3 football matches to your screen. | W, A, S, D or Up arrow, Down arrow, Left arrow, Right arrow to move. Use the mouse to adjust the camera. Hold ... |
| 29 | Monkey Tag IO | Petit Kyanpu | 3 | 2026-06-03 | 101,515 | 860 | 4.9 | 97 | kb_move_fewkeys | both | Multiplayer, 3D, .io | Monkey Tag IO is a multiplayer simulation game about swinging through blocky arenas. | Use WASD or joystick to move, use the mouse to adjust the camera angle. |
| 30 | Magikmon | Ravalmatic | 13 | 2026-01-12 | 214,075 | 823 | 6.3 | - | mouse_point_drag | both | - | Magikmon is an adventure game about a student in a magical school. | Mouse click to move. |

Excluded as big publisher/external IP (Inference), which would otherwise have ranked in this range: Hole.io (Voodoo, 6056/day); Talking Tom Gold Run (Outfit7, 3997/day); Kick The Buddy (StoreRider, 2604/day); Scary Teacher 3D (ZnK Games, 2369/day); Tank Stars (StoreRider, 1689/day); Paper.io 2 (Voodoo, 1488/day); Steal a Brainrot (emolingo games, 1203/day); Drift Hunters (BoneCracker Games, 1168/day); Decor Life (SayGames, 1131/day); Hill Climb Racing Lite (Fingersoft, 1088/day); Happy Glass (Lion Studios, 988/day).

Top-30 profile (dataset): controls {'complex': 5, 'kb_move_fewkeys': 9, 'one_button': 2, 'mouse_point_drag': 14}; mobile orientation {'desktop-only': 1, 'both': 27, 'portrait': 2}; 3D-tagged 15; Multiplayer-tagged 5; 2-Player-tagged 1; on today's homepage 22; developer has 1 game 5, 2-4 games 12, 5+ games 13.

