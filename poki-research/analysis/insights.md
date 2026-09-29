# Poki blog, press and developer case studies: what they say about getting accepted and succeeding

Analyst scope: every `poki_com_blog_*` post except the Blumgi ones (another analyst covers Blumgi), plus `mobidictum_*`, `www_gamedeveloper_com_*`, `kuyimobile_*` and `defold_com_*`. Date of analysis: 2026-09-29.

I also added the following sources, all saved under `sources/` with a SOURCE line:
- the full State of Web Gaming Report PDF (the web page leaves out chart values),
- the Game Intelligence car-games PDF infographic,
- five Kuyi Mobile Substack posts that the archive listed but the local copies did not include.

Dataset numbers can be reproduced with `analysis/insights_dataset.py`, which writes `analysis/insights_dataset.txt`.

**Conventions**

- **Dataset** means `poki/games.jsonl`. "votes" = up + down. "vpd" = votes / max(days since release, 7). "home" = position in today's `desktop_home` list, where 1 = most prominent.
- **Votes are not plays.** Total votes stand in for cumulative player volume, and vpd stands in for current traction. §0 shows how noisy this proxy is.
- **Inference:** marks my own reasoning. Everything else is quoted or computed.
- Source keys used below are defined in this table.

| Key | URL |
|---|---|
| SOWG | https://poki.com/blog/state-of-web-gaming-report-2026 |
| SOWG-PDF | https://hub.poki-cdn.com/The_2026_State_of_Web_Gaming_Report_4ee6fdc260.pdf |
| SOWG-PR | https://poki.com/blog/web-gaming-report-announcement-2026 |
| HQ | https://poki.com/blog/what-makes-high-quality-browser-game |
| BUILD26 | https://poki.com/blog/building-web-browser-games-2026 |
| CAR | https://poki.com/blog/game-intelligence-car-games |
| CAR-PDF | https://hub.poki-cdn.com/Poki_Game_Intelligence_2026_Car_Games_64b100b391.pdf |
| Y2025 | https://poki.com/blog/2025-at-poki-a-year-in-review |
| DGA | https://poki.com/blog/poki-wins-dutch-game-awards-2025 |
| GT | https://poki.com/blog/developer-spotlight-gametornado |
| NPS | https://poki.com/blog/developer-spotlight-no-pressure-studios |
| EMO-P | https://poki.com/blog/how-emolingo-games-built-business-html5-web-games-poki |
| EMO-M | https://mobidictum.com/emolingo-games-webgames-poki/ |
| VP1 | https://poki.com/blog/the-story-of-vortellis-pizza |
| VP2 | https://poki.com/blog/6-million-plays-in-30-days-vortellis-pizza-delivery |
| VDU | https://poki.com/blog/i-quit-my-job-to-make-a-dress-up-web-game-and-it-blew-up |
| CC | https://poki.com/blog/how-we-made-cannon-clash-load-fast-and-boosted-conversion |
| ONR | https://poki.com/blog/meet-onrush-studio |
| ONR-PT | https://poki.com/blog/higher-success-rates-with-playtests |
| PEL | https://poki.com/blog/pelican-party-creators-of-narrow-one |
| UNI | https://poki.com/blog/beyond-the-app-stores-unico-studio-reaches-new-heights-on-web |
| O7 | https://poki.com/blog/outfit7-hit-talking-tom-live-on-poki |
| TT | https://poki.com/blog/tall-teams-launches-obby-roads-poki |
| SYBO | https://poki.com/blog/subway-surfers-match-and-blast-live-on-poki |
| GEV | https://poki.com/blog/game-events-new-tool-for-understanding-your-players |
| GGJ | https://poki.com/blog/ggj26-poki-winners |
| GGJ-END | https://poki.com/blog/green-game-jam-2026-is-over |
| GDC24 | https://poki.com/blog/poki-at-gdc-2024-introducing-poki-playtesting |
| DEF-P | https://poki.com/blog/poki-partners-with-the-defold-foundation |
| DEF-I | https://poki.com/blog/defold-foundation-x-poki-integration |
| MVA | https://mobidictum.com/pokis-web-gaming-interview-michiel-van-amerongen/ |
| M2024 | https://mobidictum.com/pokis-2024-milestones-a-booming-year-for-web-gaming/ |
| GD | https://www.gamedeveloper.com/business/the-huge-hidden-web-game-market-no-one-talks-about-and-how-to-get-in- |
| KUYI-PROC | https://kuyimobile.substack.com/p/my-game-production-process-and-how |
| KUYI-BVB | https://kuyimobile.substack.com/p/ball-vs-block-reimagining-a-classic |
| KUYI-2025 | https://kuyimobile.substack.com/p/the-year-that-was-2025 |
| KUYI-16 | https://kuyimobile.substack.com/p/16-years-of-building-joy |
| KUYI-ENG | https://kuyimobile.substack.com/p/make-games-not-engines |
| DEF-KUYI | https://defold.com/2026/02/17/Creator-Spotlight-Kuyi-Mobile/ |
| DEF-ORE | https://defold.com/2026/04/02/Creator-Spotlight-Orenji-Spark/ |
| DOC-PFT / DOC-WFT / DOC-DEAL / DOC-MON | developers.poki.com/guide/player-fit-test, /web-fit-test, /revenue-deal-types, /how-monetization-works (used here only as cross-references) |

---

## 0. Before using votes: how votes compare with sourced play counts

The ratio below is a sourced play count divided by today's vote count. Each play count was published on an earlier date, so every ratio is a **lower bound**. Figures come from `insights_dataset.txt`.

| Game | Sourced plays (date, source) | Votes today | Plays per vote (at least) |
|---|---|---|---|
| Subway Surfers | 1.7B sessions (Nov 2025, SYBO) | 21,396,026 | 79 |
| Stickman Hook | 574M (Apr 2025, GD citing a Poki presentation) | 7,894,266 | 73 |
| Monkey Mart | 300M (Apr 2025, GD) | 3,809,241 | 79 |
| Level Devil | 83M (Apr 2025, GD) | 4,142,008 | 20 |
| Rainbow Obby | 100M (Jul 2025, EMO-M) | 1,546,672 | 65 |
| Vortelli's Pizza | 40M (late 2023, VP2) | 628,070 | 64 |
| Venge.io | 50M (undated, ONR) | 2,319,969 | 22 |
| Bo's Bedroom | 2M+ (Feb 2026, DEF-KUYI) | 5,720 | 350 |
| Unico Studio (23 live games) | 500M gameplays (UNI) | 6,723,673 | 74 |

- **Inference:** the ratio runs from about 20 to more than 350 plays per vote. Votes are usable for broad tiers, such as "top-50 hit" versus "small". They are not reliable for close comparisons between games.
- Kuyi Mobile's games look especially under-voted. Sushi Merge had "millions of gameplays on the game's first month" (KUYI-2025) but has only 9,906 votes today (dataset).

---

## 1. State of Web Gaming Report 2026: every audience and developer fact

### How the survey was done (SOWG-PDF p.19, SOWG-PR)

- Poki commissioned two online surveys from Atomik Research, which is "MRS-certified".
  - Players: 2,000 "web gamers" in the US and UK. To qualify, respondents had to "play web games at least once per week".
  - Developers: 400 in the US and UK, "70% of which develop primarily for mobile platforms". The rest develop for PC.
- Fieldwork ran May 11–19, 2026.
- Traffic data is from Similarweb for May 2026.
- **Inference:** Poki paid for the study, the sample covers only US/UK weekly players, and there are no Poki-specific breakdowns. Treat it as directional.

### What the report does not contain

- **No age or gender data.** Neither the web text nor the 23-page PDF has any. The only audience-age evidence in my sources is qualitative:
  - "Poki is a playground for everyone, including kids" (developers.poki.com/guide/content-player-safety).
  - "A kid taps a link and they are playing a game within a few seconds" (Jim Hall, HappyLander, SOWG).
  - "It's so important for most kids to feel that they are in a world that's alive" (NPS).
  - Poki said it wanted more dress-up games, which the developer read as games "for little girls" (VDU; this is the developer's perception).
  - HQ talks of games "played by players of all ages".
- **No genre-preference question.** The closest item: "51% of surveyed gamers having played a web game that references internet trends/memes" (SOWG). Genre evidence comes from the car report (§3.5) and the case studies (§2 and §4).

### Player behaviour (chart values checked against the chart images on SOWG)

**How often they play** (SOWG-PDF p.6)

| Frequency | Share |
|---|---|
| Multiple times a day | 37% |
| Once a day | 20% |
| A few times a week | 29% |
| A few times a month | 14% |
| Less often | 0% |

"86% of web game players play at least a few times a week or more" (SOWG).

**Session length** (SOWG-PDF p.6)

| Length | Share |
|---|---|
| Under 5 min | 4% |
| 6–10 min | 18% |
| 11–20 min | 29% |
| 21–30 min | 22% |
| 31–60 min | 12% |
| Over 1 hour | 15% |

The most common player "plays multiple times per day, spends 11-to-20 minutes per session, and engages with two-to-three individual titles in a single session" (SOWG). **Inference:** 49% report sessions longer than 20 minutes (22 + 12 + 15).

**Games per session** (SOWG-PDF p.6)

| Games | Share |
|---|---|
| 1 | 31% |
| 2–3 | 49% |
| 4–5 | 15% |
| 6–10 | 3% |
| 11 or more | 2% |

**Inference:** 69% play two or more games per session. Hopping between games is the norm, which fits "the next game is one tap away" (BUILD26).

**Why they play** (SOWG-PDF p.5, chart checked)

| Reason | Share |
|---|---|
| They're free | 58% |
| They're easy to access | 56% |
| They're quick to play | 52% |
| They don't need to be downloaded | 34% |

The text adds 34% for "affordability" and 29% for "good value for money" (SOWG).

**When and where they play** (SOWG-PDF p.10)

| Situation | Share |
|---|---|
| Relaxing at home | 80% |
| During short breaks | 34% |
| While travelling to school or work | 22% |
| At school or work | 15% |
| None of these | 2% |

**What they do at the same time** (SOWG-PDF p.10, chart checked)

| Activity | Share |
|---|---|
| Listen to music | 56% |
| Watch shows (Netflix, YouTube, TV) | 49% |
| Use social media | 38% |
| Watch live streams | 26% |
| Chat with friends or family | 24% |
| Watch live sports | 24% |
| Play other games | 23% |
| "I don't do anything else" | 10% |

"90% of respondents" multitask. "44%, meanwhile, give the browser game their primary attention even when multitasking" (SOWG).

**Other platforms they own** (SOWG-PDF p.6, chart checked)

| Platform | Share |
|---|---|
| Android phone | 50% |
| iPhone | 45% |
| PS4/PS5 | 42% |
| Gaming computer | 34% |
| Xbox | 27% |
| Switch 1/2 | 27% |
| Non-gaming computer | 18% |
| Other | 1% |

"71% of web gamers own premium gaming hardware too" (SOWG-PR).

**Other findings**

- **Friction:** "46% ... have stopped playing a mobile game because it took too long to open or load. 28% ... because the download size was too large." On PC and console the figures are 32% and 26% (SOWG).
- **Social play:** "54% of surveyed consumers play web games with a friend or family member 'very often' or 'often'" (SOWG).
- **Quality:** "92% of consumers describe HTML5 web games as 'quite' or 'very' high quality" (SOWG). Part 3 of the report attributes the same 92% to *developers*, so the report contradicts itself.
- **Web versus social media:** 28% say their web-gaming time is increasing relative to social media, 43% say it is stable and 22% say it is decreasing. Among the most frequent players, 34% say it is increasing (SOWG-PDF p.13).

**Spending on gaming across all platforms** (SOWG-PDF p.15)

- 27% of all web gamers spend more than $50 a month.
- 35% of the most frequent players spend more than $50. Their full split: $0–10: 24%, $11–20: 15%, $21–50: 25%, $51–100: 23%, $101–200: 5%, $201+: 7%.
- Less frequent players: $0–10: 35%, $11–20: 23%, $21–50: 27%, $51–100: 13%, $101–200: 1%, $201+: 1%.
- 91% of developers rate web gamers as "quite" or "very" high-value.

**Discovery**

- "62% have downloaded or bought a game after first playing it on the web". This rises to 66% for US respondents and 72% for the most frequent players.
- 62% "have become a fan of a gaming or entertainment franchise after discovering it via a browser game" (SOWG).

**Platform audience size:** the Similarweb chart shows the top five platforms in the order Poki, CrazyGames, Friv, Coolmath Games, Playhop. It has no axis values. **Inference (pixel estimate):** CrazyGames' bar is about 60% the height of Poki's.

**Poki's growth:** "more than 100 million monthly active players in 2026, up from 10 million in 2020" (SOWG).

### Developer attitudes (SOWG-PDF pp.7–12, charts checked)

**Plans to ship on web in the next 12 months**

| Plan | Share |
|---|---|
| Port a mobile game | 53% |
| Build a native HTML5 game | 51% |
| Port a PC/console game | 41% |
| No plans | 8% |

**How hard publishing to a browser platform is**

| Answer | Share |
|---|---|
| Very easy | 27% |
| Quite easy | 47% |
| Quite difficult | 18% |
| Very difficult | 8% |
| Don't know | 1% |

**Benefits of web distribution**

| Benefit | Share |
|---|---|
| Creative freedom | 54% |
| Reach new users | 53% |
| New revenue stream | 47% |
| Discovery | 46% |
| Gateway to other platforms | 44% |
| Rapid updates and approvals | 38% |
| Early validation | 37% |

**Barriers to web distribution**

| Barrier | Share |
|---|---|
| Technical challenges | 53% |
| Not enough revenue | 36% |
| Not enough users | 36% |
| "Low quality channel" | 32% |
| Revenue cannibalisation | 31% |
| "Legacy channel" | 27% |
| "Not sticky enough" | 19% |

In addition, 54% call web a "fun nostalgia channel".

### Developer quotes in the report (SOWG)

- **Jim Hall, HappyLander:** "2-to-6 weeks of core development time suits me"; "see how real players respond within hours and act on it the next day."
- **Xavier Liard, StoreRider:** "Porting a Unity game to web takes 1-to-2 hours, but the real work lies in reducing load size, adapting controls and UI for PC and mobile, optimizing ad placement, and integrating SDKs like Poki's. Building standardized tooling can cover 70% of that effort."
- **Emre Şahin, Emolingo:** "we regularly update our games with content inspired by seasonal events, internet trends, and current player interests"; "we can also roll back to a stable version quickly."
- **Elena Lobova, Burny Games:** "the biggest barrier is still monetisation maturity compared to mobile"; web is "unlikely to match mobile in revenue scale in the near future."
- **Steindy Yanto, Gopandagames:** "the barrier to entry is lower, which increases competition ... developers need to create engaging, high-quality HTML5 games."

**Design implications (Inference):**
- Players multitask while listening to music or watching shows, so games should be glanceable and audio-optional.
- Sessions are 11–20+ minutes but spread across 2–3 games, so a game has to earn its share inside a multi-game session.
- Android is the most-owned device, so low-end Android performance matters. This matches the case studies in §4.

---

## 2. Developer case studies (Blumgi excluded)

### 2.1 Comparison table

"Dataset now" gives votes, vote rank out of 1,503, vpd, vpd rank out of 1,471 dated games, and homepage position (`insights_dataset.txt`).

| Studio | Team / engine | Key game(s) | Sourced results | Build time and iteration | What drove success | Mistakes / pain points | Dataset now |
|---|---|---|---|---|---|---|---|
| **GameTornado** (GT) | Solo (Peter Kaspar). Construct 3 | Short Life, Rex series, Dreadhead Parkour, Bullet Bros, Plonky | "first solo developer to join Poki", on Poki since 2018. Plonky was a 2025 "top performing" game (Y2025) | Fast prototypes, playtests | "simplicity and instant fun are more important than complex systems"; catalog of physics platformers | Optimisation "can sometimes be tricky with HTML5" | 18 games, 9.07M votes. Plonky: 766,030 votes, vpd 1,684 (#28), home #41 |
| **No Pressure Studios** (NPS) | Duo from a closed mobile studio. PlayCanvas plus their own engine layer and "No Pressure Net" (took 3 years) | Battle Blast (FPS), Fear Response, Crazy Cars | "a growing catalog of 1500+ web games" (sic; dataset has 11 games, so probably a typo). Crazy Cars is #5 on the car Poki Score (CAR-PDF) | 3 years building tech, then the game | Built for web from day one: bots with dynamic difficulty replace players who switch tabs; host migration instead of expensive servers | Tab-switching breaks live multiplayer; "not many network systems" handle it | 11 games, 9.54M votes. Rocket Soccer Derby 3.96M (#6). Battle Blast (2026-06-22) 63,239 votes, vpd 639, home #57 |
| **Emolingo** (EMO-P, EMO-M) | 2 → 5 full-time staff (Turkey). Per game: 1 developer, 1 3D artist, the designer. Engine not stated | Rainbow Obby, Wheat Farming (first game) | "Each of the studio's eight games ... has surpassed 10 million plays"; two above 75M; Rainbow Obby 100M; "around 800,000 gameplays per day"; concurrent players 1,000 → 10,000+ (Jul 2025) | "about three months" per title, then about a month more after "done". Soft launch to a Discord of 100,000+ | Reusable "standard character controller template"; cosmetics and power-ups "to support ad-based monetization"; Poki "advised us on game ideas based on player trends"; Poki-exclusive | Burnout from earlier big solo projects | 9 games, 3.71M votes, all but one support both orientations. Rainbow Obby 1.55M (#41). Steal a Brainrot (Oct 2025) vpd 1,203. Wheat Farming no longer in the catalog |
| **Devortel: Vortelli's Pizza** (VP1) | Solo (Wes). PlayCanvas | 3D multiplayer pizza sim | Soft launch from end of Aug 2022: 1.1M plays in about 2 months. Global launch Nov 10, 2022: concurrent players 400 → 1,400 → 2,800, peak 3,035; 7M plays at writing; later "over 40 million" (VP2) | More than a year solo; "force myself to release it as-is" | Poki homepage: featured on Poki Brazil; "Poki's system automatically moves games with strong user engagement to the front page" | Netcode desync on low-spec devices; ran up to 92 Linode servers; server autoscaling hard | 628,070 votes, vpd 422 |
| **Devortel: Vortelli's Pizza Delivery** (VP2) | Wes plus Kelsey part-time. PlayCanvas | Open-world driving | Launched Sep 20, 2023: "over 8 million times, 6 million of which were in the first 30 days"; 227 countries; about 1.2M hours | Frequent builds sent to Poki; "almost all" Poki suggestions added | 2.14MB initial download (58 requests), map loaded in chunks, Draco compression "nearly 70%"; Poki idea: coins for driving skill | Time limits frustrated players; curved roads disoriented them; "a large chunk" did not understand the minimap; blue-screen bug fixed by turning off real-time shadows | 272,763 votes, vpd 255 |
| **Devortel: Vortella's Dress Up** (VDU) | Kelsey (started with "zero game coding knowledge"), Wes joined full-time. PlayCanvas | 3D dress-up, later multiplayer competition | Dec 2024 launch: 5M gameplays in month 1, 6m28s average. By May 2025: "16 million gameplays per month", "460k daily active users", "12m 40s average session", "Largest tile on Poki USA homepage for 7 weeks", 12.5K concurrent peak | Idea from a Mar 2023 GDC chat; **78 playtest builds**; launched Dec 2024; multiplayer built in about 3 months of "nonstop work" | Poki asked for dress-up; character in a 3D world instead of scenarios; Poki bizdev and analytics asked for "a multiplayer game with a competition mode" | Half of users left at a text box; point-and-click movement not understood; scenario mode lost to a sandbox; traffic "tapering off" before new content | 1.24M votes (#60), vpd 1,892 (#23), home #23. Sister game Vortelli's Cafe (environment-management loop) has only 31,851 votes |
| **Elanra Studios: Cannon Clash** (CC) | Leonidas Maliokas. PlayCanvas plus their own "Solar Tools SDK" | Cannon Clash; earlier SimplyUp.io, ColorUp, Simply Prop Hunt | "2.4 MB download size with only 76 requests"; "81% conversion to play" in the Web Fit Test | Used Playtests and Web Fit Tests during development | Draco, Basis, MP3, atlases, async loading; "no initial menu"; systems introduced "wave by wave" | Intro story animation removed after playtests | **None of the four Elanra titles is in today's catalog** (dataset search) |
| **OnRush Studio** (ONR, ONR-PT) | 3 friends from ad tech; company founded 2021, "since grown to 10 team members". PlayCanvas (Venge) | Venge.io, Tribals.io, Sprint League | Venge "over 50 million gameplays on Poki alone"; "10 million gameplays monthly" (studio) | "one metric per iteration"; Impact × Time scoring (0–10 each); fake-door features and pop-ups to test interest | Moved from "gut feeling" to data. Pointer lock took engagement "from 2 minutes to 10 minutes almost overnight" (players' mouse left the game and hit other thumbnails) | Streamer and TikTok spikes are "random", hard to act on | 14 games, 4.56M votes. Venge 2.32M (#20). Hide and Paint (Jul 2026) vpd 2,975 (#7 overall, #4 of 2025+ releases), home #61 |
| **Pelican Party** (PEL) | Dutch duo. Three.js | Narrow.One, Nugget Royale, Ducklings | "well over 50 million gameplays total on Poki" across the catalog | "We don't release something if it's not finished" | Games "we would play ourselves"; original mechanic (arrows with drop-off); community Easter eggs | Wrote off "hypercasual" and "meme games" | 5 games, 1.78M votes. Narrow.One 850,208. Newer titles are weak: Stack City 29,055; Mouse Mouse 60,667 |
| **Unico Studio** (UNI) | Mobile studio with an in-house HTML5 team, first relying on "external expertise" | Brain Test series | "released over 25 games on Poki" in "two years", "500 million gameplays"; web "a growing share of the studio's revenue" | Port existing mobile games | "accessibility and instant engagement"; "Starting with existing games is a practical approach" | none stated | 23 games, 6.72M votes, **median only 25,037**. Brain Test 2.66M (#15, home #16) |
| **Outfit7** (O7, SOWG) | Big mobile IP owner | Talking Tom Gold Run (exclusive) | IP stats only (27B downloads) | "the porting process was straightforward and the core gameplay experience required very few changes" | Established IP, portrait endless runner | none stated | Released 2026-05-19: 531,642 votes, **vpd 3,997 (#5 of 1,471; #3 of 2025+)** |
| **SYBO** (SYBO) | Big mobile IP owner | Subway Surfers, plus Blast and Match (Nov 2025) | Subway Surfers "over 1.7 billion total gameplay sessions" in 7 years | none stated | IP | none stated | Subway Surfers #1 (21.4M votes). **Blast 16,264 and Match 3,631 votes** (vpd 51 and 11) |
| **Tall Team** (TT, CAR-PDF) | 8 people, ex-PopCap. Unity | Smash Karts; Obby Roads (Dec 2025, Poki-exclusive on web) | Smash Karts "over 4 million monthly active players", "top 10 web game"; 573s average play; "Six years of continuous updates"; Discord 250,000+ | Live service for years | "simple for a group of players to jump into and play together" | none stated | Smash Karts 1.51M votes (#44). **Obby Roads 32,626 votes, vpd 109, even though it is at home #30** |
| **Kuyi Mobile** (KUYI-*, DEF-KUYI) | Solo veteran (27 years). Defold | Sushi Merge, Coin Machine, Tower Merge, Cafe Bara, Bo's Bedroom, Ball vs Block | Sushi Merge "millions of gameplays on the game's first month"; Bo's Bedroom "over 2 million gameplays"; 702 concurrent players; first web game "still generating revenue" a year later | Prototype in 2–5 days; at most 3 months including art; Ball vs Block took 6 weeks to soft launch plus 3 weeks to global | Merge and management mechanics; data-driven iteration; 5–7MB builds | **9 rejections before the first acceptance**; "Tetris-like, Find Me, and Idle games don't really resonate"; hack-and-slash concept turned into a management game | 8 games, only 68,992 votes in total, which shows how noisy votes are |
| **Orenji Spark** (DEF-ORE) | Husband (developer) and wife (art). Unity → Defold | Jane's Fashion Studio | "build size was reduced by around 65%"; "Engagement and C2P started improving" | Rebuilt in Defold *during* soft launch | Took load-time complaints from dashboard feedback seriously | Unity build too heavy for web | Jane's (2026-03-26): 87,262 votes, vpd 467, home #129. Two more dress-up games since |
| **HappyLander** (SOWG, GEV, HQ) | Jim Hall | Diva Hair Salon, Smash Room, Stickman Fury, Ping Pong Go | Opening-object test: still playing at 3 minutes — glass 33.7%, cake 27.4%, phone 23.8% | "2-to-6 weeks of core development" | Diva Hair Salon: "how can I make a physics game that's interesting in the dress-up genre?" | Stickman Fury drop-off spikes after stage 56 turned out to be a bug in the mirrored levels | Two developer names ("Happylander", "Happylander Ltd"), 11 games. Diva Hair Salon 204,766 votes, vpd 504 |
| **Steelpan Interactive** (CAR-PDF) | Solo (Yannic Geurts). Unity | Blacktop Police Chase | 4.5M plays (US report); Poki Score 9.5; 4.4/5; "Together, my two games have brought in close to six figures" | none stated | "execution quality"; "does not reinvent the formula" | none stated | 301,742 votes, vpd 519, home #56 |
| **Fancade** (CAR-PDF, HQ) | Fancade engine | Drive Mad | "over $1 million in global revenue over 12 months"; 23.2% of US car-game plays; 358s average | none stated | "simple, funny and a bit chaotic ... Failing is part of the fun, and quick restarts"; starts immediately with the action centred on screen and on-screen arrows | none stated | 3.87M votes (#7), **home #1** |

### 2.2 Notes that do not fit in the table

**Vortella's step-by-step iteration record (VDU)** is the most detailed public before-and-after data on Poki.
- The metrics Kelsey tracked:
  - share of players past 4 minutes,
  - share watching at least one rewarded ad,
  - share clicking 1/10/20/40/100 items,
  - mean and median session,
  - tutorial funnel.
- The "stations" room with a player-controlled character "more than doubled my median engagement time from ~2 minutes to 4–5 minutes".
- Before launch: "97% clicked at least one fashion item", "25% of users clicked over 100 items", "~51% were staying longer than 4 minutes".
- Average session after each update:

| Version | Average session |
|---|---|
| Launch | about 5:30–6:30 |
| Physics and map update | about 8:30 |
| Multiplayer | 10:36 |
| Competition mode | 12:00–12:30 |

- Result: "The Poki algorithm took note and Vortella skyrocketed up the homepage, three months after its initial launch" (small → medium → large tile, 13–23 March).
- The studio motto became "Players just want to run around in a little world with other people". The evidence it cites: My Perfect Hotel (SayGames) and Monkey Mart (TinyDobbins). In the dataset these have vpd 2,170 (#19) and 2,684 (#10).

**Kuyi's process rules (KUYI-PROC, KUYI-BVB, DEF-KUYI)**
- Scope:
  - "keep my projects within a three-month development window, including art";
  - "I'll only add another month if there's a strong guarantee of getting published";
  - he capped content (Bo's Bedroom: 12 structures, 6 raw materials, 6 enemy types).
- Personal go/no-go rule: "10 playtests. If at least 3 out of 10 players stay engaged for three minutes or more, and at least one player continues playing for over ten minutes."
- Engagement gains in Ball vs Block:
  - performance fix: +30–40 s;
  - boss battles: +30 s;
  - replacing the paddle with a cannon: "an entire minute";
  - reached about 5 minutes in Player Fit Tests.
- Soft launch lasts "at least two weeks" and involves A/B tests on CTR, C2P and session time, including icon tests.

**OnRush's framework (ONR-PT)**
- Order of work: bugs first, then UX.
- Features are scored on Impact (0–10) and Time (0–10) and sorted.
- Before building a big feature: "We do fake implementations to check the potential or show a popup to see if players would like the feature."

**Dataset outcomes that contradict the headlines (Inference).** Pedigree and IP do not guarantee traction on Poki:
- Tall Team's Obby Roads: vpd 109 despite home #30.
- SYBO's match-3 spin-offs: vpd 51 and 11.
- Pelican Party's post-2023 titles: under 61k votes each.
- Devortel's Vortelli's Cafe: 31,851 votes.

By contrast, an IP port that keeps the original genre (Talking Tom Gold Run, vpd 3,997) and first-party games Poki pushed toward trends (Vortella's, SnapStyle) did well.

---

## 3. Poki's own statements

### 3.1 What makes a high-quality browser game (HQ)

HQ names four pillars: "Web-first Design", "Polished Presentation", "Originality and Uniqueness", "Inclusive Content".

**Instant play**
- Players "are not committed yet ... They are testing the waters, which makes the first few seconds of gameplay critical."
- Stickman Hook: the WebGL port was "40MB and had a median loading time of 29.5 seconds", giving "50% conversion to play". The HTML5 rebuild was "6MB", loaded in "3.7 seconds" and reached "72%", "so the game got 22% more plays".

**Drive Mad as the model:** "immediately starts up and the action is directly in the centre of the screen ... Transparent arrows ... The first few levels are specifically designed to tell the player how the gameplay loop works". Also: "core gameplay loops should be optimised for short player sessions."

**Ads:** "mostly non-intrusive adverts in the form of Rewarded Videos"; "Adverts that force themselves on the player are likely to frustrate."

**Visuals**
- "bright and colorful 2D or 3D object assets tend to garner more average plays and longer term success. Games with muted color palettes, pixel art or dark colours have a harder time standing out."
- Satisfying feedback on every click (the Jump Only example); "big, readable UI".

**Trends**
- "Implementing trends like Italian brainrot can be powerful, but they should enhance the gameplay, not just be a visual addition."
- Sprint League (OnRush) added "lots of different game modes inspired by trends" around its core mechanic.
- Diva Hair Salon combined physics with the "trending dress-up game genre".

**Depth:** "welcoming to first time players but has enough depth to offer something new for returning and experienced players" (Retro Bowl).

### 3.2 Building web games in 2026: Erik Dubbelboer, Poki Principal Engineer (BUILD26)

**Size costs players:** "For every extra megabyte a person has to download to play your game, you're going to lose a couple percent of players."

**Engines**
- "Unity is the most widely used engine among developers on our platform". But it compiles to "one large WebAssembly blob" and most Unity games "load every asset into memory at launch", which "makes conversion to play lower for Unity games than for web-native alternatives".
- Godot has the same blob problem, though lazy loading is in progress.
- PlayCanvas and Construct are "web-native". Phaser and PixiJS are frameworks.

**WebGPU:** "around 68% of players on Poki" (June 2026). Treat it "as an enhancement".

**Onboarding**
- "Web players behave more like TikTok viewers than Steam users."
- "Text-based tutorials fail. Pop-up instructions fail."
- For a Vampire Survivors–style game: "start the player off with the most crazy abilities for a couple of seconds ... then take them all away."
- The "space" key example: players "had no idea what a space bar was"; the fix was a picture of a keyboard.

**Portrait**
- "Portrait mode is winning on mobile web."
- "Asking them to rotate their phone is a conversion killer."
- "Every game submitted to Poki needs to work in portrait, and our QA team tests for it."

**Tools**
- Playtesting delivers "10 to 20 recordings" "within minutes"; "multiple versions a day."
- "Developers on Poki don't need to spend time or money on marketing."
- Automatic cloud saves.

**Dataset check:** Erik's own games (Silly Sky, Village Builder) are listed under developer "Project GD" with about 55k and 59k votes, so even Poki's principal engineer does not automatically get a hit.

### 3.3 Conversion benchmarks and loading (CC, docs)

- "a conversion rate above 70% is solid, and anything above 80% is exceptional"; "mobile users often expect faster load times" (CC).
- A game under 5MB is "doing an amazing job" (a Kasper Mol talk, paraphrased in VP2).
- Kasper Mol also says: "it's absolutely necessary to have a short and smooth loading experience through optimised file sizes and low engine overhead" (PEL).

**Fit tests (DOC-PFT, DOC-WFT, cross-referenced)**
- Player Fit Test: 500 players; pass = "average playtime over 3 minutes, and at least 25% of the 500 plays lasting over 3 minutes". "Games that succeed on Poki average 5+ minutes (10+ for management and simulation games)."
- Web Fit Test: CTR, average time on page and C2P, "weighted equally", each scored 0–5 against the category average; "about 3 to 5 days". Kuyi's experience was "5–7 days".
- For multiplayer games in the Web Fit Test, "add bots to fill open spots."

### 3.4 Game Events analytics (GEV, launched Aug 2026)

- Smash Room opening-object A/B test: glass 33.7%, cake 27.4%, phone 23.8% of players still playing at 3 minutes.
- Satisbox Mini Games: moving the stronger mini-games earlier raised the average session from 4:50 to 5:43, then to 6:23.
- Diagnostic rule: "If 80% of players see a feature but only 3% interact with it, that's a very different problem from only 10% of players ever seeing it."

### 3.5 Game Intelligence: car games (CAR, CAR-PDF; US data, 12 months, 2025–26, 154 titles)

**Category overview**
- Car games = "10% of all US plays"; 154 titles = 7.6% of the catalog; category average 332 s per play.

| Game type | Share of titles | Share of plays |
|---|---|---|
| Platform (led by Drive Mad) | 7% | 30% |
| Simulation (led by Crazy Cars) | 41% | 33% |
| Racing (led by MR RACER) | 33% | 18% |

Shares were mapped from the PDF layout.

**Share of US car-game plays:** Drive Mad 23.2%, Blacktop Police Chase 5.8%, Smash Karts 3.3%, MR RACER 3.3%, Crazy Cars 2.8%. "61.6% of category plays still come from games outside the top five."

**Longest average playtime:** Smash Karts 573 s, Build League 439 s, Traffic Escape! 423 s, Rocket Soccer Derby 397 s, Crazy Cars 395 s. "Three of the top five games include multiplayer or competitive elements, suggesting that social play can be a strong driver of retention." Drive Mad averages 358 s.

**Popularity is not satisfaction:** Drive Mad is rated 4.3, while City Car Driving: Stunt Master and Drift Boss are rated 4.6.

**Poki Score (plays + playtime + retention)**

| Rank | Game | Score | Engine | Poki exclusive? |
|---|---|---|---|---|
| 1 | Drive Mad | 10 | Fancade | yes |
| 2 | Smash Karts | 9.6 | Unity | no |
| 3 | Blacktop Police Chase | 9.5 | Unity | yes |
| 4 | Traffic Escape! | 9.2 | PixiJS | yes |
| 5 | Crazy Cars | 9.1 | PlayCanvas | yes |

"Poki exclusives account for 4 out of the 5 highest ranked games."

**What the winners share:** "A clear idea. Fast, satisfying play. And a reason to come back." Each top game won on something different: Drive Mad on "identity", Smash Karts on "live-service and community strategy", Blacktop on "execution quality".

**Inference: the report's plays and shares are consistent with each other.**
- 18.1M ÷ 23.2% ≈ 78M; 2.6M ÷ 3.3% ≈ 79M; 4.5M ÷ 5.8% ≈ 78M. So US car-game plays over 12 months come to about 78M.
- At "10% of all US plays", that implies about 780M US Poki plays a year. That would be only about 7% of the 11.1B global gameplays reported for 2025 (Y2025).
- Timeframes differ, so this is only indicative. It suggests most plays are outside the US, which is relevant to localisation and low-bandwidth markets.
- It also fits the dataset: the "Car Games" category has 128 games today, and there Drive Mad holds only 7.8% of category *votes* against 23.2% of US *plays*. Vote shares understate a hit's share of plays.

### 3.6 Platform scale, 2024–2026

| Period | Claim | Source |
|---|---|---|
| Nov 2023 | 50M monthly players; 350+ developer teams from 62 countries | DEF-P |
| Mar 2024 | 60M players per month; 350+ developers; Playtesting launched at GDC 2024 | GDC24 |
| 2024 (year) | "8.1 billion gameplays", "500 million players", "321 new titles", "150,814 minutes of playtesting" | M2024 |
| undated | "over 65 million monthly active users" | UNI |
| Jul 2025 | "over 90 million players each month"; Poki team of 65, "around 20% dedicated to building internal tools" | EMO-P |
| 2025 (year) | 625M players; 100M per month; 11.1B gameplays; 227 new releases; developers from 89 countries; "1,018 games hit the 1 million+ plays milestone"; top games "Plonky by Gametornado and SnapStyle Dress Up by PlayCap"; staff grew 50 → 65 | Y2025 |
| Jun 2025 | "1 billion plays" in a month | DGA, MVA |
| 2026 | 100M monthly active users; 600+ developers; 1B gameplays per month; "over 1,500 curated titles" | SOWG-PR, TT, MVA |
| Apr 2025 (third party) | "about 30 million monthly active users (MAU)" and "700 billion gameplays/month on Poki" (sic) | GD. **Contradicts Poki's own figures, so I treat it as unreliable** |

**Inference:** in today's catalog, 235 live games carry 2024 release dates and 211 carry 2025 dates (dataset). Poki reported 321 and 227 new titles for those years. Release-date definitions may differ, but this suggests some 2024 games were removed or re-dated. It fits the co-founder's "quality over quantity ... hand-picking the best titles" (MVA). The 2026 year-to-date count of 197 through September (dataset) runs a little ahead of the 2025 pace.

### 3.7 Co-founder interview: Michiel van Amerongen, Feb 2026 (MVA)

- **Monetisation:** "The most common concern we hear from developers relates to monetization"; "Despite lower ad rates than mobile app stores, we see games on Poki already generating up to €1 million a year."
- **Rewarded video:** "Rewarded Video has become the gold standard for browser gaming. We recommend three core strategies: game assists (like extra lives), currency rewards, and customization options."
- **Who succeeds:** "studios with up to ten team members that built their entire businesses around releasing and updating games on Poki."
- **Players:** web players "are driven by curiosity and a playground-like atmosphere where they can quickly jump between high-quality curated games."
- **Priorities:** "prioritise fast loading times and intuitive controls"; "improving their conversion to play from the get-go."
- **Plans for 2026:** "sustain our quality over quantity approach. We'll be hand-picking the best titles and welcome the right studios on board."
- **2025 breakouts:** "web-first Poki games like Drive Mad, Level Devil, and Vortella's Dress Up." In the dataset these are home #1, #4 and #23.

### 3.8 The multiplayer and social push (compiled)

- Poki's bizdev and analytics staff approached Vortella's a week after launch "if we could make Vortella's a multiplayer game with a competition mode" (VDU).
- Obby Roads was "designed for long-term player appeal and multiplayer competition", with progress kept through Poki player accounts (TT).
- "social play can be a strong driver of retention" (CAR-PDF).
- 54% of players play with friends or family often (SOWG).
- Kids "want to be in an online environment. Like an MMO vibe" (NPS).
- **The web-specific constraint:** tab-switching disconnects players. The solution was bots with dynamic difficulty plus host migration (NPS). Web Fit Test lobbies may not fill, so "add bots" (DOC-WFT).

### 3.9 Trends and seasonal content

- **Poki asks for genres:** Joep "mentioned they were looking for more dress up games on Poki" (Mar 2023, VDU). Poki "advised us on game ideas based on player trends" (EMO-P).
- **Dress-up is a proven lane.** Examples: SnapStyle Dress Up was a 2025 top game (Y2025; dataset vpd 1,999, #20), Vortella's, Jane's Fashion Studio, and Diva Hair Salon.
- **Green Game Jam 2026:** 34 Poki games took part. "most participating games saw a nice increase in gameplays and earnings"; much of the traffic "came from returning users" (GGJ-END). Snake vs Human gameplays rose 170% (GGJ).
- **Pelican Party pushes the other way:** "We don't make meme games" (PEL). Poki's position is that trends must "enhance the gameplay" (HQ).

---

## 4. Lessons that cut across the sources

### 4.1 Scope and timelines

| Who | Time | Source |
|---|---|---|
| HappyLander | 2–6 weeks of core development | SOWG |
| Kuyi Mobile | Prototype in 2–5 days; at most 3 months total; Ball vs Block 6 weeks to soft launch plus 3 weeks to global | KUYI-PROC, KUYI-BVB |
| Emolingo | About 3 months per title, including about 1 month of post-"done" polish | EMO-P |
| Playgama (third party) | "1-3 months. Including testing." "Cost: under $10 000." | GD |
| Vortella's Dress Up | About 21 months from idea (Mar 2023) to launch (Dec 2024); 78 playtest builds; 3 more months for multiplayer | VDU |
| Vortelli's Pizza | More than a year solo | VP1 |
| No Pressure Net | 3 years | NPS |
| Smash Karts | 6 years of live updates | CAR-PDF |

**Inference:** the teams that ship often (Kuyi, Emolingo, HappyLander, Unico) keep each game to about 3 months or less and decide early with playtests and fit tests. The long projects that paid off (Vortella's, Smash Karts, Venge) turned into live-service games that kept iterating after launch. Neither group bet a long build on an untested concept. Vortella's was playtested continuously.

### 4.2 Catalog strategy

- **Many shots:**
  - Emolingo: 8 games, each above 10M plays.
  - Unico: 25+ games in 2 years, 500M plays. Its dataset median is only 25,037 votes against 2.66M for the top title, so returns are concentrated.
  - Kuyi: 5 web games in his first year, a 6th on the way.
  - GameTornado: 18 live games.
- **Concentration (dataset):** the top 15 games hold 21.1% of all votes and the top 150 hold 60.9%.
- **The long tail:** "The long tail is not long ... A spike and then a slow death" (GD, Playgama).
- **Updates revive games:** Vortella's grew three months after launch through updates (VDU). Smash Karts shows "continued performance ... five years after its launch" (TT), and "Six years of continuous updates have kept the game growing" (CAR-PDF).
- **Inference:** a small studio should ship several low-cost, playtest-validated games and then pour updates, and multiplayer where it fits, into the one that shows traction.

### 4.3 What failed and why

**Genres and loops**
- Kuyi's 9 rejections: "Tetris-like, Find Me, and Idle games don't really resonate well with Poki's audience" (DEF-KUYI). Bo's Bedroom began as a hack-and-slash RPG that "didn't resonate" and was pivoted to management.
- Vortelli's Cafe: a management game where the player controls the environment. "engagement was way below where we needed it to be. We iterated through ideas and designs for months" (VDU). Dataset: 31,851 votes.
- Vortella's first loop (dress characters for scenarios) lost to a sandbox: "the simpler version that allowed more freedom ended up with longer sessions" (VDU).

**Onboarding and UX**
- "half of the users dropped when introduced to a text box modal" (VDU).
- Point-and-click movement "a lot of players didn't understand" (VDU).
- Mouse-camera with keyboard movement was hard for casual players (VDU).
- The "space" icon was not understood (BUILD26).
- Cannon Clash's intro animation was removed (CC).
- Players' mouse left the game area in OnRush's shooter and clicked other thumbnails (ONR-PT).

**Technical**
- Stickman Hook's 40MB WebGL port (HQ).
- Jane's Fashion Studio's Unity load time, fixed by a Defold rebuild (DEF-ORE).
- Low-end devices: Vortelli's Pizza netcode desync (VP1); Ball vs Block slowdown with dozens of balls (KUYI-BVB); a GPU-related blue screen fixed by turning off real-time shadows (VP2).

**Other**
- No new content: traffic "had been tapering off" (VDU).
- Pedigree without fit (dataset): Obby Roads, SYBO's Blast and Match, Pelican's later titles (§2.2).

**Catalog churn (dataset):**
- Elanra's four titles and Emolingo's first game, Wheat Farming, cannot be found in today's catalog by title, slug, developer or description.
- **Inference:** games can leave Poki or be renamed, so acceptance does not guarantee permanent listing.

### 4.4 Engine choices and load time

| Engine | Studios / games in these sources | Notes |
|---|---|---|
| PlayCanvas | Devortel (all titles), Elanra, No Pressure (Crazy Cars, Battle Blast), OnRush (Venge) | Web-native; delayed asset loading is easy (BUILD26); Draco and Basis built in (CC, VP2) |
| Defold | Kuyi Mobile, Orenji Spark; Monkey Mart and Cow Bay (DEF-P) | Poki's "preferred partner"; one-click "Bundle for Poki" and SDK template (DEF-I); "keeping a game within 5–7MB" (DEF-KUYI) |
| Construct 3 | GameTornado | "quick prototyping and performance" (GT) |
| Three.js | Pelican Party | "so small so everything downloads really fast" (PEL) |
| PixiJS | Fomo Games (Traffic Escape!, car #4) | CAR-PDF |
| Unity | Tall Team (Smash Karts), Steelpan (Blacktop); Orenji left it | "most widely used" but lower C2P (BUILD26). Still, **two of the top three car games are Unity** (CAR-PDF) |
| Own engines | Fancade (Drive Mad); No Pressure Sandbox on PlayCanvas | none |

**Load-size benchmarks**

| Game | Download | Result | Source |
|---|---|---|---|
| Vortelli's Pizza Delivery | 2.14MB, 58 requests | none stated | VP2 |
| Cannon Clash | 2.4MB, 76 requests | 81% C2P | CC |
| OnRush survival game | about 1MB | none stated | ONR |
| Stickman Hook (HTML5 rebuild) | 6MB | 72% C2P | HQ |
| Kuyi's games | 5–7MB target | none stated | DEF-KUYI |
| Kasper Mol's guideline | under 5MB | none stated | VP2 |

**Inference:** Unity is not ruled out, but it carries a C2P penalty unless the build is aggressively reduced. A small 2D/2.5D team aiming for the highest acceptance odds should pick a web-native engine (Defold, PlayCanvas, Construct, Phaser/Pixi) and keep the first download under about 5MB.

### 4.5 Promotion is earned through metrics

- Vortelli's Pizza: "featured on the front page of Poki Brazil" during soft launch (VP1).
- Vortella's moved small → medium → large tile after its session length rose (VDU).
- Poki's recommendation system is "performance-driven" (UNI).
- The Web Fit Test scores CTR, time on page and C2P against category averages (DOC-WFT).
- **Inference:** the thumbnail (CTR), load and onboarding (C2P) and session length are the three levers behind both acceptance and homepage exposure.

---

## 5. Revenue and business evidence (sourced numbers only)

| Claim | Source (date) |
|---|---|
| Drive Mad "generated over $1 million in global revenue over 12 months" | CAR (Sep 2026) |
| "games on Poki already generating up to €1 million a year"; ad rates lower than mobile app stores | MVA (Feb 2026) |
| "revenues for its top developers have increased tenfold in five years, varying from $50,0000 [sic] to $1 million annually" | DGA (Dec 2025) |
| Steelpan (solo): "Together, my two games have brought in close to six figures", enough for "financial freedom" | CAR-PDF (2026) |
| Emolingo grew from 2 to 5 full-time staff "With the revenue from their Poki titles"; the Poki partnership "provided not just funding" | EMO-P (Jul 2025) |
| Tall Team (8 people): "profitable self-funded game studios" | TT |
| OnRush: 10 staff, "10 million gameplays monthly" | ONR-PT |
| Unico: web "a growing share of the studio's revenue"; "profitability and sustainability" | UNI |
| Kuyi: first web game "still generating revenue today" a year later; now full-time on web | KUYI-16 (Apr 2026) |
| Vortella's: Kelsey left UX work to become a "Web Game Developer" full-time | VDU (2025) |
| Deal terms: web-exclusive by default for 5 years, with "a revenue share on players Poki brings" and everything from direct traffic "is yours". Non-exclusive = "one-time flat license fee". Terms are "indicative" | DOC-DEAL |
| Ad formats: midroll via `commercialBreak()` and rewarded via `rewardedBreak()`; portrait-capable games also get "Gamebar Display ads" | DOC-MON |
| Third-party cost figures: web game costs "under $10 000" and takes "1-3 months". Mobile needs "at least 25% of the budget into marketing, plus pay a 15-30% service fee"; publisher "30/70 split" | GD (Apr 2025) |
| Survey: 36% of developers say "not enough revenue"; 47% see a new revenue stream | SOWG |

**Inference:** outcomes range from roughly five figures a year for a modest hit to more than $1M for a category leader. There is no public revenue-per-play figure, so this material does not support converting plays or votes into money. Designing rewarded placements (assists, currency, cosmetics) is the lever Poki recommends.

---

## 6. The most decision-relevant insights

1. **Acceptance is decided by engagement data, not by a pitch.**
   - The sequence is: Player Fit Test (500 players; average over 3 minutes and at least 25% of plays over 3 minutes) → Web Fit Test (CTR, time on page and C2P weighted equally) → soft launch of at least 2 weeks → global launch.
   - "Games that succeed on Poki average 5+ minutes (10+ for management and simulation games)" (DOC-PFT).
   - A 25-year veteran was rejected 9 times before his first acceptance (DEF-KUYI). Budget for several concept attempts.
2. **Design the first 10 seconds for "TikTok viewers".**
   - No menu and no text: "Text-based tutorials fail. Pop-up instructions fail" (BUILD26). Half of Vortella's players left at a text box (VDU).
   - Put the action in the centre of the screen and teach through play, as Drive Mad does (HQ).
3. **Load size is a direct revenue lever.**
   - "every extra megabyte ... lose a couple percent" (BUILD26).
   - Stickman Hook went from 40MB / 29.5 s / 50% C2P to 6MB / 3.7 s / 72%, giving "22% more plays" (HQ).
   - Aim for under about 5MB and above 70% C2P; above 80% is "exceptional" (CC).
4. **Portrait support is mandatory.** "Every game submitted to Poki needs to work in portrait, and our QA team tests for it" (BUILD26). Portrait support also unlocks Gamebar ads (DOC-MON).
5. **Choose a web-native engine.**
   - Nearly every indie case study uses PlayCanvas, Defold, Construct or Three.js. Unity "conversion to play" is lower (BUILD26).
   - Orenji cut its build size by about 65% by rebuilding a Unity game in Defold mid–soft launch (DEF-ORE).
   - Unity still works if trimmed: two of the top three car games use it (CAR-PDF).
6. **"Players just want to run around in a little world with other people."**
   - A controllable character in a small world doubled Vortella's median engagement.
   - Updates to physics and map, then multiplayer, then a competition mode took the average session from about 6 to about 12 minutes, which set off homepage promotion (VDU).
   - Three of the five car games with the longest sessions are multiplayer or competitive (CAR-PDF).
7. **Web multiplayer has to survive tab-switching.** Use bots with dynamic difficulty and host migration (NPS), and add bots so Web Fit Test lobbies fill (DOC-WFT).
8. **Poki names the genres it wants.**
   - Dress-up was requested in 2023 and became a 2025 top game category: SnapStyle Dress Up (Y2025), Vortella's, Jane's, Diva Hair Salon.
   - Emolingo's trend-led catalog reached 8 games of 10M+ plays each by Jul 2025 (EMO-P). Its live titles are obby, escape and, since Oct 2025, brainrot games (dataset).
   - Trends must "enhance the gameplay, not just be a visual addition" (HQ).
9. **Avoid these genres and loops:** Tetris-like, "Find Me" and idle games (DEF-KUYI); environment-control management (Vortelli's Cafe, 31,851 votes); scenario-driven dress-up (VDU); a genre-swapped IP spin-off (SYBO's match-3 games have 16,264 and 3,631 votes against 21.4M for Subway Surfers; dataset).
10. **Use a bright, cohesive visual style.** Muted palettes, pixel art and dark colours "have a harder time standing out" (HQ). The thumbnail drives CTR, which is a third of the Web Fit Test score (DOC-WFT).
11. **Keep scope to 2–12 weeks per game and prototype in days.**
    - HappyLander: 2–6 weeks of core development (SOWG). Kuyi: 3 months at most; Ball vs Block took 6 + 3 weeks (KUYI-BVB). Emolingo: about 3 months (EMO-P). Playgama: under $10k (GD).
    - Kuyi's go rule: at least 3 of 10 playtesters past 3 minutes and at least 1 past 10 minutes (KUYI-BVB).
12. **Iterate one metric at a time with Poki's free tools.**
    - OnRush's pointer-lock fix took engagement from 2 to 10 minutes (ONR-PT).
    - Satisbox went from 4:50 to 6:23 just by reordering levels (GEV).
    - Smash Room's opening-object test ranged from 33.7% to 23.8% still playing at 3 minutes (GEV).
    - Vortella's needed 78 builds (VDU).
13. **Hits are made after launch.** Vortella's reached the large homepage tile three months after launch, through updates (VDU). Smash Karts is still growing after six years of updates (CAR-PDF). Seasonal events like the Green Game Jam brought players back, and Snake vs Human rose 170% (GGJ, GGJ-END).
14. **Promotion is algorithmic and earned.** The homepage follows engagement (VP1, VDU). Poki does the marketing, so no UA budget is needed (BUILD26). The same three metrics (CTR, C2P, session length) govern both acceptance and exposure.
15. **Know the audience from the only survey (US/UK weekly players).**
    - 37% play several times a day; the most common session is 11–20 minutes across 2–3 games.
    - 90% multitask (music 56%, shows 49%).
    - They play because games are free (58%), easy to access (56%) and quick (52%).
    - Android is the most-owned device (50%).
    - **No age or gender data was published.** The qualitative evidence says kids are a large segment (SOWG, docs).
16. **Most plays are probably outside the US (Inference).** The car report's numbers imply about 780M US plays a year against 11.1B global gameplays in 2025. Localisation and low-bandwidth performance matter. One example: Venezuela averages 3.9 Mbps (VP2).
17. **The revenue range for sourced examples:**
    - category leader: $1M+ over 12 months (Drive Mad, CAR);
    - "up to €1 million a year" (MVA);
    - top developers "$50,000 to $1 million annually" (DGA, typo corrected);
    - a solo developer with two games: "close to six figures" (CAR-PDF).
    - Monetise with rewarded video (assists, currency, cosmetics) (MVA).
18. **Expect web exclusivity.** The default deal is 5 years with a revenue share on players Poki brings (DOC-DEAL). Four of the top five car games are Poki exclusives (CAR).
19. **Two business models work, and both concentrate returns.**
    - Catalog cadence: Emolingo, Unico (25+ games, 500M plays), Kuyi.
    - A single long-lived multiplayer hit: Smash Karts, Venge, Vortella's.
    - Unico's median game has only 25k votes (dataset), and the top 150 games hold 60.9% of all votes (dataset). **Inference:** ship several cheap validated games, then double down on the winner.
20. **Pedigree does not guarantee traction** (dataset). Tall Team's Obby Roads has vpd 109 despite home #30. Pelican's post-2023 titles have under 61k votes each. By contrast, Talking Tom Gold Run, a straight IP port in its original genre, has vpd 3,997 (#5 of 1,471).
21. **The vote proxy is noisy.** Sourced plays per vote range from about 20 to more than 350 (§0). Kuyi's Sushi Merge had "millions" of plays but 9,906 votes. Use votes for broad tiers only.
22. **Acceptance is not permanent.** Elanra's four titles (including the Cannon Clash case study) and Emolingo's first game are missing from today's catalog (dataset). Poki reported 321 new titles in 2024, but only 235 live games carry 2024 dates today. Poki now stresses "quality over quantity ... hand-picking the best titles" (MVA).
