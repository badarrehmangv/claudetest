# Poki catalogue analysis — what gets traction (as of 2026-09-29)

Analyst: catalogue/quant stream. Data: `poki/games.jsonl` (1,503 games live on poki.com, crawled 2026-09-29) and `poki/homepage.json` (today's poki.com/en desktop homepage order). All numbers below are computed by `analysis/catalog_build.py` (reproducible, pure python); citation tag **[dataset: …]** names the computation.

## 0. Method and caveats (read first)

- **Votes are not plays.** `votes = up + down` (thumbs votes) is the best available proxy for cumulative player volume; `votes/day = votes / max(days since release_date, 7)` is the proxy for current traction. Both are proxies only. [dataset]
- **Recent cohort** = games with release_date ≥ 2025-01-01: **n = 408**. Overall recent medians: votes/day median **127.5**, p75 **352.1**, p90 **874.1**. [dataset: votes/max(days,7) over 408 games]
- 32 games have null release_date (likely soft release; the Poki docs say soft-release games appear only "on relevant category pages" and "We're not promoting the game on our homepage" — https://developers.poki.com/guide/release-process). They are excluded from all votes/day stats. 95 games carry the 2019-03-11 bulk-migration date and are treated as "2019 or earlier". [dataset]
- **Launch-boost bias.** Poki states a new game "will also get a significant push for around 2 weeks" after global release (https://developers.poki.com/guide/release-process). The data shows the effect: newer games have higher votes/day (Spearman(days, votes/day) = -0.24 over 408 recent games). Median votes/day by age band: 0-30d: 336.9 (n=25); 30-90d: 151.1 (n=53); 90-180d: 165.8 (n=59); 180-365d: 108.8 (n=118); 365-∞d: 98.8 (n=153). I therefore add an **age-adjusted index** (a game's votes/day ÷ median votes/day of recent games in the same age band; 1.0 = typical) as a robustness column. [dataset]
- **Possible re-releases / long soft launches.** For 12 recent games the Poki game id is much older than the release_date (id-implied creation date > 365 days before release, estimated from the median release date of the 21 nearest ids), so votes may predate the release date and votes/day is inflated: blockpost (1409d), paperio-2 (481d), sprunki (428d), drift-hunters (2363d), hill-climb-racing-lite (366d), speed-stars (438d), magikmon (2293d), ant-art-tycoon (2099d), blockpost-legacy (1043d), kates-cooking-party (1181d), lips-diy-master (531d), dummies-fight (425d). Flagged ⚑ in tables. [dataset: id vs release_date]
- **Legacy re-releases.** 8 recent releases are Flash-era catalogue re-releases by Flipline Studios, Nitrome (median votes/day 1.9); they depress Retro/Arcade/Platform medians and are excluded from the "clean" robustness column. [dataset]
- **"Clean" baseline** used for robustness = recent games excluding big-brand/publisher ports (Fingersoft, Gametion Global, Hipster Whale, Imangi Studios, Lion Studios, Outfit7, SYBO, SayGames, StoreRider, Sybo, Unico Studio, Voodoo, Yes2Games, ZnK Games), ⚑ and legacy re-releases: n = 343, median votes/day **118.8**. [dataset]
- **Survivorship.** The dataset only contains games live today; games that failed soft release or were removed are invisible, so medians describe survivors, not all submissions. Inference: true hit rates per genre are lower than shown.
- **Editorial/meta tags** (marked †: Flash Games, Mobile Games, New Games, Popular Games) and developer-franchise tags (‡: Henry Stickmin Games, Nitrome Games, Papa's Games) are shown in tables but excluded from opportunity and trend claims ("Popular Games"/"Mobile Games" are applied to already-successful games, so their traction is circular — e.g. 84% of recent "Popular Games" are in the recent top quartile). "Games for Boys/Girls" are audience tags.
- Require n ≥ 5 for any claim; n is shown everywhere. Percentiles use linear interpolation.

## 1. Release volume

### 1a. Games live today by release year [dataset: count by release_date year; migration date and null separated]

| Release year | Games live today |
|---|---|
| 2013 | 1 |
| 2018 | 1 |
| 2019 | 146 |
| 2020 | 169 |
| 2021 | 157 |
| 2022 | 131 |
| 2023 | 128 |
| 2024 | 235 |
| 2025 | 211 |
| 2026 | 197 |
| 2019-03-11 migration bucket (≤2019) | 95 |
| null (soft release?) | 32 |
| **Total** | 1503 |

### 1b. By quarter, 2023–2026 [dataset: count by release quarter]

| Year | Q1 | Q2 | Q3 | Q4 | Year total |
|---|---|---|---|---|---|
| 2023 | 33 | 21 | 16 | 58 | 128 |
| 2024 | 40 | 59 | 48 | 88 | 235 |
| 2025 | 43 | 57 | 54 | 57 | 211 |
| 2026 (Q3 through 2026-09-28; Q4 not started) | 58 | 60 | 79 | 0 | 197 |

Interpretation: releases stepped up from 128 (2023) to 235 (2024) and have held at ~200+/yr since (211 in 2025; 197 in 2026 through Sep 28 = 265/yr annualised pace). [dataset] Cross-check: Poki reports "227 new game releases" in 2025 (https://poki.com/blog/2025-at-poki-a-year-in-review); 211 of 2025-dated games are live today. Inference: roughly 4–5 global releases per week compete for the same new-game promotion slots; in 2025–26 each quarter brought 43–79 releases, with 2026 Q3 the busiest on record in this window.

## 2. Genre and category performance

Columns: n (all) = games live today; median / p90 ("top decile" threshold) of total votes across all ages; recent = released ≥ 2025-01-01 (n=408); votes/day stats shown only when n recent ≥ 5; age-adj idx = median age-adjusted index (1.0 = typical recent game of the same age); "share in recent top quartile" = share of the group's recent games with votes/day ≥ 352.1 (the recent-cohort p75; baseline 25%). [dataset]

### 2a. Primary genre (field `genre`), sorted by recent median votes/day

| Primary genre | n (all) | median votes | p90 votes | n recent (≥2025) | median votes/day | p75 votes/day | age-adj idx | share in recent top quartile |
|---|---|---|---|---|---|---|---|---|
| Shooting Games | 73 | 177,662 | 881,085 | 20 | 357.1 | 644.6 | 3.07 | 50% |
| Sports Games | 97 | 85,731 | 962,269 | 21 | 274.3 | 818.8 | 2.55 | 48% |
| Fighting Games | 29 | 224,067 | 714,527 | 6 | 224.6 | 578.1 | 1.36 | 33% |
| Beauty Games | 53 | 140,340 | 660,390 | 24 | 221.2 | 520.1 | 1.55 | 38% |
| Racing Games | 70 | 125,170 | 996,626 | 15 | 198.4 | 354.6 | 1.66 | 27% |
| Driving Games | 62 | 204,963 | 1,289,582 | 20 | 158.1 | 314.8 | 1.36 | 25% |
| Board Games | 26 | 67,404 | 607,061 | 5 | 148.9 | 159.4 | 1.51 | 0% |
| Decoration Games | 25 | 89,352 | 366,359 | 12 | 145.4 | 303.0 | 1.12 | 25% |
| Adventure Games | 45 | 40,069 | 321,252 | 17 | 136.5 | 319.6 | 0.82 | 24% |
| Simulation Games | 178 | 71,239 | 402,438 | 71 | 135.7 | 386.0 | 1.02 | 28% |
| Action Games | 53 | 65,330 | 1,116,290 | 28 | 135.6 | 396.2 | 0.94 | 25% |
| Escape Games | 11 | 159,358 | 534,900 | 6 | 135.4 | 317.6 | 1.06 | 33% |
| Platform Games | 129 | 73,933 | 481,841 | 21 | 128.4 | 266.1 | 1.05 | 14% |
| Skill Games | 180 | 84,676 | 756,428 | 39 | 107.6 | 472.2 | 0.72 | 31% |
| Strategy Games | 30 | 64,690 | 385,995 | 5 | 94.5 | 119.9 | 0.64 | 0% |
| Brain Games | 99 | 35,685 | 262,811 | 27 | 78.1 | 117.1 | 0.67 | 15% |
| Idle Games | 48 | 27,950 | 380,988 | 17 | 64.7 | 306.1 | 0.64 | 12% |
| Puzzle Games | 176 | 20,771 | 214,127 | 45 | 33.1 | 158.8 | 0.31 | 9% |
| Arcade Games | 82 | 13,362 | 310,648 | 8 | 29.9 | 56.9 | 0.29 | 12% |
| Card Games | 21 | 9,701 | 33,266 | 1 | – | – | – | – |
| Educational Games | 9 | 142,011 | 183,876 | 0 | – | – | – | – |
| Battle Royale Games | 7 | 780,704 | 1,983,374 | 0 | – | – | – | – |

Interpretation (2a): leaders among recent releases by median votes/day — Shooting 357 (n=20; clean 194); Sports 274 (n=21; clean 325); Fighting 225 (n=6; clean –); Beauty 221 (n=24; clean 229); Racing 198 (n=15; clean 157). Laggards — Puzzle 33 (n=45; clean 31); Arcade 30 (n=8; clean 35); Idle 65 (n=17; clean 61); Brain 78 (n=27; clean 77); Strategy 94 (n=5; clean 94). Puzzle is the 3rd-largest primary genre (176 games live) yet recent Puzzle releases have a median of only 33 votes/day. Shooting and Racing lose much of their lead once brand ports and ⚑ games are removed (clean medians above); Sports and Beauty hold up. [dataset] Inference: Sports and Beauty/dress-up are the genre-level bets whose strength does not depend on brands.

### 2b. Every category (exploded `categories` list; a game counts in each of its categories), sorted by recent median votes/day; groups with n recent < 5 listed after, by size

| Category | n (all) | median votes | p90 votes | n recent (≥2025) | median votes/day | p75 votes/day | age-adj idx | share in recent top quartile |
|---|---|---|---|---|---|---|---|---|
| Popular Games † | 99 | 326,550 | 1,969,270 | 62 | 965.7 | 1,527.5 | 5.97 | 84% |
| .io Games | 40 | 262,840 | 1,745,385 | 9 | 860.3 | 1,488.5 | 5.96 | 78% |
| Crazy Games | 67 | 339,094 | 1,717,770 | 10 | 779.3 | 2,075.1 | 7.89 | 60% |
| Mobile Games † | 98 | 207,998 | 1,550,179 | 67 | 750.9 | 1,360.5 | 5.19 | 84% |
| Running Games | 47 | 250,446 | 1,706,285 | 11 | 744.0 | 1,666.3 | 4.49 | 55% |
| First Person Shooter Games | 16 | 181,536 | 1,409,117 | 6 | 494.0 | 638.3 | 3.70 | 50% |
| Soccer Games | 39 | 201,110 | 1,392,303 | 11 | 472.0 | 933.1 | 3.12 | 64% |
| Parkour Games | 29 | 157,255 | 1,551,061 | 5 | 437.4 | 540.6 | 3.26 | 60% |
| Games for Boys | 272 | 251,971 | 1,536,136 | 45 | 336.9 | 932.8 | 2.74 | 47% |
| Ragdoll Games | 30 | 129,012 | 605,378 | 14 | 332.4 | 872.9 | 2.25 | 50% |
| Sports Games | 148 | 120,010 | 1,009,130 | 22 | 325.4 | 803.9 | 2.66 | 50% |
| Gun Games | 63 | 220,437 | 1,097,524 | 16 | 309.3 | 644.6 | 3.13 | 44% |
| Horror Games | 25 | 52,054 | 185,449 | 8 | 306.7 | 382.9 | 2.48 | 50% |
| Stickman Games | 60 | 253,675 | 1,061,599 | 13 | 298.1 | 804.6 | 2.45 | 46% |
| Fashion Games | 35 | 129,098 | 637,342 | 15 | 281.9 | 678.8 | 1.96 | 47% |
| Basketball Games | 16 | 108,304 | 824,686 | 5 | 274.3 | 281.6 | 2.59 | 20% |
| Obby Games | 36 | 217,032 | 1,557,644 | 11 | 267.2 | 1,081.8 | 2.10 | 45% |
| 2 Player Games | 136 | 226,600 | 1,436,631 | 23 | 260.5 | 402.0 | 2.27 | 30% |
| Cozy Games | 82 | 93,140 | 549,696 | 13 | 255.3 | 403.8 | 1.26 | 31% |
| Games for Girls | 181 | 165,186 | 708,804 | 46 | 231.4 | 551.7 | 2.12 | 35% |
| Ball Games | 93 | 69,696 | 572,950 | 16 | 231.3 | 528.1 | 2.05 | 44% |
| Shooting Games | 104 | 150,950 | 877,225 | 28 | 230.5 | 637.4 | 2.08 | 43% |
| Bike Games | 25 | 160,465 | 1,576,303 | 5 | 226.5 | 290.9 | 1.76 | 20% |
| Dress Up Games | 65 | 126,371 | 577,623 | 28 | 221.2 | 476.1 | 1.55 | 36% |
| Beauty Games | 63 | 129,098 | 579,194 | 28 | 221.2 | 476.1 | 1.55 | 36% |
| Fighting Games | 60 | 209,446 | 947,838 | 11 | 214.9 | 484.8 | 0.93 | 27% |
| Meme Games | 18 | 136,585 | 673,718 | 10 | 210.9 | 464.8 | 1.10 | 30% |
| 3D Games | 277 | 85,731 | 976,831 | 111 | 196.0 | 530.0 | 1.73 | 36% |
| Airplane Games | 11 | 65,953 | 208,341 | 5 | 193.6 | 196.0 | 1.80 | 0% |
| Color Games | 42 | 57,326 | 378,832 | 9 | 186.7 | 688.0 | 1.24 | 44% |
| Multiplayer Games | 152 | 222,290 | 1,417,569 | 41 | 186.6 | 519.3 | 1.73 | 32% |
| Escape Games | 43 | 165,186 | 1,120,637 | 11 | 181.8 | 317.1 | 1.84 | 27% |
| Christmas Games | 20 | 149,404 | 1,229,969 | 5 | 177.9 | 267.2 | 1.80 | 20% |
| War Games | 43 | 244,101 | 889,899 | 6 | 173.7 | 320.8 | 1.76 | 33% |
| Racing Games | 125 | 127,296 | 1,237,038 | 31 | 170.8 | 414.0 | 1.62 | 29% |
| New Games † | 131 | 8,586 | 69,327 | 124 | 165.7 | 472.1 | 0.99 | 34% |
| Driving Games | 114 | 127,334 | 1,272,973 | 28 | 165.4 | 377.9 | 1.60 | 29% |
| Number Games | 38 | 19,921 | 207,396 | 15 | 159.4 | 595.0 | 1.00 | 33% |
| Car Games | 128 | 139,456 | 1,014,473 | 31 | 157.7 | 360.3 | 1.45 | 26% |
| Action Games | 322 | 125,943 | 965,983 | 97 | 153.7 | 437.4 | 1.25 | 31% |
| Simulation Games | 263 | 80,999 | 479,108 | 93 | 136.7 | 370.4 | 1.02 | 27% |
| Brainrot Games | 27 | 111,929 | 549,987 | 17 | 136.5 | 407.8 | 1.30 | 29% |
| Drawing Games | 35 | 64,310 | 289,106 | 13 | 135.0 | 688.0 | 1.22 | 38% |
| Decoration Games | 35 | 58,418 | 366,359 | 16 | 131.7 | 303.0 | 1.08 | 25% |
| Monster Games | 23 | 29,028 | 157,535 | 10 | 131.5 | 545.4 | 1.01 | 30% |
| Skill Games | 410 | 84,550 | 766,251 | 80 | 128.6 | 472.1 | 1.00 | 30% |
| Make Up Games | 16 | 190,143 | 685,219 | 6 | 126.5 | 249.5 | 0.97 | 17% |
| Adventure Games | 234 | 87,078 | 834,218 | 61 | 120.5 | 233.5 | 0.95 | 20% |
| Board Games | 57 | 26,408 | 214,400 | 6 | 118.7 | 156.8 | 1.16 | 0% |
| Mouse Games | 317 | 75,636 | 673,498 | 70 | 113.8 | 458.6 | 0.91 | 30% |
| Co-op Games | 32 | 247,410 | 1,443,022 | 5 | 113.8 | 260.5 | 1.05 | 0% |
| Cooking Games | 30 | 163,164 | 443,323 | 6 | 107.9 | 262.2 | 0.82 | 17% |
| Platform Games | 211 | 70,929 | 534,900 | 43 | 103.3 | 266.6 | 0.84 | 19% |
| Construction Games | 19 | 17,240 | 479,647 | 8 | 97.7 | 173.3 | 0.66 | 0% |
| Farm Games | 25 | 59,097 | 382,747 | 7 | 94.9 | 333.4 | 0.87 | 29% |
| Strategy Games | 65 | 67,938 | 381,599 | 15 | 88.4 | 161.5 | 0.64 | 7% |
| Cat Games | 32 | 97,283 | 318,447 | 11 | 88.3 | 287.1 | 0.58 | 27% |
| Slime Games | 15 | 42,049 | 220,849 | 7 | 84.6 | 293.8 | 0.51 | 14% |
| Idle Games | 130 | 33,812 | 359,404 | 57 | 80.1 | 261.6 | 0.69 | 18% |
| Watermelon Games | 18 | 8,475 | 390,035 | 5 | 77.9 | 85.1 | 0.56 | 20% |
| Easy Games | 81 | 116,530 | 520,974 | 13 | 76.6 | 600.8 | 0.67 | 38% |
| Restaurant Games | 41 | 118,625 | 411,100 | 10 | 76.3 | 262.6 | 0.63 | 20% |
| Clicker Games | 38 | 30,972 | 428,539 | 15 | 74.8 | 242.8 | 0.69 | 20% |
| Tower Defense Games | 29 | 60,443 | 379,697 | 7 | 72.6 | 107.2 | 0.44 | 14% |
| Food Games | 82 | 69,915 | 577,609 | 16 | 71.5 | 178.6 | 0.62 | 19% |
| Brain Games | 340 | 41,078 | 340,709 | 75 | 66.1 | 175.6 | 0.58 | 16% |
| Tycoon Games | 62 | 82,594 | 430,141 | 17 | 64.7 | 195.7 | 0.65 | 18% |
| Arcade Games | 219 | 53,637 | 698,699 | 22 | 61.7 | 215.4 | 0.46 | 14% |
| Animal Games | 165 | 47,931 | 428,003 | 48 | 60.8 | 197.2 | 0.53 | 17% |
| Survival Games | 41 | 72,749 | 1,450,028 | 12 | 58.3 | 104.4 | 0.57 | 0% |
| Zombie Games | 31 | 50,960 | 631,046 | 11 | 58.3 | 482.7 | 0.59 | 36% |
| Puzzle Games | 355 | 34,876 | 313,708 | 85 | 57.3 | 157.7 | 0.43 | 12% |
| Bubble Shooter Games | 20 | 17,734 | 226,304 | 5 | 57.3 | 65.5 | 0.40 | 0% |
| Dinosaur Games | 18 | 54,588 | 1,364,433 | 9 | 51.5 | 298.1 | 0.52 | 22% |
| Block Games | 62 | 61,316 | 543,409 | 16 | 49.1 | 205.4 | 0.36 | 6% |
| Difficult Games | 120 | 302,772 | 2,099,109 | 6 | 47.0 | 1,923.2 | 0.43 | 33% |
| Hidden Object Games | 35 | 67,884 | 309,913 | 7 | 46.3 | 258.2 | 0.47 | 29% |
| Retro Games | 74 | 36,610 | 455,712 | 16 | 36.2 | 48.7 | 0.27 | 6% |
| Merge Games | 82 | 11,989 | 318,171 | 41 | 27.2 | 85.1 | 0.23 | 7% |
| Matching Games | 76 | 19,584 | 179,104 | 25 | 25.2 | 85.1 | 0.19 | 4% |
| Match 3 Games | 21 | 20,076 | 83,848 | 5 | 11.3 | 50.7 | 0.10 | 0% |
| Nitrome Games ‡ | 37 | 4,953 | 177,351 | 6 | 1.4 | 2.2 | 0.01 | 0% |
| Flash Games † | 98 | 74,598 | 768,707 | 2 | – | – | – | – |
| Classic Games | 67 | 68,826 | 368,320 | 1 | – | – | – | – |
| 1v1 Games | 60 | 515,689 | 1,758,187 | 3 | – | – | – | – |
| Educational Games | 28 | 63,734 | 225,172 | 2 | – | – | – | – |
| Halloween Games | 28 | 118,294 | 873,334 | 2 | – | – | – | – |
| Card Games | 23 | 9,701 | 31,803 | 2 | – | – | – | – |
| Drifting Games | 20 | 380,430 | 1,456,786 | 1 | – | – | – | – |
| Quiz Games | 20 | 107,892 | 883,323 | 0 | – | – | – | – |
| Truck Games | 19 | 165,138 | 656,834 | 1 | – | – | – | – |
| Solitaire Games | 18 | 8,306 | 28,085 | 2 | – | – | – | – |
| Snake Games | 18 | 99,332 | 1,063,707 | 4 | – | – | – | – |
| Maze Games | 17 | 58,811 | 593,653 | 2 | – | – | – | – |
| Papa's Games ‡ | 17 | 126,905 | 510,691 | 2 | – | – | – | – |
| Word Games | 16 | 34,228 | 144,093 | 1 | – | – | – | – |
| Dirt Bike Games | 16 | 201,872 | 1,732,614 | 3 | – | – | – | – |
| Mahjong Games | 15 | 24,296 | 59,383 | 1 | – | – | – | – |
| Fish Games | 14 | 46,637 | 573,952 | 2 | – | – | – | – |
| Space Games | 13 | 60,519 | 372,421 | 3 | – | – | – | – |
| Doctor Games | 12 | 157,493 | 555,666 | 3 | – | – | – | – |
| Robot Games | 12 | 16,562 | 308,353 | 4 | – | – | – | – |
| Tank Games | 12 | 250,719 | 561,643 | 3 | – | – | – | – |
| Police Games | 11 | 301,742 | 1,303,159 | 2 | – | – | – | – |
| World Cup Games | 11 | 269,974 | 1,421,178 | 4 | – | – | – | – |
| Pizza Games | 11 | 102,631 | 406,497 | 3 | – | – | – | – |
| Monster Truck Games | 11 | 281,117 | 1,128,422 | 1 | – | – | – | – |
| Battle Royale Games | 11 | 555,911 | 2,319,969 | 0 | – | – | – | – |
| Dog Games | 10 | 17,919 | 181,141 | 2 | – | – | – | – |
| Anime Games | 10 | 499,936 | 1,271,115 | 3 | – | – | – | – |
| Football Games | 10 | 47,587 | 220,390 | 1 | – | – | – | – |
| Penalty Games | 10 | 247,714 | 1,338,184 | 1 | – | – | – | – |
| Boat Games | 9 | 73,260 | 733,938 | 2 | – | – | – | – |
| Sniper Games | 9 | 546,455 | 996,666 | 1 | – | – | – | – |
| Jigsaw Puzzle Games | 8 | 16,653 | 96,682 | 2 | – | – | – | – |
| Parking Games | 8 | 89,684 | 564,695 | 1 | – | – | – | – |
| Boxing Games | 8 | 103,860 | 628,752 | 0 | – | – | – | – |
| Wrestling Games | 8 | 249,626 | 751,057 | 0 | – | – | – | – |
| Cake Games | 8 | 119,242 | 346,433 | 0 | – | – | – | – |
| Hunting Games | 8 | 636,445 | 1,211,678 | 0 | – | – | – | – |
| Love Games | 8 | 326,674 | 407,612 | 0 | – | – | – | – |
| Shopping Games | 7 | 170,194 | 1,931,874 | 1 | – | – | – | – |
| Fishing Games | 7 | 35,406 | 319,483 | 3 | – | – | – | – |
| Princess Games | 7 | 275,409 | 1,151,129 | 1 | – | – | – | – |
| Horse Games | 7 | 140,340 | 370,047 | 1 | – | – | – | – |
| Chess Games | 7 | 75,787 | 835,350 | 1 | – | – | – | – |
| Typing Games | 6 | 41,856 | 84,752 | 0 | – | – | – | – |
| Tractor Games | 6 | 157,912 | 353,808 | 2 | – | – | – | – |
| Hair Games | 6 | 335,340 | 909,982 | 2 | – | – | – | – |
| Pool Games | 6 | 86,844 | 449,174 | 0 | – | – | – | – |
| Sudoku Games | 6 | 28,669 | 76,918 | 0 | – | – | – | – |
| Backrooms Games | 5 | 541,462 | 2,725,334 | 1 | – | – | – | – |
| Monkey Games | 5 | 101,515 | 2,399,077 | 1 | – | – | – | – |
| Music Games | 5 | 232,149 | 2,424,951 | 1 | – | – | – | – |
| Hockey Games | 5 | 23,183 | 96,256 | 1 | – | – | – | – |
| Tennis Games | 5 | 423,095 | 703,511 | 0 | – | – | – | – |
| Henry Stickmin Games ‡ | 5 | 1,006,403 | 2,920,611 | 0 | – | – | – | – |
| Bowling Games | 4 | 103,896 | 125,316 | 0 | – | – | – | – |
| Cricket Games | 3 | 153,487 | 338,266 | 0 | – | – | – | – |
| Golf Games | 3 | 79,163 | 109,754 | 0 | – | – | – | – |
| Bus Games | 2 | 343,511 | 513,431 | 1 | – | – | – | – |
| Baseball Games | 1 | 31,259 | 31,259 | 1 | – | – | – | – |

Interpretation (2b): excluding editorial (†) and franchise (‡) tags, the 12 highest recent medians (votes/day) are .io 860 (n=9), Crazy 779 (n=10), Running 744 (n=11), First Person Shooter 494 (n=6), Soccer 472 (n=11), Parkour 437 (n=5), Games for Boys 337 (n=45), Ragdoll 332 (n=14), Sports 325 (n=22), Gun 309 (n=16), Horror 307 (n=8), Stickman 298 (n=13); the 10 lowest are Match 3 11 (n=5), Matching 25 (n=25), Merge 27 (n=41), Retro 36 (n=16), Hidden Object 46 (n=7), Difficult 47 (n=6), Block 49 (n=16), Dinosaur 51 (n=9), Bubble Shooter 57 (n=5), Puzzle 57 (n=85). Section 2c tests which of these hold up after removing brand ports and re-releases. [dataset]

### 2c. Demand vs supply opportunity table (categories, recent releases only)

Rules (fixed before looking at names): **demand index** = category median votes/day ÷ recent-cohort median (127.5). **Supply** = number of 2025–26 releases in the category (share of the 408). Eligible: n recent ≥ 5 and not an editorial/franchise tag. Quadrants: **Under-supplied** = demand index ≥ 1.5 and n recent < 20 (< ~5% of recent releases); **Crowded but rewarding** = index ≥ 1.5 and n recent ≥ 20; **Saturated** = index < 0.8 and n recent ≥ 20; **Thin & weak** = index < 0.8 and n recent < 20. Robustness columns: "clean" median = median votes/day after removing big-brand/publisher ports, ⚑ and legacy re-releases (§0; clean baseline 118.8); age-adjusted index; number of distinct developers. **Robust ✔** = clean median ≥ 1.5× clean baseline AND age-adj idx ≥ 1.5 AND ≥ 4 distinct developers (so the signal is not one studio or one brand). [dataset]

| Quadrant | Category | n recent (share) | distinct devs | median votes/day | demand index | p75 votes/day | clean median (n) | age-adj idx | share in recent top quartile | Robust | n all | p90 total votes (all) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Under-supplied | .io Games | 9 (2.2%) | 7 | 860.3 | 6.75 | 1,488.5 | 625.1 (7) | 5.96 | 78% | ✔ | 40 | 1,745,385 |
| Under-supplied | Crazy Games | 10 (2.5%) | 5 | 779.3 | 6.11 | 2,075.1 | 779.3 (10) | 7.89 | 60% | ✔ | 67 | 1,717,770 |
| Under-supplied | Running Games | 11 (2.7%) | 9 | 744.0 | 5.84 | 1,666.3 | 266.1 (9) | 4.49 | 55% | ✔ | 47 | 1,706,285 |
| Under-supplied | First Person Shooter Games | 6 (1.5%) | 5 | 494.0 | 3.88 | 638.3 | – (4) | 3.70 | 50% | – | 16 | 1,409,117 |
| Under-supplied | Soccer Games | 11 (2.7%) | 9 | 472.0 | 3.70 | 933.1 | 818.8 (9) | 3.12 | 64% | ✔ | 39 | 1,392,303 |
| Under-supplied | Parkour Games | 5 (1.2%) | 5 | 437.4 | 3.43 | 540.6 | 437.4 (5) | 3.26 | 60% | ✔ | 29 | 1,551,061 |
| Under-supplied | Ragdoll Games | 14 (3.4%) | 13 | 332.4 | 2.61 | 872.9 | 298.1 (13) | 2.25 | 50% | ✔ | 30 | 605,378 |
| Under-supplied | Gun Games | 16 (3.9%) | 15 | 309.3 | 2.43 | 644.6 | 48.3 (11) | 3.13 | 44% | – | 63 | 1,097,524 |
| Under-supplied | Horror Games | 8 (2.0%) | 7 | 306.7 | 2.41 | 382.9 | 355.0 (7) | 2.48 | 50% | ✔ | 25 | 185,449 |
| Under-supplied | Stickman Games | 13 (3.2%) | 12 | 298.1 | 2.34 | 804.6 | 400.4 (11) | 2.45 | 46% | ✔ | 60 | 1,061,599 |
| Under-supplied | Fashion Games | 15 (3.7%) | 10 | 281.9 | 2.21 | 678.8 | 354.7 (14) | 1.96 | 47% | ✔ | 35 | 637,342 |
| Under-supplied | Basketball Games | 5 (1.2%) | 4 | 274.3 | 2.15 | 281.6 | 274.3 (5) | 2.59 | 20% | ✔ | 16 | 824,686 |
| Under-supplied | Obby Games | 11 (2.7%) | 10 | 267.2 | 2.10 | 1,081.8 | 427.8 (10) | 2.10 | 45% | ✔ | 36 | 1,557,644 |
| Under-supplied | Cozy Games | 13 (3.2%) | 13 | 255.3 | 2.00 | 403.8 | 104.8 (11) | 1.26 | 31% | – | 82 | 549,696 |
| Under-supplied | Ball Games | 16 (3.9%) | 16 | 231.3 | 1.81 | 528.1 | 281.6 (15) | 2.05 | 44% | ✔ | 93 | 572,950 |
| Under-supplied | Bike Games | 5 (1.2%) | 5 | 226.5 | 1.78 | 290.9 | 226.5 (5) | 1.76 | 20% | ✔ | 25 | 1,576,303 |
| Under-supplied | Fighting Games | 11 (2.7%) | 10 | 214.9 | 1.69 | 484.8 | 222.0 (9) | 0.93 | 27% | – | 60 | 947,838 |
| Under-supplied | Meme Games | 10 (2.5%) | 8 | 210.9 | 1.65 | 464.8 | 196.8 (8) | 1.10 | 30% | – | 18 | 673,718 |
| Under-supplied | Airplane Games | 5 (1.2%) | 5 | 193.6 | 1.52 | 196.0 | – (4) | 1.80 | 0% | – | 11 | 208,341 |
| Crowded but rewarding | Games for Boys | 45 (11.0%) | 32 | 336.9 | 2.64 | 932.8 | 211.3 (36) | 2.74 | 47% | ✔ | 272 | 1,536,136 |
| Crowded but rewarding | Sports Games | 22 (5.4%) | 17 | 325.4 | 2.55 | 803.9 | 376.5 (19) | 2.66 | 50% | ✔ | 148 | 1,009,130 |
| Crowded but rewarding | 2 Player Games | 23 (5.6%) | 19 | 260.5 | 2.04 | 402.0 | 263.3 (20) | 2.27 | 30% | ✔ | 136 | 1,436,631 |
| Crowded but rewarding | Games for Girls | 46 (11.3%) | 25 | 231.4 | 1.82 | 551.7 | 228.7 (43) | 2.12 | 35% | ✔ | 181 | 708,804 |
| Crowded but rewarding | Shooting Games | 28 (6.9%) | 25 | 230.5 | 1.81 | 637.4 | 152.7 (20) | 2.08 | 43% | – | 104 | 877,225 |
| Crowded but rewarding | Dress Up Games | 28 (6.9%) | 16 | 221.2 | 1.74 | 476.1 | 228.7 (27) | 1.55 | 36% | ✔ | 65 | 577,623 |
| Crowded but rewarding | Beauty Games | 28 (6.9%) | 16 | 221.2 | 1.74 | 476.1 | 228.7 (27) | 1.55 | 36% | ✔ | 63 | 579,194 |
| Crowded but rewarding | 3D Games | 111 (27.2%) | 63 | 196.0 | 1.54 | 530.0 | 196.4 (92) | 1.73 | 36% | ✔ | 277 | 976,831 |
| Middle | Color Games | 9 (2.2%) | 8 | 186.7 | 1.47 | 688.0 | 88.6 (6) | 1.24 | 44% | – | 42 | 378,832 |
| Middle | Multiplayer Games | 41 (10.0%) | 29 | 186.6 | 1.46 | 519.3 | 174.1 (38) | 1.73 | 32% | – | 152 | 1,417,569 |
| Middle | Escape Games | 11 (2.7%) | 7 | 181.8 | 1.43 | 317.1 | 241.1 (6) | 1.84 | 27% | ✔ | 43 | 1,120,637 |
| Middle | Christmas Games | 5 (1.2%) | 5 | 177.9 | 1.40 | 267.2 | 177.9 (5) | 1.80 | 20% | – | 20 | 1,229,969 |
| Middle | War Games | 6 (1.5%) | 5 | 173.7 | 1.36 | 320.8 | 153.7 (5) | 1.76 | 33% | – | 43 | 889,899 |
| Middle | Racing Games | 31 (7.6%) | 25 | 170.8 | 1.34 | 414.0 | 160.2 (27) | 1.62 | 29% | – | 125 | 1,237,038 |
| Middle | Driving Games | 28 (6.9%) | 23 | 165.4 | 1.30 | 377.9 | 160.2 (25) | 1.60 | 29% | – | 114 | 1,272,973 |
| Middle | Number Games | 15 (3.7%) | 13 | 159.4 | 1.25 | 595.0 | 159.4 (15) | 1.00 | 33% | – | 38 | 207,396 |
| Middle | Car Games | 31 (7.6%) | 29 | 157.7 | 1.24 | 360.3 | 155.9 (27) | 1.45 | 26% | – | 128 | 1,014,473 |
| Middle | Action Games | 97 (23.8%) | 64 | 153.7 | 1.21 | 437.4 | 153.7 (73) | 1.25 | 31% | – | 322 | 965,983 |
| Middle | Simulation Games | 93 (22.8%) | 61 | 136.7 | 1.07 | 370.4 | 123.4 (81) | 1.02 | 27% | – | 263 | 479,108 |
| Middle | Brainrot Games | 17 (4.2%) | 14 | 136.5 | 1.07 | 407.8 | 136.5 (17) | 1.30 | 29% | – | 27 | 549,987 |
| Middle | Drawing Games | 13 (3.2%) | 11 | 135.0 | 1.06 | 688.0 | 127.8 (10) | 1.22 | 38% | – | 35 | 289,106 |
| Middle | Decoration Games | 16 (3.9%) | 13 | 131.7 | 1.03 | 303.0 | 128.3 (15) | 1.08 | 25% | – | 35 | 366,359 |
| Middle | Monster Games | 10 (2.5%) | 10 | 131.5 | 1.03 | 545.4 | 47.7 (7) | 1.01 | 30% | – | 23 | 157,535 |
| Middle | Skill Games | 80 (19.6%) | 65 | 128.6 | 1.01 | 472.1 | 128.9 (69) | 1.00 | 30% | – | 410 | 766,251 |
| Middle | Make Up Games | 6 (1.5%) | 6 | 126.5 | 0.99 | 249.5 | 100.6 (5) | 0.97 | 17% | – | 16 | 685,219 |
| Middle | Adventure Games | 61 (15.0%) | 45 | 120.5 | 0.95 | 233.5 | 114.5 (48) | 0.95 | 20% | – | 234 | 834,218 |
| Middle | Board Games | 6 (1.5%) | 3 | 118.7 | 0.93 | 156.8 | 88.4 (5) | 1.16 | 0% | – | 57 | 214,400 |
| Middle | Mouse Games | 70 (17.2%) | 50 | 113.8 | 0.89 | 458.6 | 104.0 (60) | 0.91 | 30% | – | 317 | 673,498 |
| Middle | Co-op Games | 5 (1.2%) | 3 | 113.8 | 0.89 | 260.5 | 113.8 (5) | 1.05 | 0% | – | 32 | 1,443,022 |
| Middle | Cooking Games | 6 (1.5%) | 5 | 107.9 | 0.85 | 262.2 | 80.8 (5) | 0.82 | 17% | – | 30 | 443,323 |
| Middle | Platform Games | 43 (10.5%) | 36 | 103.3 | 0.81 | 266.6 | 113.8 (37) | 0.84 | 19% | – | 211 | 534,900 |
| Thin & weak | Construction Games | 8 (2.0%) | 7 | 97.7 | 0.77 | 173.3 | 97.7 (8) | 0.66 | 0% | – | 19 | 479,647 |
| Thin & weak | Farm Games | 7 (1.7%) | 7 | 94.9 | 0.74 | 333.4 | 94.9 (7) | 0.87 | 29% | – | 25 | 382,747 |
| Thin & weak | Strategy Games | 15 (3.7%) | 12 | 88.4 | 0.69 | 161.5 | 80.5 (14) | 0.64 | 7% | – | 65 | 381,599 |
| Thin & weak | Cat Games | 11 (2.7%) | 9 | 88.3 | 0.69 | 287.1 | 70.6 (10) | 0.58 | 27% | – | 32 | 318,447 |
| Thin & weak | Slime Games | 7 (1.7%) | 5 | 84.6 | 0.66 | 293.8 | 84.6 (7) | 0.51 | 14% | – | 15 | 220,849 |
| Thin & weak | Watermelon Games | 5 (1.2%) | 5 | 77.9 | 0.61 | 85.1 | 77.9 (5) | 0.56 | 20% | – | 18 | 390,035 |
| Thin & weak | Easy Games | 13 (3.2%) | 13 | 76.6 | 0.60 | 600.8 | 66.7 (11) | 0.67 | 38% | – | 81 | 520,974 |
| Thin & weak | Restaurant Games | 10 (2.5%) | 10 | 76.3 | 0.60 | 262.6 | 71.8 (9) | 0.63 | 20% | – | 41 | 411,100 |
| Thin & weak | Clicker Games | 15 (3.7%) | 14 | 74.8 | 0.59 | 242.8 | 70.7 (14) | 0.69 | 20% | – | 38 | 428,539 |
| Thin & weak | Tower Defense Games | 7 (1.7%) | 7 | 72.6 | 0.57 | 107.2 | 51.3 (6) | 0.44 | 14% | – | 29 | 379,697 |
| Thin & weak | Food Games | 16 (3.9%) | 14 | 71.5 | 0.56 | 178.6 | 65.1 (15) | 0.62 | 19% | – | 82 | 577,609 |
| Thin & weak | Tycoon Games | 17 (4.2%) | 14 | 64.7 | 0.51 | 195.7 | 33.3 (12) | 0.65 | 18% | – | 62 | 430,141 |
| Thin & weak | Survival Games | 12 (2.9%) | 11 | 58.3 | 0.46 | 104.4 | 58.3 (12) | 0.57 | 0% | – | 41 | 1,450,028 |
| Thin & weak | Zombie Games | 11 (2.7%) | 11 | 58.3 | 0.46 | 482.7 | 58.3 (9) | 0.59 | 36% | – | 31 | 631,046 |
| Thin & weak | Bubble Shooter Games | 5 (1.2%) | 5 | 57.3 | 0.45 | 65.5 | 57.3 (5) | 0.40 | 0% | – | 20 | 226,304 |
| Thin & weak | Dinosaur Games | 9 (2.2%) | 7 | 51.5 | 0.40 | 298.1 | 51.5 (9) | 0.52 | 22% | – | 18 | 1,364,433 |
| Thin & weak | Block Games | 16 (3.9%) | 13 | 49.1 | 0.39 | 205.4 | 45.1 (14) | 0.36 | 6% | – | 62 | 543,409 |
| Thin & weak | Difficult Games | 6 (1.5%) | 5 | 47.0 | 0.37 | 1,923.2 | 47.0 (6) | 0.43 | 33% | – | 120 | 2,099,109 |
| Thin & weak | Hidden Object Games | 7 (1.7%) | 7 | 46.3 | 0.36 | 258.2 | 46.3 (5) | 0.47 | 29% | – | 35 | 309,913 |
| Thin & weak | Retro Games | 16 (3.9%) | 10 | 36.2 | 0.28 | 48.7 | 42.4 (8) | 0.27 | 6% | – | 74 | 455,712 |
| Thin & weak | Match 3 Games | 5 (1.2%) | 3 | 11.3 | 0.09 | 50.7 | – (3) | 0.10 | 0% | – | 21 | 83,848 |
| Saturated | Idle Games | 57 (14.0%) | 49 | 80.1 | 0.63 | 261.6 | 77.5 (52) | 0.69 | 18% | – | 130 | 359,404 |
| Saturated | Brain Games | 75 (18.4%) | 49 | 66.1 | 0.52 | 175.6 | 65.1 (57) | 0.58 | 16% | – | 340 | 340,709 |
| Saturated | Arcade Games | 22 (5.4%) | 21 | 61.7 | 0.48 | 215.4 | 61.7 (18) | 0.46 | 14% | – | 219 | 698,699 |
| Saturated | Animal Games | 48 (11.8%) | 34 | 60.8 | 0.48 | 197.2 | 57.2 (47) | 0.53 | 17% | – | 165 | 428,003 |
| Saturated | Puzzle Games | 85 (20.8%) | 53 | 57.3 | 0.45 | 157.7 | 52.9 (67) | 0.43 | 12% | – | 355 | 313,708 |
| Saturated | Merge Games | 41 (10.0%) | 32 | 27.2 | 0.21 | 85.1 | 27.2 (39) | 0.23 | 7% | – | 82 | 318,171 |
| Saturated | Matching Games | 25 (6.1%) | 21 | 25.2 | 0.20 | 85.1 | 21.9 (22) | 0.19 | 4% | – | 76 | 179,104 |

Same rule applied to **primary genres** (n recent ≥ 5):

| Quadrant | Primary genre | n recent (share) | distinct devs | median votes/day | demand index | clean median (n) | age-adj idx | share in recent top quartile | Robust |
|---|---|---|---|---|---|---|---|---|---|
| Under-supplied | Fighting Games | 6 (1.5%) | 5 | 224.6 | 1.76 | – (4) | 1.36 | 33% | – |
| Under-supplied | Racing Games | 15 (3.7%) | 13 | 198.4 | 1.56 | 157.0 (12) | 1.66 | 27% | – |
| Crowded but rewarding | Shooting Games | 20 (4.9%) | 19 | 357.1 | 2.80 | 193.6 (15) | 3.07 | 50% | ✔ |
| Crowded but rewarding | Sports Games | 21 (5.1%) | 16 | 274.3 | 2.15 | 325.4 (18) | 2.55 | 48% | ✔ |
| Crowded but rewarding | Beauty Games | 24 (5.9%) | 15 | 221.2 | 1.74 | 228.7 (23) | 1.55 | 38% | ✔ |
| Middle | Driving Games | 20 (4.9%) | 17 | 158.1 | 1.24 | 158.1 (18) | 1.36 | 25% | – |
| Middle | Board Games | 5 (1.2%) | 3 | 148.9 | 1.17 | – (4) | 1.51 | 0% | – |
| Middle | Decoration Games | 12 (2.9%) | 9 | 145.4 | 1.14 | 135.0 (11) | 1.12 | 25% | – |
| Middle | Adventure Games | 17 (4.2%) | 17 | 136.5 | 1.07 | 136.5 (13) | 0.82 | 24% | – |
| Middle | Simulation Games | 71 (17.4%) | 46 | 135.7 | 1.06 | 115.9 (62) | 1.02 | 28% | – |
| Middle | Action Games | 28 (6.9%) | 25 | 135.6 | 1.06 | 135.6 (24) | 0.94 | 25% | – |
| Middle | Escape Games | 6 (1.5%) | 4 | 135.4 | 1.06 | – (3) | 1.06 | 33% | – |
| Middle | Platform Games | 21 (5.1%) | 17 | 128.4 | 1.01 | 137.0 (17) | 1.05 | 14% | – |
| Middle | Skill Games | 39 (9.6%) | 32 | 107.6 | 0.84 | 107.6 (35) | 0.72 | 31% | – |
| Thin & weak | Strategy Games | 5 (1.2%) | 5 | 94.5 | 0.74 | 94.5 (5) | 0.64 | 0% | – |
| Thin & weak | Idle Games | 17 (4.2%) | 16 | 64.7 | 0.51 | 60.9 (16) | 0.64 | 12% | – |
| Thin & weak | Arcade Games | 8 (2.0%) | 7 | 29.9 | 0.23 | 34.9 (5) | 0.29 | 12% | – |
| Saturated | Brain Games | 27 (6.6%) | 19 | 78.1 | 0.61 | 77.3 (22) | 0.67 | 15% | – |
| Saturated | Puzzle Games | 45 (11.0%) | 34 | 33.1 | 0.26 | 31.3 (35) | 0.31 | 9% | – |

**Robust high-demand categories** (✔, any supply level): Soccer Games (n=11, clean median 819, 9 devs, quadrant: Under-supplied); Crazy Games (n=10, clean median 779, 5 devs, quadrant: Under-supplied); .io Games (n=9, clean median 625, 7 devs, quadrant: Under-supplied); Parkour Games (n=5, clean median 437, 5 devs, quadrant: Under-supplied); Obby Games (n=11, clean median 428, 10 devs, quadrant: Under-supplied); Stickman Games (n=13, clean median 400, 12 devs, quadrant: Under-supplied); Sports Games (n=22, clean median 377, 17 devs, quadrant: Crowded but rewarding); Horror Games (n=8, clean median 355, 7 devs, quadrant: Under-supplied); Fashion Games (n=15, clean median 355, 10 devs, quadrant: Under-supplied); Ragdoll Games (n=14, clean median 298, 13 devs, quadrant: Under-supplied); Ball Games (n=16, clean median 282, 16 devs, quadrant: Under-supplied); Basketball Games (n=5, clean median 274, 4 devs, quadrant: Under-supplied); Running Games (n=11, clean median 266, 9 devs, quadrant: Under-supplied); 2 Player Games (n=23, clean median 263, 19 devs, quadrant: Crowded but rewarding); Escape Games (n=11, clean median 241, 7 devs, quadrant: Middle); Games for Girls (n=46, clean median 229, 25 devs, quadrant: Crowded but rewarding); Dress Up Games (n=28, clean median 229, 16 devs, quadrant: Crowded but rewarding); Beauty Games (n=28, clean median 229, 16 devs, quadrant: Crowded but rewarding); Bike Games (n=5, clean median 227, 5 devs, quadrant: Under-supplied); Games for Boys (n=45, clean median 211, 32 devs, quadrant: Crowded but rewarding); 3D Games (n=111, clean median 196, 63 devs, quadrant: Crowded but rewarding). [dataset]

**Under-supplied on the raw median but NOT robust** (signal driven by brands/⚑ games, few devs, or n<5 after cleaning): First Person Shooter Games (raw 494 → clean –, n clean=4, 5 devs); Gun Games (raw 309 → clean 48.3, n clean=11, 15 devs); Cozy Games (raw 255 → clean 104.8, n clean=11, 13 devs); Fighting Games (raw 215 → clean 222.0, n clean=9, 10 devs); Meme Games (raw 211 → clean 196.8, n clean=8, 8 devs); Airplane Games (raw 194 → clean –, n clean=4, 5 devs). [dataset]

## 3. Cohort comparison: top 50 recent (by votes/day) vs top 50 all-time (by total votes)

Top-50 recent = highest votes/day among 408 games released ≥ 2025-01-01 (threshold: 759.2 votes/day). Top-50 all-time = highest total votes among all 1,503 (threshold: 1,421,178 votes). [dataset]

Release years of the all-time top 50: 2020: 8, 2021: 6, 2022: 4, 2023: 4, 2024: 3, 2025: 1, ≤2019 (incl. migration): 24 [dataset]. The all-time list is therefore mostly a picture of what won 2019–2024.

### 3a. Primary genre

| Primary genre | top-50 all-time | top-50 recent | change (pp of 50) | share of all recent releases (n=408) | over-/under-representation in recent top 50 (top-50 share ÷ release share) |
|---|---|---|---|---|---|
| Beauty Games | 0 | 5 | +10 | 5.9% | 1.70× |
| Simulation Games | 4 | 8 | +8 | 17.4% | 0.92× |
| Sports Games | 5 | 7 | +4 | 5.1% | 2.72× |
| Decoration Games | 0 | 2 | +4 | 2.9% | 1.36× |
| Puzzle Games | 0 | 1 | +2 | 11.0% | 0.18× |
| Action Games | 3 | 4 | +2 | 6.9% | 1.17× |
| Adventure Games | 1 | 2 | +2 | 4.2% | 0.96× |
| Platform Games | 2 | 2 | +0 | 5.1% | 0.78× |
| Fighting Games | 1 | 1 | +0 | 1.5% | 1.36× |
| Brain Games | 3 | 2 | -2 | 6.6% | 0.60× |
| Arcade Games | 2 | 1 | -2 | 2.0% | 1.02× |
| Escape Games | 1 | 0 | -2 | 1.5% | 0.00× |
| Racing Games | 4 | 2 | -4 | 3.7% | 1.09× |
| Skill Games | 11 | 9 | -4 | 9.6% | 1.88× |
| Board Games | 2 | 0 | -4 | 1.2% | 0.00× |
| Battle Royale Games | 2 | 0 | -4 | 0.0% | – |
| Shooting Games | 4 | 2 | -4 | 4.9% | 0.82× |
| Driving Games | 5 | 2 | -6 | 4.9% | 0.82× |

### 3b. Categories (shown if present ≥ 4 times across the two lists)

| Category | top-50 all-time | top-50 recent | change (pp of 50) | share of all recent releases (n=408) | over-/under-representation in recent top 50 (top-50 share ÷ release share) |
|---|---|---|---|---|---|
| New Games † | 0 | 22 | +44 | 30.4% | 1.45× |
| Mobile Games † | 12 | 33 | +42 | 16.4% | 4.02× |
| Popular Games † | 17 | 37 | +40 | 15.2% | 4.87× |
| 3D Games | 16 | 24 | +16 | 27.2% | 1.76× |
| Simulation Games | 5 | 11 | +12 | 22.8% | 0.97× |
| Dress Up Games | 0 | 5 | +10 | 6.9% | 1.46× |
| Beauty Games | 0 | 5 | +10 | 6.9% | 1.46× |
| Fashion Games | 0 | 4 | +8 | 3.7% | 2.18× |
| Ragdoll Games | 1 | 4 | +6 | 3.4% | 2.33× |
| Games for Girls | 8 | 10 | +4 | 11.3% | 1.77× |
| Puzzle Games | 4 | 5 | +2 | 20.8% | 0.48× |
| Ball Games | 2 | 3 | +2 | 3.9% | 1.53× |
| World Cup Games | 2 | 3 | +2 | 1.0% | 6.12× |
| Soccer Games | 4 | 5 | +2 | 2.7% | 3.71× |
| Idle Games | 4 | 3 | -2 | 14.0% | 0.43× |
| Shooting Games | 4 | 3 | -2 | 6.9% | 0.87× |
| Brain Games | 8 | 7 | -2 | 18.4% | 0.76× |
| Sports Games | 8 | 7 | -2 | 5.4% | 2.60× |
| Fighting Games | 3 | 2 | -2 | 2.7% | 1.48× |
| Platform Games | 6 | 4 | -4 | 10.5% | 0.76× |
| Stickman Games | 6 | 4 | -4 | 3.2% | 2.51× |
| .io Games | 7 | 5 | -4 | 2.2% | 4.53× |
| Block Games | 3 | 1 | -4 | 3.9% | 0.51× |
| Cozy Games | 3 | 1 | -4 | 3.2% | 0.63× |
| Skill Games | 21 | 18 | -6 | 19.6% | 1.84× |
| Car Games | 8 | 5 | -6 | 7.6% | 1.32× |
| Running Games | 8 | 5 | -6 | 2.7% | 3.71× |
| Parkour Games | 4 | 1 | -6 | 1.2% | 1.63× |
| Escape Games | 4 | 1 | -6 | 2.7% | 0.74× |
| Mouse Games | 14 | 11 | -6 | 17.2% | 1.28× |
| Gun Games | 5 | 2 | -6 | 3.9% | 1.02× |
| Obby Games | 6 | 3 | -6 | 2.7% | 2.23× |
| Retro Games | 4 | 0 | -8 | 3.9% | 0.00× |
| Animal Games | 6 | 2 | -8 | 11.8% | 0.34× |
| Co-op Games | 4 | 0 | -8 | 1.2% | 0.00× |
| Driving Games | 9 | 4 | -10 | 6.9% | 1.17× |
| Survival Games | 5 | 0 | -10 | 2.9% | 0.00× |
| Flash Games † | 5 | 0 | -10 | 0.5% | 0.00× |
| Action Games | 18 | 13 | -10 | 23.8% | 1.09× |
| Crazy Games | 11 | 5 | -12 | 2.5% | 4.08× |
| Racing Games | 10 | 3 | -14 | 7.6% | 0.79× |
| Adventure Games | 14 | 5 | -18 | 15.0% | 0.67× |
| Multiplayer Games | 16 | 6 | -20 | 10.0% | 1.19× |
| Arcade Games | 14 | 2 | -24 | 5.4% | 0.74× |
| 2 Player Games | 15 | 3 | -24 | 5.6% | 1.06× |
| 1v1 Games | 13 | 0 | -26 | 0.7% | 0.00× |
| Games for Boys | 32 | 14 | -36 | 11.0% | 2.54× |
| Difficult Games | 21 | 2 | -38 | 1.5% | 2.72× |

**Named trend shifts (all-time top 50 → recent top 50, counts out of 50):**

- **Rising:** 3D 16→24; Simulation 5→11; Dress Up 0→5; Fashion 0→4; Ragdoll 1→4; Games for Girls 8→10; Soccer 4→5 (categories); primary genres Beauty 0→5, Simulation 4→8, Sports 5→7, Decoration 0→2. [dataset]
- **Fading:** Difficult 21→2; 1v1 13→0; 2 Player 15→3; Arcade 14→2; Multiplayer 16→6; Adventure 14→5; Racing 10→3; Games for Boys 32→14; Survival 5→0 (categories); primary genres Driving 5→2, Racing 4→2, Battle Royale 2→0, Board 2→0. [dataset]
- Interpretation: the 2019–2024 winners were twitchy skill/arcade games (Stickman Hook, Moto X3M, Level Devil, Tunnel Rush), local 2-player/1v1 duels (Basketball Stars, Football Masters, 12 MiniBattles) and battle-royale/.io multiplayer. The 2025–26 winners skew to 3D, simulation ("control a character in a little world") loops, dress-up/fashion, ragdoll physics and football. Caveats: (1) the all-time list rewards age, so fading ≠ dead — Skill Games still supplies the most recent top-50 entries (9); (2) part of the "Difficult"/"1v1" drop is a tagging artifact — these tags sit on many older hits (even Subway Surfers and Monkey Mart carry "Difficult") but on only 6 and 3 recent releases respectively. [dataset] Inference: a 2D precision platformer or local 2-player duel competes against a large entrenched back-catalogue; a 3D simulation, dress-up or football concept competes mostly with other recent titles.

### 3c. The two lists

| # | Top-50 recent (votes/day) | developer | genre | released | votes | votes/day | # | Top-50 all-time (votes) | developer | genre | released | votes |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Hole.io | Voodoo | Arcade Games | 2026-09-07 | 133,232 | 6,056 | 1 | Subway Surfers | SYBO | Skill Games | 2019-02-25 | 21,396,026 |
| 2 | Blockpost ⚑ | Skullcap Studios | Shooting Games | 2025-07-17 | 1,853,339 | 4,222 | 2 | Murder | Studio Seufz | Skill Games | 2019-03-11 | 9,048,862 |
| 3 | Talking Tom Gold Run | Outfit7 | Skill Games | 2026-05-19 | 531,642 | 3,997 | 3 | Stickman Hook | Madbox | Skill Games | 2018-12-20 | 7,894,266 |
| 4 | Hide and Paint | OnRush Studio | Simulation Games | 2026-07-07 | 249,934 | 2,975 | 4 | Moto X3M | Madpuffers | Action Games | 2019-03-11 | 5,304,251 |
| 5 | Kick The Buddy | StoreRider | Shooting Games | 2026-08-12 | 124,994 | 2,639 | 5 | Level Devil | Unept | Skill Games | 2023-12-01 | 4,142,008 |
| 6 | Slice Master | PlayCalm | Skill Games | 2025-12-01 | 791,813 | 2,622 | 6 | Rocket Soccer Derby | No Pressure Studios | Sports Games | 2020-02-05 | 3,963,308 |
| 7 | Neon Challenge Legends | Jungle Tavern | Skill Games | 2026-02-06 | 598,541 | 2,547 | 7 | Drive Mad | Fancade | Driving Games | 2022-07-27 | 3,869,379 |
| 8 | Scary Teacher 3D | ZnK Games | Simulation Games | 2025-03-03 | 1,362,275 | 2,369 | 8 | Monkey Mart | TinyDobbins | Simulation Games | 2022-11-10 | 3,809,241 |
| 9 | Count Control Legends | Jungle Tavern | Skill Games | 2025-11-10 | 755,115 | 2,338 | 9 | Friday Night Funkin' | ninjamuffin99 | Skill Games | 2021-05-27 | 3,789,080 |
| 10 | Soccer REAL | splax.net | Sports Games | 2026-07-08 | 184,076 | 2,218 | 10 | Penalty Shooters 2 | 10x10games | Sports Games | 2019-03-11 | 3,600,851 |
| 11 | SnapStyle Dress Up | PlayCap | Beauty Games | 2025-06-10 | 951,542 | 1,999 | 11 | We Become What We Behold | Nicky Case | Simulation Games | 2021-07-23 | 3,286,550 |
| 12 | Backrooms Recovery | Sleepless Games | Adventure Games | 2026-08-27 | 55,914 | 1,724 | 12 | Escaping the Prison | PuffballsUnited | Escape Games | 2019-09-30 | 3,257,376 |
| 13 | Phone CASE DIY | WeLoPlay | Decoration Games | 2026-06-12 | 187,128 | 1,717 | 13 | Temple of Boom | Colin Lane Games AB | Action Games | 2019-03-11 | 2,882,921 |
| 14 | Tank Stars | StoreRider | Skill Games | 2026-02-10 | 390,180 | 1,689 | 14 | Temple Run 2 | Imangi Studios | Skill Games | 2020-10-02 | 2,874,562 |
| 15 | Plonky | Gametornado | Platform Games | 2025-07-01 | 766,030 | 1,684 | 15 | Brain Test: Tricky Puzzles | Unico Studio | Brain Games | 2020-06-04 | 2,659,211 |
| 16 | NSR Street Car Racing | Yes2Games | Racing Games | 2026-09-23 | 11,076 | 1,582 | 16 | Basketball Stars | Madpuffers | Sports Games | 2019-05-28 | 2,553,837 |
| 17 | World Soccer Champions | Finz Games | Sports Games | 2025-04-23 | 807,203 | 1,540 | 17 | City Car Driving: Stunt Master | BoneCracker Games | Driving Games | 2021-03-23 | 2,476,487 |
| 18 | Paper.io 2 ⚑ | Voodoo | Action Games | 2026-08-24 | 53,585 | 1,488 | 18 | Fleeing the Complex | PuffballsUnited | Brain Games | 2019-10-18 | 2,415,464 |
| 19 | Rail in the Air | OPlay Games | Driving Games | 2026-04-21 | 239,514 | 1,488 | 19 | Sushi Party | Terminarch Games | Battle Royale Games | 2019-11-21 | 2,372,364 |
| 20 | Planet Destruction | Boop Games | Simulation Games | 2025-12-31 | 400,699 | 1,473 | 20 | Venge.io | OnRush Studio | Shooting Games | 2020-06-12 | 2,319,969 |
| 21 | Slime Keyboard Escape | Blasters | Platform Games | 2026-08-12 | 69,849 | 1,455 | 21 | 3D Moto Simulator 2 | Faramel games | Driving Games | 2019-03-11 | 2,167,342 |
| 22 | Magic Battleground | vessel | Fighting Games | 2026-03-18 | 267,497 | 1,372 | 22 | Who Is? | Unico Studio | Brain Games | 2021-04-12 | 2,048,584 |
| 23 | Beauty Salon | WeLoPlay | Beauty Games | 2025-08-01 | 572,095 | 1,349 | 23 | Crossy Road | Hipster Whale | Skill Games | 2024-12-02 | 1,956,143 |
| 24 | Fashion Legends | Jungle Tavern | Beauty Games | 2026-02-27 | 275,409 | 1,287 | 24 | Master Chess | Codethislab | Board Games | 2019-03-11 | 1,949,441 |
| 25 | Stickman Battle | EasyCats | Action Games | 2025-11-24 | 397,584 | 1,287 | 25 | EvoWorld io (FlyOrDie io) | Pixel Voices | Skill Games | 2019-10-30 | 1,937,420 |
| 26 | Sprunki ⚑ | NyankoBfLol | Simulation Games | 2026-03-20 | 232,149 | 1,203 | 26 | G-Switch 3 | Serius Games | Skill Games | 2019-03-11 | 1,912,789 |
| 27 | Steal a Brainrot | emolingo games | Action Games | 2025-10-17 | 417,385 | 1,203 | 27 | Stick Merge | TinyDobbins | Shooting Games | 2021-01-29 | 1,895,384 |
| 28 | Drift Hunters ⚑ | BoneCracker Games | Racing Games | 2026-04-14 | 196,279 | 1,168 | 28 | Blockpost | Skullcap Studios | Shooting Games | 2025-07-17 | 1,853,339 |
| 29 | Merge Rot | TapMen | Brain Games | 2025-05-28 | 562,775 | 1,151 | 29 | Super Star Car | Barnzmu | Racing Games | 2021-07-26 | 1,829,555 |
| 30 | Decor Life | SayGames | Decoration Games | 2026-04-02 | 203,663 | 1,131 | 30 | My Perfect Hotel | SayGames | Simulation Games | 2024-06-18 | 1,807,264 |
| 31 | Car Circle | Shoom Games | Skill Games | 2026-06-19 | 114,077 | 1,118 | 31 | Stunt Bike Extreme | Hyperkani | Racing Games | 2024-08-19 | 1,761,913 |
| 32 | Super Dress | WeLoPlay | Beauty Games | 2026-08-26 | 37,792 | 1,112 | 32 | Bad Ice-Cream | Nitrome | Arcade Games | 2019-10-05 | 1,759,433 |
| 33 | Robo Cleaner Simulator | Camu | Simulation Games | 2026-09-02 | 29,845 | 1,105 | 33 | Iron Snout | SnoutUp Games | Skill Games | 2019-03-11 | 1,758,049 |
| 34 | Hill Climb Racing Lite ⚑ | Fingersoft | Driving Games | 2025-12-03 | 326,550 | 1,088 | 34 | Football Masters | Madpuffers | Sports Games | 2019-12-05 | 1,728,452 |
| 35 | Speed Stars ⚑ | Luke | Sports Games | 2026-02-06 | 233,781 | 995 | 35 | Snake.is MLG Edition | CrioDev | Battle Royale Games | 2019-12-11 | 1,724,048 |
| 36 | Happy Glass | Lion Studios | Brain Games | 2025-01-17 | 612,471 | 988 | 36 | Puppet Master | Freeze Nova | Shooting Games | 2019-08-26 | 1,713,584 |
| 37 | Perfect Shape | Sunday Monday | Skill Games | 2026-08-20 | 38,379 | 972 | 37 | 12 MiniBattles | Shared Dreams Studio | Action Games | 2019-03-11 | 1,704,842 |
| 38 | Ragdoll Chaos | OSA Studio | Action Games | 2026-09-01 | 26,167 | 959 | 38 | Parkour Race | Madbox | Skill Games | 2020-12-04 | 1,568,616 |
| 39 | Soccer Skills 2 World Cup | Radical Play | Sports Games | 2026-04-20 | 151,198 | 933 | 39 | Stickman Dragon Fight | PEGASUS | Fighting Games | 2023-11-15 | 1,558,361 |
| 40 | Soccer League | OnRush Studio | Sports Games | 2026-07-16 | 69,327 | 933 | 40 | Crazy Cars | No Pressure Studios | Driving Games | 2022-09-21 | 1,557,164 |
| 41 | Teleport Master | Fluffy | Puzzle Games | 2026-09-22 | 6,344 | 906 | 41 | Rainbow Obby | emolingo games | Platform Games | 2023-09-07 | 1,546,672 |
| 42 | Monkey Tag IO | Petit Kyanpu | Simulation Games | 2026-06-03 | 101,515 | 860 | 42 | Vectaria.io | Vectaria | Adventure Games | 2023-09-26 | 1,539,040 |
| 43 | Magikmon ⚑ | Ravalmatic | Adventure Games | 2026-01-12 | 214,075 | 825 | 43 | Dino Game | Chrome UX | Arcade Games | 2020-02-12 | 1,525,961 |
| 44 | Soccer 5 | Radical Play | Sports Games | 2026-06-26 | 77,786 | 819 | 44 | Smash Karts | Tall Team | Driving Games | 2020-04-29 | 1,509,997 |
| 45 | Dino Simulator | Story Giant Games | Simulation Games | 2026-07-27 | 52,384 | 818 | 45 | TicTacToe | Playtouch | Board Games | 2019-07-23 | 1,503,023 |
| 46 | Count War | Nineties Games | Skill Games | 2026-04-24 | 127,123 | 805 | 46 | Roller Coaster Builder 2 | Rabbit Mountain | Simulation Games | 2019-10-14 | 1,469,087 |
| 47 | Anime Dress Up | WeLoPlay | Beauty Games | 2025-01-31 | 478,897 | 790 | 47 | Duo Survival | 7Spot Games | Platform Games | 2020-09-23 | 1,450,028 |
| 48 | Harvest Simulator | Camu | Simulation Games | 2025-05-06 | 393,242 | 770 | 48 | Top Speed 3D | Faramel games | Racing Games | 2019-03-11 | 1,445,633 |
| 49 | Supercar Legends | Jungle Tavern | Skill Games | 2026-05-13 | 106,638 | 767 | 49 | Tunnel Rush | Deer Cat Games | Racing Games | 2019-03-11 | 1,423,234 |
| 50 | Basketball REAL | splax.net | Sports Games | 2026-05-20 | 100,214 | 759 | 50 | Soccer Skills World Cup | Radical Play | Sports Games | 2022-09-12 | 1,421,178 |

## 4. Big-brand / mobile-publisher ports vs web-first indies among the top 60 recent performers

Classification rule: **Big** = established mobile/PC brand, big mobile publisher, or a port of an established mobile IP; **Web-first/indie** = everything else (includes mid-sized web-first studios such as WeLoPlay, OnRush, Gametornado). Confidence "medium" = no positive evidence either way beyond the developer name/description (defaults to indie). ⚑ = re-release/long-soft-launch flag (§0).

| # | Game | Developer | Genre | Released | votes/day | Class | Conf. | Evidence |
|---|---|---|---|---|---|---|---|---|
| 1 | Hole.io | Voodoo | Arcade Games | 2026-09-07 | 6,056 | Big | high | Major French mobile hyper-casual publisher (Hole.io, Paper.io 2 are mobile hits). |
| 2 | Blockpost ⚑ | Skullcap Studios | Shooting Games | 2025-07-17 | 4,222 | Web-first/indie | high | Blockpost is a long-running browser FPS (⚑ release-date anomaly: id implies ~2021). |
| 3 | Talking Tom Gold Run | Outfit7 | Skill Games | 2026-05-19 | 3,997 | Big | high | Poki blog: "creator of the award winning Talking Tom & Friends brand"; game "has amassed over 3.2 billion downloads" (https://poki.com/blog/outfit7-hit-talking-tom-live-on-poki). |
| 4 | Hide and Paint | OnRush Studio | Simulation Games | 2026-07-07 | 2,975 | Web-first/indie | high | Web-first studio (Venge.io, Tribals.io); Poki spotlight https://poki.com/blog/meet-onrush-studio. |
| 5 | Kick The Buddy | StoreRider | Shooting Games | 2026-08-12 | 2,639 | Big | high | Porting company; Kick the Buddy and Tank Stars are established mobile IPs (Inference from titles). CEO quoted: "Porting a Unity game to web takes 1-to-2 hours" (https://poki.com/blog/state-of-web-gaming-report-2026). |
| 6 | Slice Master | PlayCalm | Skill Games | 2025-12-01 | 2,622 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 7 | Neon Challenge Legends | Jungle Tavern | Skill Games | 2026-02-06 | 2,547 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 8 | Scary Teacher 3D | ZnK Games | Simulation Games | 2025-03-03 | 2,369 | Big | high | Scary Teacher 3D is an established mobile franchise (Inference: widely known mobile hit; 14 games on Poki). |
| 9 | Count Control Legends | Jungle Tavern | Skill Games | 2025-11-10 | 2,338 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 10 | Soccer REAL | splax.net | Sports Games | 2026-07-08 | 2,218 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 11 | SnapStyle Dress Up | PlayCap | Beauty Games | 2025-06-10 | 1,999 | Web-first/indie | high | SnapStyle Dress Up named a 2025 "top performing" game (https://poki.com/blog/2025-at-poki-a-year-in-review); other Poki titles are web games. |
| 12 | Backrooms Recovery | Sleepless Games | Adventure Games | 2026-08-27 | 1,724 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 13 | Phone CASE DIY | WeLoPlay | Decoration Games | 2026-06-12 | 1,717 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 14 | Tank Stars | StoreRider | Skill Games | 2026-02-10 | 1,689 | Big | high | Porting company; Kick the Buddy and Tank Stars are established mobile IPs (Inference from titles). CEO quoted: "Porting a Unity game to web takes 1-to-2 hours" (https://poki.com/blog/state-of-web-gaming-report-2026). |
| 15 | Plonky | Gametornado | Platform Games | 2025-07-01 | 1,684 | Web-first/indie | high | Web-first; Plonky named a 2025 "top performing" game (https://poki.com/blog/2025-at-poki-a-year-in-review). |
| 16 | NSR Street Car Racing | Yes2Games | Racing Games | 2026-09-23 | 1,582 | Big | medium | Its only other Poki game is Dan The Man (a Halfbrick mobile IP) [dataset: developer_games]; Inference: mobile-IP porting/publishing partner. |
| 17 | World Soccer Champions | Finz Games | Sports Games | 2025-04-23 | 1,540 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 18 | Paper.io 2 ⚑ | Voodoo | Action Games | 2026-08-24 | 1,488 | Big | high | Major French mobile hyper-casual publisher (Hole.io, Paper.io 2 are mobile hits). |
| 19 | Rail in the Air | OPlay Games | Driving Games | 2026-04-21 | 1,488 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 20 | Planet Destruction | Boop Games | Simulation Games | 2025-12-31 | 1,473 | Web-first/indie | high | Planet Destruction listed as a Green Game Jam 2026 entry (https://poki.com/blog/green-game-jam-2026-is-over); "first game on Poki". |
| 21 | Slime Keyboard Escape | Blasters | Platform Games | 2026-08-12 | 1,455 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 22 | Magic Battleground | vessel | Fighting Games | 2026-03-18 | 1,372 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 23 | Beauty Salon | WeLoPlay | Beauty Games | 2025-08-01 | 1,349 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 24 | Fashion Legends | Jungle Tavern | Beauty Games | 2026-02-27 | 1,287 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 25 | Stickman Battle | EasyCats | Action Games | 2025-11-24 | 1,287 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 26 | Sprunki ⚑ | NyankoBfLol | Simulation Games | 2026-03-20 | 1,203 | Web-first/indie | high | Sprunki: fan-made viral music mod (trend IP, solo creator). |
| 27 | Steal a Brainrot | emolingo games | Action Games | 2025-10-17 | 1,203 | Web-first/indie | high | Web-first HTML5 studio (https://poki.com/blog/how-emolingo-games-built-business-html5-web-games-poki). |
| 28 | Drift Hunters ⚑ | BoneCracker Games | Racing Games | 2026-04-14 | 1,168 | Web-first/indie | high | Drift Hunters is a long-running browser game (⚑ id implies ~2019). |
| 29 | Merge Rot | TapMen | Brain Games | 2025-05-28 | 1,151 | Web-first/indie | high | Description: "Originally released under the name Merge Fellas" — a viral indie title, not a big-publisher brand. |
| 30 | Decor Life | SayGames | Decoration Games | 2026-04-02 | 1,131 | Big | high | Large mobile publisher (My Perfect Hotel etc.); cited in https://poki.com/blog/i-quit-my-job-to-make-a-dress-up-web-game-and-it-blew-up. |
| 31 | Car Circle | Shoom Games | Skill Games | 2026-06-19 | 1,118 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 32 | Super Dress | WeLoPlay | Beauty Games | 2026-08-26 | 1,112 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 33 | Robo Cleaner Simulator | Camu | Simulation Games | 2026-09-02 | 1,105 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 34 | Hill Climb Racing Lite ⚑ | Fingersoft | Driving Games | 2025-12-03 | 1,088 | Big | high | Description: "brings the iconic mobile experience to desktop browsers for the first time" [dataset: hill-climb-racing-lite description]; named among "iconic hits" in https://poki.com/blog/state-of-web-gaming-report-2026. |
| 35 | Speed Stars ⚑ | Luke | Sports Games | 2026-02-06 | 995 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 36 | Happy Glass | Lion Studios | Brain Games | 2025-01-17 | 988 | Big | high | Mobile hyper-casual publisher (Happy Glass, Mr Bullet, Love Balls are mobile hits). Inference from knowledge of the brand. |
| 37 | Perfect Shape | Sunday Monday | Skill Games | 2026-08-20 | 972 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 38 | Ragdoll Chaos | OSA Studio | Action Games | 2026-09-01 | 959 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 39 | Soccer Skills 2 World Cup | Radical Play | Sports Games | 2026-04-20 | 933 | Web-first/indie | high | Web studio quoted in https://poki.com/blog/state-of-web-gaming-report-2026 (Soccer Skills series). |
| 40 | Soccer League | OnRush Studio | Sports Games | 2026-07-16 | 933 | Web-first/indie | high | Web-first studio (Venge.io, Tribals.io); Poki spotlight https://poki.com/blog/meet-onrush-studio. |
| 41 | Teleport Master | Fluffy | Puzzle Games | 2026-09-22 | 906 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 42 | Monkey Tag IO | Petit Kyanpu | Simulation Games | 2026-06-03 | 860 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 43 | Magikmon ⚑ | Ravalmatic | Adventure Games | 2026-01-12 | 825 | Web-first/indie | high | Magikmon is an older browser game (⚑ id implies ~2019). |
| 44 | Soccer 5 | Radical Play | Sports Games | 2026-06-26 | 819 | Web-first/indie | high | Web studio quoted in https://poki.com/blog/state-of-web-gaming-report-2026 (Soccer Skills series). |
| 45 | Dino Simulator | Story Giant Games | Simulation Games | 2026-07-27 | 818 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 46 | Count War | Nineties Games | Skill Games | 2026-04-24 | 805 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 47 | Anime Dress Up | WeLoPlay | Beauty Games | 2025-01-31 | 790 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 48 | Harvest Simulator | Camu | Simulation Games | 2025-05-06 | 770 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 49 | Supercar Legends | Jungle Tavern | Skill Games | 2026-05-13 | 767 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 50 | Basketball REAL | splax.net | Sports Games | 2026-05-20 | 759 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 51 | Catch a Pet | Kimchi Soup Studios | Simulation Games | 2026-09-17 | 751 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 52 | Guns Guns Guns | CHEPERGame | Shooting Games | 2026-05-15 | 744 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 53 | Sword Legends | Fluffy | Adventure Games | 2026-09-15 | 708 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 54 | Marble Run 3D | OSA Studio | Racing Games | 2025-01-02 | 696 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 55 | Ant Art Tycoon ⚑ | Wix Games | Idle Games | 2025-07-24 | 688 | Web-first/indie | high | Ant Art Tycoon older browser game (⚑ id implies ~2019). |
| 56 | Cat Pizza | Cosmonautic Games | Simulation Games | 2025-02-10 | 682 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 57 | 67 Game | stupidella | Brain Games | 2026-03-04 | 682 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 58 | Tear Blocks Down | AM-Games | Shooting Games | 2025-12-23 | 673 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 59 | Punchy Guy | Finz Games | Fighting Games | 2026-04-03 | 671 | Web-first/indie | medium | No evidence of an established mobile/PC brand or big publisher in the description or sources; developer-name inference. |
| 60 | Mr Bullet | Lion Studios | Shooting Games | 2025-02-17 | 662 | Big | high | Mobile hyper-casual publisher (Happy Glass, Mr Bullet, Love Balls are mobile hits). Inference from knowledge of the brand. |

**Result:** 49/60 (82%) of the top-60 recent performers are web-first/indie; 11/60 are big-brand/publisher ports. Big brands are concentrated at the very top: 4/10 of the top 10 and 7/20 of the top 20. [dataset + classification above]
Median votes/day within the top 60: big 1,582 (n=11) vs indie 1,105 (n=49). [dataset]

Robustness: re-ranking the top 60 after dropping ⚑ games gives 50/60 web-first/indie (83%) and 10/60 big (new entrants beyond #60 classified with the same rule: Battle Blast (No Pressure Studios: Web-first/indie), Blast Buddies (Blasters: Web-first/indie), Real City Bikes (Fuego! Games: Web-first/indie), You Monster! (Shoom Games: Web-first/indie), Ragdoll Drop (Ericetto: Web-first/indie), Mom's Diary Cooking Games (a1games: Web-first/indie), Tower Destiny Survive (SayGames: Big), Rumble Rush (PocketHaven: Web-first/indie)). [dataset]

Genres where indies win (top-60 recent, by primary genre):

| Primary genre | Indie in top 60 | Big in top 60 | Indie titles |
|---|---|---|---|
| Simulation Games | 9 | 1 | Hide and Paint, Planet Destruction, Sprunki, Robo Cleaner Simulator, Monkey Tag IO, Dino Simulator, Harvest Simulator, Catch a Pet, Cat Pizza |
| Sports Games | 7 | 0 | Soccer REAL, World Soccer Champions, Speed Stars, Soccer Skills 2 World Cup, Soccer League, Soccer 5, Basketball REAL |
| Skill Games | 7 | 2 | Slice Master, Neon Challenge Legends, Count Control Legends, Car Circle, Perfect Shape, Count War, Supercar Legends |
| Beauty Games | 5 | 0 | SnapStyle Dress Up, Beauty Salon, Fashion Legends, Super Dress, Anime Dress Up |
| Shooting Games | 3 | 2 | Blockpost, Guns Guns Guns, Tear Blocks Down |
| Action Games | 3 | 1 | Stickman Battle, Steal a Brainrot, Ragdoll Chaos |
| Adventure Games | 3 | 0 | Backrooms Recovery, Magikmon, Sword Legends |
| Racing Games | 2 | 1 | Drift Hunters, Marble Run 3D |
| Brain Games | 2 | 1 | Merge Rot, 67 Game |
| Platform Games | 2 | 0 | Plonky, Slime Keyboard Escape |
| Fighting Games | 2 | 0 | Magic Battleground, Punchy Guy |
| Decoration Games | 1 | 1 | Phone CASE DIY |
| Driving Games | 1 | 1 | Rail in the Air |
| Puzzle Games | 1 | 0 | Teleport Master |
| Idle Games | 1 | 0 | Ant Art Tycoon |
| Arcade Games | 0 | 1 |  |

Most common (non-editorial) categories among the indie top-60 entries: 3D Games 22, Skill Games 15, Action Games 13, Simulation Games 13, Mouse Games 13, Games for Boys 11, Games for Girls 10, Multiplayer Games 7, Sports Games 7, Brain Games 6, Crazy Games 5, Adventure Games 5, Running Games 5, Soccer Games 5. Among big-brand entries: 3D Games 4, Games for Boys 4, Action Games 4, Skill Games 3, .io Games 2, Shooting Games 2, Puzzle Games 2, Mouse Games 2. [dataset]

Whole recent cohort: 47 of 408 recent releases are from the big-brand list; their median votes/day is 181.0 vs 118.8 for everyone else (n=361). [dataset] Inference: a brand buys a higher floor, but most of the top-60 slots are still won by web-first teams.

## 5. Today's desktop homepage (poki.com/en)

Homepage has 145 game slots [dataset: homepage.json desktop_home]. Release years — top 60: 2020: 2, 2021: 1, 2022: 2, 2023: 3, 2024: 15, 2025: 14, 2026: 16, ≤2019: 7; all 145: 2020: 4, 2021: 6, 2022: 5, 2023: 8, 2024: 22, 2025: 32, 2026: 54, ≤2019: 14.
**30/60 of the top-60 homepage positions and 86/145 of all homepage slots are 2025–2026 releases** (8/12 of the first 12). For comparison, 2025–26 releases are 408/1,503 = 27% of the catalogue. [dataset]

### 5a. Primary genre on homepage top 60 vs catalogue

| Primary genre | homepage top 60 | share | catalogue share (1,503) | lift |
|---|---|---|---|---|
| Skill Games | 14 | 23% | 12.0% | 1.95× |
| Simulation Games | 6 | 10% | 11.8% | 0.84× |
| Shooting Games | 5 | 8% | 4.9% | 1.72× |
| Sports Games | 5 | 8% | 6.5% | 1.29× |
| Beauty Games | 4 | 7% | 3.5% | 1.89× |
| Brain Games | 4 | 7% | 6.6% | 1.01× |
| Platform Games | 4 | 7% | 8.6% | 0.78× |
| Driving Games | 3 | 5% | 4.1% | 1.21× |
| Arcade Games | 3 | 5% | 5.5% | 0.92× |
| Racing Games | 3 | 5% | 4.7% | 1.07× |
| Action Games | 3 | 5% | 3.5% | 1.42× |
| Puzzle Games | 2 | 3% | 11.7% | 0.28× |
| Fighting Games | 2 | 3% | 1.9% | 1.73× |
| Escape Games | 1 | 2% | 0.7% | 2.28× |
| Board Games | 1 | 2% | 1.7% | 0.96× |

### 5b. Categories on homepage top 60 (≥ 6 games) vs catalogue

| Category | homepage top 60 | share | catalogue share | lift |
|---|---|---|---|---|
| Popular Games † | 36 | 60% | 6.6% | 9.11× |
| Mobile Games † | 31 | 52% | 6.5% | 7.92× |
| Skill Games | 26 | 43% | 27.3% | 1.59× |
| Games for Boys | 19 | 32% | 18.1% | 1.75× |
| 3D Games | 19 | 32% | 18.4% | 1.72× |
| Mouse Games | 18 | 30% | 21.1% | 1.42× |
| Difficult Games | 17 | 28% | 8.0% | 3.55× |
| Action Games | 17 | 28% | 21.4% | 1.32× |
| Brain Games | 15 | 25% | 22.6% | 1.11× |
| Games for Girls | 15 | 25% | 12.0% | 2.08× |
| Multiplayer Games | 14 | 23% | 10.1% | 2.31× |
| New Games † | 12 | 20% | 8.7% | 2.29× |
| Platform Games | 10 | 17% | 14.0% | 1.19× |
| Puzzle Games | 10 | 17% | 23.6% | 0.71× |
| Arcade Games | 9 | 15% | 14.6% | 1.03× |
| Car Games | 9 | 15% | 8.5% | 1.76× |
| Racing Games | 8 | 13% | 8.3% | 1.60× |
| Obby Games | 8 | 13% | 2.4% | 5.57× |
| Simulation Games | 8 | 13% | 17.5% | 0.76× |
| 2 Player Games | 8 | 13% | 9.0% | 1.47× |
| Adventure Games | 8 | 13% | 15.6% | 0.86× |
| Crazy Games | 7 | 12% | 4.5% | 2.62× |
| Running Games | 7 | 12% | 3.1% | 3.73× |
| Driving Games | 6 | 10% | 7.6% | 1.32× |
| Shooting Games | 6 | 10% | 6.9% | 1.45× |
| Ball Games | 6 | 10% | 6.2% | 1.62× |
| Sports Games | 6 | 10% | 9.8% | 1.02× |

### 5c. Homepage top 24 positions

| Pos | Game | Developer | Genre | Released | votes | votes/day |
|---|---|---|---|---|---|---|
| 1 | Drive Mad | Fancade | Driving Games | 2022-07-27 | 3,869,379 | 2,537 |
| 2 | Robo Cleaner Simulator | Camu | Simulation Games | 2026-09-02 | 29,845 | 1,105 |
| 3 | Kick The Buddy | StoreRider | Shooting Games | 2026-08-12 | 124,994 | 2,639 |
| 4 | Level Devil | Unept | Skill Games | 2023-12-01 | 4,142,008 | 4,010 |
| 5 | Slice Master | PlayCalm | Skill Games | 2025-12-01 | 791,813 | 2,622 |
| 6 | Beauty Salon | WeLoPlay | Beauty Games | 2025-08-01 | 572,095 | 1,349 |
| 7 | Count Control Legends | Jungle Tavern | Skill Games | 2025-11-10 | 755,115 | 2,338 |
| 8 | Subway Surfers | SYBO | Skill Games | 2019-02-25 | 21,396,026 | 7,716 |
| 9 | Car Circle | Shoom Games | Skill Games | 2026-06-19 | 114,077 | 1,118 |
| 10 | Perfect Landing, Plane Pilot | GeniGames | Skill Games | 2025-06-05 | 149,194 | 310 |
| 11 | Super Dress | WeLoPlay | Beauty Games | 2026-08-26 | 37,792 | 1,112 |
| 12 | My Perfect Hotel | SayGames | Simulation Games | 2024-06-18 | 1,807,264 | 2,170 |
| 13 | Planet Destruction | Boop Games | Simulation Games | 2025-12-31 | 400,699 | 1,473 |
| 14 | Goods Master | Tuki Tuki Games | Puzzle Games | 2026-08-19 | 6,435 | 159 |
| 15 | Blumgi Bounce | Blumgi | Skill Games | 2025-12-02 | 84,748 | 282 |
| 16 | Brain Test: Tricky Puzzles | Unico Studio | Brain Games | 2020-06-04 | 2,659,211 | 1,152 |
| 17 | Kawaii Fruits 3D | Okashi Games | Skill Games | 2024-01-29 | 72,466 | 74 |
| 18 | Blumgi Slime | Blumgi | Arcade Games | 2023-02-16 | 1,032,676 | 782 |
| 19 | Under the Red Sky | Dedra Games × Federico | Platform Games | 2024-11-25 | 481,813 | 716 |
| 20 | Nuts and Bolts: Screwing Puzzle | Unico Studio | Brain Games | 2024-08-26 | 168,952 | 221 |
| 21 | Supercar Legends | Jungle Tavern | Skill Games | 2026-05-13 | 106,638 | 767 |
| 22 | Stickman Hook | Madbox | Skill Games | 2018-12-20 | 7,894,266 | 2,780 |
| 23 | Vortella's Dress Up | Devortel | Beauty Games | 2024-12-13 | 1,239,199 | 1,892 |
| 24 | Brain Test 2: Tricky Stories | Unico Studio | Brain Games | 2021-07-26 | 677,988 | 359 |

Interpretation: the homepage is the demand signal Poki's promotion system produces. 30/60 top slots go to 2025–26 releases even though they are 27% of the catalogue, and among recent homepage games higher votes/day sits higher (Spearman below), consistent with the docs' statement that "the promotion system will automatically show your game on any of our localized homepages" depending on performance (https://developers.poki.com/guide/release-process). Skill is the top homepage genre (14/60, lift 1.95×); by category the biggest over-representations are Obby (8/60, 5.6×), Running (7, 3.7×), Difficult (17, 3.5×, mostly older evergreen hits), Crazy (7), Multiplayer (14) and Games for Girls (15); Puzzle genre is strongly under-represented (2/60, lift 0.28×). [dataset]

Spearman(homepage position, votes/day) among the 86 homepage games released ≥2025: -0.53 (negative = higher-traction games sit higher). [dataset]

Desktop "popular searches" today: subway-surfers (Skill Games, ≤2019), master-chess (Board Games, ≤2019), minefun-io (Action Games, 2024), tag (Skill Games, 2023), cryzen-io (Shooting Games, 2024), scary-teacher-3d (Simulation Games, 2025), steal-a-brainrot (Action Games, 2025), level-devil (Skill Games, 2023), basketball-stars (Sports Games, ≤2019), hole-io (Arcade Games, 2026), stickman-battle (Action Games, 2025), slime-keyboard-escape (Platform Games, 2026). [dataset: homepage.json]

## 6. Rating vs traction

- Recent games (n=408): Spearman(rating, votes/day) = **0.27**; Pearson(rating, log votes/day) = 0.27. [dataset]
  - age band 0–30 days (n=25): Spearman = 0.45
  - age band 30–90 days (n=53): Spearman = 0.13
  - age band 90–180 days (n=59): Spearman = 0.27
  - age band 180–365 days (n=118): Spearman = 0.23
  - age band 365–∞ days (n=153): Spearman = 0.35
- All games with a release date (n=1471): Spearman(rating, total votes) = 0.32. [dataset]
- Median rating: recent top 60 = 4.40 vs rest of recent cohort = 4.30 (n=348). Min rating in recent top 60 = 3.71. [dataset]
- Note: `rating` is not simply 5×up/(up+down) (e.g. jetpack-speed-obby: rating 4.37 vs 5×up-share 4.21); it appears smoothed. Inference: it behaves like a quality score with a narrow range, so it cannot discriminate well among survivors.

Rating distribution:

| Rating | all games (n=1,503) | recent (n=408) | recent median votes/day | recent top-60 |
|---|---|---|---|---|
| < 3.5 | 7 (0%) | 1 | – (n<5) | 0 |
| 3.5–3.8 | 45 (3%) | 5 | 52.0 | 1 |
| 3.8–4.0 | 96 (6%) | 22 | 54.4 | 0 |
| 4.0–4.2 | 288 (19%) | 77 | 65.5 | 5 |
| 4.2–4.4 | 601 (40%) | 180 | 146.6 | 23 |
| 4.4–4.6 | 427 (28%) | 111 | 216.4 | 30 |
| ≥ 4.6 | 39 (3%) | 12 | 127.8 | 1 |

All-game rating: median 4.31, p10 4.00, p90 4.51, min 3.12, max 5.00. Recent: median 4.32, p10 4.05, p90 4.50. [dataset]

Interpretation: rating is only weakly correlated with traction (Spearman 0.27), and ratings are compressed — 1028/1,503 games (68%) sit in 4.2–4.6. But 54/60 recent top performers rate ≥ 4.2 and recent games rated < 4.2 have median votes/day ≤ 65. [dataset] Inference: ~4.2+ behaves like a quality floor for hits rather than a predictor; the ≥4.6 bucket (n=12) has median votes/day 128 (≈ cohort median) and includes legacy/niche titles (Papa Louie 2/3), so very high ratings do not imply scale.

## 7. Debut success ("This is their first game on Poki")

Definition A (as instructed): description contains "This is their first game on Poki". Caveat: the sentence is static text; 144 flagged games have non-empty `developer_games` (the developer has since shipped more), and 54 unflagged games have empty `developer_games`. Definition B (robustness): the game is the earliest-released title of its developer in the dataset. [dataset]

| Group (recent, ≥2025) | n | median votes/day | p75 votes/day | age-adj idx | share in recent top quartile | in recent top 60 |
|---|---|---|---|---|---|---|
| A: debut flag | 96 | 119.7 | 292.2 | 1.06 | 23% | 9 |
| A: not flagged | 312 | 128.6 | 358.5 | 0.96 | 26% | 51 |
| B: developer's first release | 111 | 115.5 | 285.8 | 1.00 | 23% | 12 |
| B: later release of that developer | 297 | 135.0 | 363.2 | 1.00 | 26% | 48 |
| A, excl. big brands | 92 | 117.1 | 277.3 | 1.01 | 23% | 8 |
| Returning web-first devs (not A, not big) | 269 | 120.0 | 336.9 | 0.92 | 24% | 41 |

- Recent games whose developer has 1 game on Poki (n=67): median votes/day 108.5, share in top quartile 21%. [dataset: developer game counts]
- Recent games whose developer has 2–3 games on Poki (n=90): median votes/day 135.7, share in top quartile 32%. [dataset: developer game counts]
- Recent games whose developer has 4–9 games on Poki (n=152): median votes/day 154.8, share in top quartile 28%. [dataset: developer game counts]
- Recent games whose developer has 10+ games on Poki (n=99): median votes/day 107.6, share in top quartile 16%. [dataset: developer game counts]

Interpretation: debut games perform almost the same as games from developers already on Poki (median 120 vs 129 votes/day; top-quartile share 23% vs 26%), but debuts are somewhat under-represented at the very top: 9/60 of the recent top 60 (15%) vs 24% of recent releases. Developers with 2–9 games do somewhat better; 10+-game developers have a lower median (volume strategies). [dataset] Inference: once a game passes soft release, a newcomer's typical outcome is close to average; the gap appears only among the biggest hits, where experienced web studios (WeLoPlay, OnRush, Jungle Tavern's later titles, Radical Play, splax.net) cluster.

### Top 15 debut games (definition A) released 2025–2026, by votes/day

| # | Game | Developer | Genre | Key categories | Released | votes | votes/day | rating | Class |
|---|---|---|---|---|---|---|---|---|---|
| 1 | Blockpost ⚑ | Skullcap Studios | Shooting Games | Action, Block, Multiplayer, Shooting, 3D, Gun, Games for Boys, First Person Shoo | 2025-07-17 | 1,853,339 | 4,222 | 4.40 | Web-first/indie |
| 2 | Count Control Legends | Jungle Tavern | Skill Games | Games for Girls, Brain, Skill, Mouse, 3D, Running, Stickman, Games for Boys, Num | 2025-11-10 | 755,115 | 2,338 | 4.42 | Web-first/indie |
| 3 | Paper.io 2 ⚑ | Voodoo | Action Games | Action, Strategy, .io, Color | 2026-08-24 | 53,585 | 1,488 | 4.36 | Big |
| 4 | Planet Destruction | Boop Games | Simulation Games | Mouse, Simulation, 3D, Space | 2025-12-31 | 400,699 | 1,473 | 4.47 | Web-first/indie |
| 5 | Magic Battleground | vessel | Fighting Games | Action, Ragdoll, Fighting | 2026-03-18 | 267,497 | 1,372 | 4.41 | Web-first/indie |
| 6 | Merge Rot | TapMen | Brain Games | Games for Girls, Brain, Mouse, Puzzle, Matching, Games for Boys, Crazy, Meme, Me | 2025-05-28 | 562,775 | 1,151 | 4.50 | Web-first/indie |
| 7 | Speed Stars ⚑ | Luke | Sports Games | Sports, Skill, Running | 2026-02-06 | 233,781 | 995 | 4.33 | Web-first/indie |
| 8 | Dino Simulator | Story Giant Games | Simulation Games | Animal, Simulation, 3D, Dinosaur | 2026-07-27 | 52,384 | 818 | 4.30 | Web-first/indie |
| 9 | Cat Pizza | Cosmonautic Games | Simulation Games | Games for Girls, Animal, Simulation, Cat, Pizza, Restaurant, Food, Tycoon | 2025-02-10 | 406,497 | 682 | 4.57 | Web-first/indie |
| 10 | Blast Buddies | Blasters | Shooting Games | Action, Multiplayer, Shooting, Gun, First Person Shooter | 2026-04-28 | 97,765 | 637 | 4.38 | Web-first/indie |
| 11 | Real City Bikes | Fuego! Games | Driving Games | Racing, Bike, 3D, Driving | 2026-03-30 | 114,789 | 627 | 4.43 | Web-first/indie |
| 12 | Mom's Diary Cooking Games | a1games | Simulation Games | Cooking, Simulation, Restaurant, Food, Easy | 2026-08-17 | 25,491 | 601 | 3.86 | Web-first/indie |
| 13 | Rumble Rush | PocketHaven | Platform Games | Skill, Platform, Multiplayer, Halloween, Games for Boys, .io, Obby | 2025-06-30 | 268,343 | 588 | 4.39 | Web-first/indie |
| 14 | Little Farm World | Tapfire | Simulation Games | Simulation, Farm, Food | 2026-09-15 | 6,963 | 497 | 4.30 | Web-first/indie |
| 15 | Oozy's Lab | Wackytoaster | Skill Games | Adventure, Skill, Platform, Slime | 2026-07-02 | 42,049 | 472 | 3.85 | Web-first/indie |

## 8. Extra: platform / orientation among recent releases

| Segment (recent) | n | median votes/day | p75 votes/day |
|---|---|---|---|
| mobile + desktop | 397 | 128.4 | 355.0 |
| desktop only | 11 | 12.2 | 196.4 |
| mobile orientation: both | 333 | 128.4 | 400.4 |
| mobile orientation: landscape only | 39 | 153.7 | 259.5 |
| mobile orientation: portrait only | 25 | 98.9 | 251.6 |
| 3D Games tag | 111 | 196.0 | 530.0 |
| no 3D tag | 297 | 100.6 | 270.8 |
| Multiplayer Games tag | 41 | 186.6 | 519.3 |
| 2 Player Games tag | 23 | 260.5 | 402.0 |

[dataset: mobile/desktop/mobile_orientation fields]. Note: 8 of the 11 desktop-only recent releases are Nitrome/Flipline legacy re-releases and the other hits are ⚑ Blockpost / Blockpost Legacy / Drift Hunters, so the desktop-only median is confounded. 397/408 recent releases ship on mobile+desktop and 333 support both orientations. Inference: shipping on mobile + desktop with both orientations is the norm; 3D (median 196 vs 101) and multiplayer/2-player tags are associated with higher traction.

