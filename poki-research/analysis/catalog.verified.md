# Fact-check of `analysis/catalog.md` (Catalogue supply/demand & trends)

Checked 2026-09-29 by an independent analyst. I did not reuse the original code. Every dataset number here was recomputed by `analysis/verify_catalog.py`, a new script, plus short inline checks. Definitions are the same as the report's so the results can be compared. votes = up + down (thumbs votes; **votes are not plays**). votes/day = votes / max(days since release_date, 7), measured to 2026-09-29T00:00Z. "Recent" = release_date ≥ 2025-01-01 (n = 408). 2019-03-11 is treated as "≤2019". The 32 null-date games are excluded from votes/day. "Clean" drops the same big-brand developer list, the 12 ⚑ games and the Nitrome/Flipline re-releases. Source quotes were re-read in `sources/*.txt`.

**Overall verdict.** The arithmetic in catalog.md is almost entirely correct. All 26 numeric checks below reproduced exactly or to rounding. The problems are in interpretation:
- **One factual error:** the report says the rating "appears smoothed". In fact rating is an exact linear function of the thumbs-up share.
- **One unsupported headline:** "82% of top performers are indie".
- **Overclaimed robustness** for four "robust ✔" categories (Crazy, Soccer, Obby, Running).
- **One trend mislabel:** Simulation is not rising in hit rate.
- **Omissions:** Poki's portrait guidance, the World Cup timing of the soccer releases, how few studios the tag signals rest on, soft-launch votes counted before release_date, and votes-per-play varying more than 10× between games.

---

## (a) Checked claims

| # | Claim in catalog.md | Independent check | Verdict |
|---|---|---|---|
| 1 | Recent cohort n = 408; votes/day median 127.5, p75 352.1, p90 874.1 | dataset: same definition → 408; 127.5 / 352.1 / 874.1 | CONFIRMED |
| 2 | 32 null release_date; 95 on the 2019-03-11 migration date | dataset: 32 and 95. Everything ≤2019 including migration = 243 | CONFIRMED |
| 3 | Releases live today by year: 2023 128, 2024 235, 2025 211, 2026 197 (to Sep 28); quarterly table; 2026 annualised pace ≈ 265 | dataset: every year and quarter count matches. Latest release 2026-09-28T15:20Z. 197 × 365/271 = 265 | CONFIRMED. One wording fix: "2026 Q3 the busiest on record in this window" holds only within 2025–26. 2024 Q4 had **88** releases, more than 2026 Q3's 79. These counts cover surviving games only |
| 4 | Poki: "227 new game releases" in 2025 | https://poki.com/blog/2025-at-poki-a-year-in-review: "This year, we saw 227 new game releases and played host to talented developers from 89 countries" | CONFIRMED (verbatim) |
| 5 | Launch push "significant push for around 2 weeks"; age-band medians 336.9 (0–30d, n=25) / 151.1 / 165.8 / 108.8 / 98.8; Spearman(days, votes/day) = −0.24 | https://developers.poki.com/guide/release-process: "As a new game, it will also get a significant push for around 2 weeks". dataset: same bands and n; Spearman −0.243 | CONFIRMED |
| 6 | Soft-release games appear "only" on "relevant category pages"; "We're not promoting the game on our homepage" | Same doc: "your game will be released on relevant category pages … there's also a chance that your game gets promoted in additional categories … We're not promoting the game on our homepage or localized homepages during this phase." dataset: none of the 32 null-date games is in today's 145 homepage slots | CONFIRMED with nuance. "Only" overstates it, because the doc allows promotion into additional categories |
| 7 | 12 recent games flagged ⚑ (id much older than release_date) | Different method: median release date of the 15 nearest ids by absolute distance, gap > 365 d. Gives the **same 12 slugs** (blockpost, paperio-2, sprunki, drift-hunters, hill-climb-racing-lite, speed-stars, magikmon, ant-art-tycoon, blockpost-legacy, kates-cooking-party, lips-diy-master, dummies-fight) | CONFIRMED |
| 8 | Primary-genre recent medians: Shooting 357.1 (n=20), Sports 274.3 (21), Beauty 221.2 (24), Racing 198.4 (15), Puzzle 33.1 (45), Arcade 29.9 (8). Clean: Shooting 193.6, Sports 325.4, Beauty 228.7, Racing 157.0 | dataset: all identical | CONFIRMED |
| 9 | "Sports and Beauty/dress-up are the genre-level bets whose strength does not depend on brands" | dataset: true for brands. But Beauty leans on one studio: WeLoPlay has 6 of 24 recent Beauty-genre games and 3 of the 5 Beauty games in the recent top 50. Beauty without WeLoPlay: median 201.3 (n=18). Sports without soccer-tagged games: 251.6 (n=11). Beauty in games ≥90 days old: 185.6 (n=20) | CONFIRMED, but it is weaker than the report implies (≈1.5–2× baseline, not 2–2.5×) |
| 10 | Category leaders: .io 860.3 (n=9), Crazy 779.3 (10), Running 744.0 (11), Soccer 472.0 (11), Parkour 437.4 (5) | dataset: identical | CONFIRMED (numbers). Note that n is 5–11 |
| 11 | Crazy Games is "Robust ✔" (clean 779, 5 devs) | dataset: 8 of the 10 recent Crazy games come from 3 studios: OnRush 3, Jungle Tavern 3, emolingo 2. Dropping Jungle Tavern alone gives a median of **270.8** (n=7). Games ≥90 days old: 407.8 (n=9) | CORRECTED. This is a signal about a few studios, not a genre. It should not carry ✔ |
| 12 | Soccer is "Robust ✔", clean median 818.8 (n=9) | dataset: 818.8 reproduces, but only because 2 Lion Studios games are removed. Dropping Radical Play gives **376.5**. Games ≥90 days old: **283.5** (n=8). **7 of 11** recent soccer releases came out between Apr and Jul 2026. 3 of them are also tagged "World Cup Games". 3 more soccer games are in soft launch now (pro-referee-simulator, no-fault-cup-2026, sling-star-kick). Inference: the 2026 FIFA World Cup (Jun–Jul 2026, general knowledge, not in the sources) lifted this cohort | CORRECTED. The real signal is about 280–380/day (≈2–3× baseline) and is partly seasonal |
| 13 | Obby is "Robust ✔" (clean 427.8); homepage Obby lift 5.6× (8/60) | dataset: Obby games ≥90 days old have a median of **128.4** (n=7), about the baseline. Only 2 of the 8 Obby-tagged games in the homepage top 60 are 2025–26 releases (obby-roads, slime-keyboard-escape). The other 6 are older hits that carry the tag: drive-mad, level-devil, subway-surfers, tunnel-rush, rainbow-obby, minefun-io | CORRECTED. The lead comes from launch-boosted new games and tag breadth |
| 14 | Running Games is "Robust ✔" | dataset: raw 744 → clean **266.1** (n=9) once Talking Tom Gold Run (Outfit7) and ⚑ Speed Stars are removed. Jungle Tavern has 2 of 11 | CORRECTED. It is a moderate signal (≈2× clean baseline), not a 5.8× one |
| 15 | Saturated/weak: Merge 27.2 (n=41), Matching 25.2 (25), Puzzle category 57.3 (85), Idle 80.1 (57), Brain 66.1 (75) | dataset: identical. They stay low after cleaning, after dropping the top developer, and when restricted to games ≥90 days old (Merge 23.6, Puzzle 52.1) | CONFIRMED. Caveat about votes-per-play: see omission O6 |
| 16 | Top-50 recent threshold 759.2 votes/day; top-50 all-time threshold 1,421,178 votes; all-time top 50 has 24 games from ≤2019 | dataset: 759.2; 1,421,178; ≤2019 (including migration) = 24, 2020 = 8, 2021 = 6, 2022 = 4, 2023 = 4, 2024 = 3, 2025 = 1 | CONFIRMED |
| 17 | Trend shifts: 3D 16→24, Dress Up 0→5, Fashion 0→4, Ragdoll 1→4, Difficult 21→2, 1v1 13→0, 2 Player 15→3, Games for Boys 32→14; **Simulation "Rising" 5→11** | dataset: every count matches. But Simulation is 22.8% of recent releases and 22% (11/50) of the recent top 50, which is **0.97×**. As a primary genre it is 0.92× | CORRECTED for Simulation. Its supply is rising; its hit rate is not. The 3D, Dress-up/Fashion and Ragdoll rises are real over-representation (1.5–2.3×) |
| 18 | 11 of the top 60 recent are big-brand ports; 4 of the top 10 and 7 of the top 20; median 1,582 (big) vs 1,105 (others); across all recent games, 47 big at median 181.0 vs 118.8 for 361 others | dataset: identical. Big brands hold 16 of the 102 top-quartile recent games (16%) while being 11.5% of releases | CONFIRMED |
| 19 | "49/60 (82%) of the top-60 recent performers are web-first/indie" | catalog.md §4 table: 35 of the 49 "indie" labels have "medium" confidence, which the report defines as "no positive evidence either way … defaults to indie". Only 14 have positive evidence, and 5 of those 14 are ⚑ re-releases of old browser games (Blockpost, Sprunki, Drift Hunters, Magikmon, Ant Art Tycoon) | UNSUPPORTED as stated. What the data supports: 11/60 are known big-brand ports, 14 are evidenced web-first, and 35 are unverified |
| 20 | Homepage: 30/60 top slots and 86/145 slots are 2025–26 releases (8/12 of the first 12); Spearman(position, votes/day) = −0.53 over the 86 recent homepage games | dataset: 30, 86, 8, −0.526 | CONFIRMED. The reading "the homepage is the demand signal" needs a caveat: the homepage slot also *produces* votes, so causation runs both ways |
| 21 | Homepage genre: Skill 14/60 (lift 1.95×), Puzzle genre 2/60 (0.28×); Difficult 17/60 "mostly older evergreen hits" | dataset: 14, 2. Difficult: 16 of 17 are pre-2025 | CONFIRMED |
| 22 | Spearman(rating, votes/day) = 0.27 over recent games; 54/60 of the top 60 rate ≥ 4.2; recent games rated < 4.2 have median ≤ 65 votes/day | dataset: 0.271; 54; pooled median for < 4.2 = 65.1 (n=105; the 4.0–4.2 band alone is 65.5) | CONFIRMED (rounding) |
| 23 | "`rating` is not simply 5×up/(up+down) … it appears smoothed" | dataset: **rating = 1 + 4 × up/(up+down)** for all 1,503 games. Largest deviation is 0.005 (rounding); Pearson(rating, up-share) = 1.000. Example: jetpack-speed-obby 1 + 4 × 1192/1414 = 4.372, shown as 4.37 | CORRECTED. Rating is not smoothed; it is the thumbs-up share rescaled to 1–5. Rating 4.2 = 80% thumbs-up, 4.4 = 85%, 4.6 = 90%. The top-60 minimum of 3.71 = 68% |
| 24 | Debut flag ("This is their first game on Poki"): n = 96, median 119.7 vs 312 at 128.6; top-quartile share 23% vs 26%; 9 of the top 60. Side note: "144 flagged games have non-empty developer_games; 54 unflagged have empty" | dataset: 96 / 119.7 / 312 / 128.6 / 23% / 26% / 9. The side-note counts are **142** and **59** | CONFIRMED (main result); CORRECTED (side counts, no effect on the conclusion) |
| 25 | Median votes/day by how many games the developer has on Poki: 1 game 108.5 (n=67); 2–3 games 135.7 (90); 4–9 games 154.8 (152); 10+ games 107.6 (99) | dataset: identical | CONFIRMED |
| 26 | Platform: mobile + desktop 397/408 (median 128.4); desktop-only 11 (12.2), of which 8 are Nitrome/Flipline; orientation both 333 (128.4) / landscape 39 (153.7) / portrait 25 (98.9); 3D 196.0 vs 100.6 | dataset: identical. The 3D gap **holds in every age band**: 0–30 d 829 vs 215; 30–90 d 376 vs 140; 90–180 d 363 vs 132; 180–365 d 135 vs 85; 365+ d 171 vs 88 | CONFIRMED |
| 27 | Brand evidence quotes: Outfit7 "has amassed over 3.2 billion downloads"; StoreRider CEO "Porting a Unity game to web takes 1-to-2 hours"; Hill Climb Racing among "iconic hits"; SnapStyle Dress Up and Plonky "top performing" in 2025 | https://poki.com/blog/outfit7-hit-talking-tom-live-on-poki; https://poki.com/blog/state-of-web-gaming-report-2026 ("Xavier Liard, CEO, StoreRider"); https://poki.com/blog/2025-at-poki-a-year-in-review ("Our top performing games were Plonky by Gametornado and SnapStyle Dress Up by PlayCap") | CONFIRMED (verbatim) |
| 28 | Simulation winners follow the loop "control a character in a little world" (shown in quote marks, no citation) | https://poki.com/blog/i-quit-my-job-to-make-a-dress-up-web-game-and-it-blew-up: "players wanted to control a character that runs around in a little world" | CORRECTED. The report put a paraphrase in quote marks without a source. The verbatim wording and URL are above |
| 29 | 84% of recent "Popular Games"-tagged games are in the recent top quartile, so the tag is circular | dataset: 62 games, 84% | CONFIRMED |

---

## (b) Important omissions (with evidence)

**O1. Rating is just the thumbs-up ratio (see #23).** A pitch team can use a hard, interpretable target. 54 of the recent top 60 have ≥ 80% thumbs-up (rating ≥ 4.2). Recent games below 80% have a median of 65.1 votes/day (n=105), about half the cohort median. [dataset: rating vs 1 + 4 × up/(up+down), max deviation 0.005]

**O2. Poki explicitly advises supporting portrait; the report's orientation table invites the wrong reading.** Source: https://developers.poki.com/guide/easy-access says "we strongly advise supporting portrait: portrait-playable games see more players enter gameplay on average, and become eligible for Gamebar Display ads". In the dataset, **55 of the recent top 60** support portrait (51 'both' + 4 portrait-only), 3 are landscape-only and 2 are desktop-only. Of the homepage top 60, 48 are 'both' and 7 portrait-only. The landscape-only median of 153.7 (n=39) is a small-n group median. It is not a reason to ship landscape-only. [dataset: mobile_orientation]

**O3. Soccer demand is partly seasonal, and more supply is coming.** 7 of 11 recent soccer releases came out between Apr and Jul 2026. Three are also tagged "World Cup Games" (soccer-real, a-small-world-cup-2, soccer-skills-2-world-cup). Three soccer games are in soft launch today (pro-referee-simulator, no-fault-cup-2026, sling-star-kick). Soccer games ≥90 days old have a median of 283.5 votes/day (n=8). [dataset] Inference: the Jun–Jul 2026 World Cup boosted this cohort, so a new soccer title releasing in 2027 should not expect 800+/day.

**O4. The top of the chart is concentrated in a few repeat studios, which inflates tag-level signals.** 12 studios with ≥ 2 entries hold **28 of the recent top 60**. Jungle Tavern and WeLoPlay have 4 each. Jungle Tavern's first Poki game (Count Control Legends, 2025-11-10, flagged "first game on Poki") was followed by 3 more, and all 4 are in the recent top 50 (767–2,547 votes/day). Crazy Games (8/10 from 3 studios), Running, Fashion and Beauty all lean on these studios. [dataset: developer counts in top 60 / top 50] Inference: the reproducible thing may be those studios' execution pattern (3D, short sessions, "Legends"-style meta loops) more than the tag.

**O5. Soft-launch votes land before release_date, which inflates very young games.** release_date looks like the *global* release date. Vortelli's Pizza Delivery "launched on Poki on September 20, 2023" (https://poki.com/blog/6-million-plays-in-30-days-vortellis-pizza-delivery), but its dataset release_date is 2023-10-24. That is consistent with the docs' soft release of "around 2-3 weeks" before global release. So votes from the soft launch sit in the numerator while days are counted from global release. Teleport Master (6.3 days old, 6,344 votes → 906/day) and NSR Street Car Racing (6.0 days → 1,582/day) are in the recent top 50 for this reason. 5 of the top 50 are < 30 days old, and 15 are < 90 days old against 19% of the cohort. Restricting to games ≥ 90 days old (baseline 109.4):
- **Leads that shrink or collapse:** Obby 267 → 128 (n=7), Horror 307 → 193 (6), Crazy 779 → 408 (9), Soccer 472 → 284 (8).
- **Leads that hold:** .io 607 (6), Running 869 (8), Stickman 400 (9), Ragdoll 298 (11), Fashion 282 (11), 2 Player 263 (22), 3D 176 (86).

[dataset]

**O6. Votes per play vary by more than 10× between games, so votes are a noisy volume proxy.** The plays figures come from the sources and the votes from today's dataset. Plays were reported at article time and votes are counted today, so each ratio is an upper bound.

| Game | Plays (source) | Votes today | Votes/plays |
|---|---|---|---|
| Rainbow Obby | "100 million gameplays" | 1,546,672 | ≤ 1.5% |
| Draw My Path Obby | emolingo: "Each of the studio's eight games … has surpassed 10 million plays" | 66,392 | ≤ 0.66% |
| Grow My Farm | same | 68,262 | ≤ 0.68% |
| Car Machines | same | 91,226 | ≤ 0.9% |
| Vortelli's Pizza Delivery | "played over 8 million times" | 272,763 | ≤ 3.4% |
| Bo's Bedroom | "over 2 million gameplays" | 5,720 | ≤ 0.29% |
| Sushi Merge | "millions of gameplays on the game's first month" | 9,906 | ≤ 0.5% |

Sources: https://poki.com/blog/how-emolingo-games-built-business-html5-web-games-poki; https://poki.com/blog/6-million-plays-in-30-days-vortellis-pizza-delivery; https://defold.com/2026/02/17/Creator-Spotlight-Kuyi-Mobile/; https://kuyimobile.substack.com/p/the-year-that-was-2025.

Inference: genre gaps under about 2× in votes/day may partly reflect how often players vote rather than how much they play. Casual merge/idle titles (Kuyi Mobile) show very few votes per play. The Merge/Puzzle weakness is still backed by independent evidence: Puzzle holds 2 of the homepage top 60 (0.28×), and those categories stay weak after every robustness cut.

**O7. Outcomes are heavy-tailed; the report gives no absolute expectation for a typical release.** The top 10% of recent games hold 57% of all recent votes, and the top 20% hold 74%. For recent games aged 180–365 days (past the launch push), total votes are p25 10,306 / median 29,764 / p75 82,978 / p90 219,497. [dataset]

**O8. Few games seem to disappear after global release.** 211 of the "227 new game releases" Poki reports for 2025 are live today with a 2025 date (93%). Inference: most filtering happens before global release, in tests and soft launch. So the report's statement that "true hit rates per genre are lower than shown" probably matters less for post-launch outcomes than for getting accepted at all. The two counts may be defined differently.

**O9. Frequent updates go with traction (correlation only).** The recent top 60 have a median of 76.5 days since `version_last_updated`, against 196 for the rest. Among recent games ≥ 180 days old, 19% of the top quartile were updated in the last 60 days, against 9% of the rest. [dataset] Source: https://poki.com/blog/i-quit-my-job-to-make-a-dress-up-web-game-and-it-blew-up says "We were unsure how pushing updates to a game months after its initial launch would perform, but clearly it can work." Success may cause updates as much as updates cause success.

**O10. Poki's own plays data for car games, which the report does not use.** Source: https://poki.com/blog/game-intelligence-car-games says "Car games account for 10% of all US plays on Poki"; "Drive Mad accounts for 23.2% of car game plays, nearly 4x more than the next-largest title"; and "platform games make up 7% of titles but generate 30% of plays". So car demand is large but concentrated in one evergreen game, and Drive Mad is homepage position #1 today. That fits the report's "Middle" rating for recent Car releases (median 157.7, n=31), and adds the reason: a new car game competes with Drive Mad.

**O11. The current soft-launch pipeline, visible in the 32 null-date games (median 1,777 votes, none on the homepage).** By genre: Adventure 4, Simulation 4, Sports 4 (3 soccer), Puzzle 3, Arcade 3, Shooting 2 (including Blockpost 2.0 by Skullcap), Beauty 2 and Racing 2. There is also a second Outfit7 title (talking-tom-drop-and-pop) and a Voodoo title (aquaparkio). [dataset] This is competition that will launch in the next few weeks.

---

## (c) Corrected key findings for pitch designers

Every votes figure is thumbs votes, a proxy for player volume. Votes are not plays; see O6 for why.

1. **Market size and pace.** 1,503 games are live. 408 were released since 2025-01-01, about 4–5 global releases a week (211 live from 2025, 197 in 2026 up to Sep 28; Poki reports "227 new game releases" in 2025). A typical recent release gets a median 127.5 votes/day; p75 is 352 and p90 is 874. [dataset; poki.com/blog/2025-at-poki-a-year-in-review]
2. **Always compare at the same age.** New games get "a significant push for around 2 weeks" (developers.poki.com/guide/release-process), and soft-launch votes predate release_date. Median votes/day is 337 at 0–30 days against 99 after a year. Judge concepts on games ≥ 90 days old (baseline 109).
3. **3D is the most robust positive trait.** Recent 3D-tagged games have a median of 196 votes/day vs 101 for the rest. The gap holds in every age band, after removing brands (clean 196, n=92), and at 1.76× over-representation in the recent top 50.
4. **Genre bets that survive every cut** (brand removal, top-studio removal, age ≥ 90 d): Ragdoll (≈298, 13 devs), Stickman (≈400, n=9–11), 2 Player (≈263, 19 devs), Fashion/Dress-up/Beauty (≈185–280; WeLoPlay-heavy) and Sports (≈250–325; soccer-heavy). .io holds (≈607–625) but only n = 6–7, and it means real-time multiplayer.
5. **Downgrade these "robust" signals:**
   - Crazy Games: 8/10 from 3 studios; 271 without Jungle Tavern.
   - Soccer: 284 for games ≥ 90 d; 7/11 released around the 2026 World Cup; 3 more soccer games in soft launch.
   - Obby: 128 for games ≥ 90 d; its homepage lift comes from older hits carrying the tag.
   - Running: 266 once Talking Tom is removed.
   - Horror: n = 8; 193 for games ≥ 90 d.
   - Gun/Shooting: brand- and ⚑-driven; Gun clean 48, Shooting clean 194.
   - Parkour, Basketball, Bike: n = 5 each.
6. **Consistently weak on every cut:** Puzzle genre (median 33, n=45; 2 of the homepage top 60, lift 0.28×), Merge (27, n=41), Matching (25), Match-3 (11), Idle genre (65), Brain (66–78), Arcade genre (30) and Retro (36). They are also crowded: the Puzzle, Brain and Merge tags are on 21%, 18% and 10% of recent releases (tags overlap).
7. **Simulation is crowded, not hot.** It is the largest recent genre (71 releases, 17%). Its outcomes are about average (median 136, age-adjusted 1.02) and it is 0.92–0.97× represented in the top 50: supply is rising, hit rate is not. The winning pattern Devortel describes is that players "wanted to control a character that runs around in a little world" (poki.com/blog/i-quit-my-job-to-make-a-dress-up-web-game-and-it-blew-up).
8. **The homepage rewards new, performing games.** 30 of the top 60 slots and 86 of 145 go to 2025–26 releases, which are 27% of the catalogue. Among those, position correlates with votes/day at ρ = −0.53. Causation runs both ways. Skill is the top homepage genre (14/60, 1.95×).
9. **Brands raise the floor but do not own the chart.** 47 recent big-brand ports have a median of 181 vs 119 for everyone else. They take 4 of the top 10 and 7 of the top 20, but only 11 of the top 60. Do not repeat "82% of hits are indie": 35 of the 49 "indie" labels are unverified defaults.
10. **Debuts perform about average but rarely become the biggest hits.** First-game-on-Poki titles have a median of 120 votes/day vs 129 for other games, and a top-quartile share of 23% vs 26%. They hold only 9 of the top 60 (15%) against 24% of releases. Repeat studios dominate the top (12 studios hold 28 of the top 60). Developers with 2–9 games do best (medians 136–155). Inference: plan a series of releases, not a single shot.
11. **Quality floor: at least 80% thumbs-up.** Rating = 1 + 4 × thumbs-up share, so rating 4.2 means 80% up. 54 of the recent top 60 are at ≥ 80%, and games below that have a median of 65 votes/day. Rating correlates only weakly with scale (ρ = 0.27), so it gates success rather than predicting it.
12. **Platform.** Ship on mobile and desktop (397 of 408 recent releases do; desktop-only is a legacy niche at median 12) and support portrait. Poki "strongly advise[s] supporting portrait" (developers.poki.com/guide/easy-access), and 55 of the top 60 do.
13. **Set realistic expectations.** The top 10% of recent games hold 57% of recent votes. A recent game past its launch window (180–365 days old) has a median of about 30k total votes; p75 is about 83k and p90 about 219k.
14. **Keep updating after launch.** Top-60 games were updated a median of 77 days ago vs 196 for the rest (correlation only). Devortel's blog says post-launch updates "clearly it can work".
15. **Leave room for measurement error.** Votes per play range from ≤ 0.3% to ≤ 3.4% across the documented cases. Inference: treat any category gap under about 2× as within the noise of the metric, and rely on findings 3–6, which hold across several independent cuts.

Files: `analysis/catalog.verified.md` (this file) and `analysis/verify_catalog.py` (independent recomputation).
