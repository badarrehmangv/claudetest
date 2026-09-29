# Blumgi: the full analysis (Loïc Roger, 13 games on Poki)

Prepared 2026-09-29. Scope: every Blumgi game on Poki today, plus everything Loïc Roger has published about how he works.

## How to read this

- **Votes are not plays.** Votes = `up + down` thumbs. They are the best available proxy for how many players a game has had in total. Votes/day = votes / max(days since release, 7) is the proxy for current traction. Neither one measures playtime or revenue. That matters here: Loïc calls Blumgi Merge his most successful game, but it ranks only 8th of 13 by votes (see section 3).
- **RTI (cohort-relative traction index)** = a game's votes/day divided by the median votes/day of all Poki games released in the same calendar quarter. Rows with the 2019-03-11 migration date are excluded from the cohorts. RTI 1.0 is typical for the quarter. **Qtr pct** = the share of same-quarter games with lower votes/day.
- The dataset is one snapshot of surviving games. It cannot show how a game's votes changed over time.
- All dataset numbers come from `analysis/blumgi_analysis.py`, which runs on `poki/games.jsonl` (1,503 games, 1,471 of them with a release date) and `poki/homepage.json`. Today = 2026-09-29.
- **Inference:** marks my own interpretation. Everything else is either quoted from a source or computed from the dataset.

### Sources (the dates are the pages' own publish dates, read from page metadata today)

| Key | URL | Date |
|---|---|---|
| S1 | https://blumgi.games/10th-game/ | 2024-10-23 |
| S2 | https://blumgi.games/my-love-story-with-small-games/ | 2024-11-24 |
| S3 | https://blumgi.games/ive-killed-my-first-blumgi-game/ | 2025-08-28 |
| S4 | https://blumgi.games/how-my-15-year-old-son-gave-me-a-game-making-lesson/ | 2025-09-07 |
| S5 | https://blumgi.games/from-idea-to-millions-of-players/ | 2025-09-15 |
| S6 | https://blumgi.games/coming-soon/ and https://blumgi.games/about/ | 2024-04 |
| S7 | https://poki.com/blog/blumgi-my-journey-on-the-web-how-i-reached-100m-players-in-2-years-as-an-indie-game-developer | 2023-09-05 |
| S8 | https://poki.com/blog/developer-spotlight-blumgi-games-part-1 | 2026-04-09 |
| S9 | https://poki.com/blog/developer-spotlight-blumgi-games-part-2 | 2026-05-10 |
| S10 | https://store.steampowered.com/app/2918940/Blumgi_Soccer/ | Steam release 2024-05-14 |
| P1 | https://developers.poki.com/guide/content-player-safety | today's copy |
| P2 | https://developers.poki.com/guide/reading-results | today's copy |
| P3 | https://developers.poki.com/guide/final-review | today's copy |
| P4 | https://developers.poki.com/guide/how-testing-works | today's copy |
| P5 | https://poki.com/blog/building-web-browser-games-2026 | today's copy |

The blumgi.games RSS feed lists 6 posts. S1 to S6 cover all of them.

---

## 1. Who he is and how he works

### Person and background
- **Loïc Roger** is "the solo-developer behind Blumgi Games" [S8]. The Blumgi Ball description on Poki calls Blumgi "a game development studio based in France" (dataset).
- **Animation first.** He worked at Ankama as "an animator" on the Wakfu TV series [S8]. Ankama's "transmedia" setup let him try game creation, and "I fell in love with the process" [S8]. His first game was part of the Maximini project in Ankama's universes: "Yes my first game was a web game!" [S2].
- **Mobile.** He made King Tongue and Drag'N'Boom with one programmer each. "Both games were featured by Apple" [S2]. In his words: "it was magical that you could make a game with only two people" [S8].
- **Madjoh, later Madbox (hyper-casual).** "Over four years, I worked on around 30 games, always with a programmer as my teammate … Out of those 30 games, one of them really took off: Stickman Hook, which I co-created with Valentin Barat" [S2]. The idea came from the Worms Armageddon Ninja Rope: "one button, touch to hook, release to fly" [S8]. He calls it "one character, two gameplay elements and one button" and "technically my most successful game ever" [S9]. Another Madbox team did the Poki port [S7].
  - Dataset: `stickman-hook` (developer Madbox, released 2018-12-20) has 7,894,266 votes. That is **#3 of all 1,503 games** by votes, and it holds desktop homepage position 22 today.
- **Going indie.** He left after "15 years as an employee in animation and gaming" [S7] and started Blumgi "alone at first to limit the risks" [S7]. He "founded Blumgi studio three years ago" (written Oct 2024) [S1]. The first Blumgi game went live on 2021-11-05 (dataset). A French state allowance "gives you about a year to take risks safely" [S9]. "My first game did really well, enough to make a living right away" [S9]. By Sept 2023, with "six games" out: "My games have now been played more than 100M times" [S7]. That is Loïc's own count, not the dataset.
- **Deal with Poki:** "I create the games, they do the rest, and we share the revenue" [S7].

### Team: solo, with rotating co-creators
| Person or credit | Role | Source |
|---|---|---|
| Florent Juchniewicz | Co-created Blumgi Paintball ("I had the pleasure of co-creating it with my friend Florent Juchniewicz"). He was also a game-design intern on Drag'N'Boom | S1, S2 |
| Joachim Leclercq | Art direction on Blumgi Chase (the killed game), "supported by a regional grant from Picanovo" | S2, S3 |
| Tom (his son) | Concept and programming for Blumgi Merge | S4 |
| Venturous, Gesinimo, Puya | Poki co-developer credits: Swingo = "Blumgi × Gesinimo × Venturous", Racers = "Blumgi × Venturous", Paintball = "Blumgi × Puya" | dataset `developer` |
| Music | "In most of my games I've outsourced it, or my co-creators made it" | S5 |

**Inference (not verified):** "Puya" may be Florent Juchniewicz's label, because both are attached to Paintball.

### Tools
- **Engine: Construct 3.** "I used Construct 3 (a web game engine) to prototype my games in the mobile industry … Construct 3 worked perfectly with Poki, especially with constraints like low build sizes" [S8]. His son programmed "in Construct 3, which I also use" [S4].
- **Art: Adobe Animate.** "I use Adobe Animate for everything. It comes from my background at Ankama where we used Flash" [S9].
- **Ideation:** notes on his phone and drawings on his iPad. "One line concept lists and one picture per concept list" [S5].

### How he works
1. **Three idea sources** [S5]:
   - (A) passive ideas, such as diving: "breathe in, your body floats up";
   - (B) "Active ideas I hunt deliberately … to solve a fit problem with platform constraints";
   - (C) "Extracted mechanics": "one micro mechanic from a bigger game … like turning Worms ninja rope to a one button portrait mobile game".
2. **Prototype first, not paper.** "Now I try to play the experience I have in mind as soon as possible by making a prototype … I use all the shortcuts: dirty code and placeholders" [S5].
3. **Find the fun levers**, so there is "enough depth to be playable for around one hour" [S5]. He sketches many variants of the main mechanic on the iPad. The post shows sketches for Paintball, Swingo, Racers, Soccer, Dragon, Bloom and Rocket [S5].
4. **Platform-fit checklist** (verbatim list) [S5]: "playable in both portrait and landscape?", "confortable to play in a small window", "controls work on desktop (mouse/keyboard/trackpad) and touch", "controls and rules easy to understand?", "popular fantasy, theme, or characters?", "build size small", "low-skill / high-reward?", "ad-friendly (short gameplay chunks; rewards unlocked via ads)?", "content easy to produce once the core gameplay is set?". He adds: "when I design a game for Poki, I often hunt ideas with the platform constraints in mind from the start."
5. **Order of work:** mechanic first, then "themes and aesthetics that serve the gameplay". Structure has been "very level-based … super linear" and is "not my strongest area". Music comes "at the end" [S5].
6. **Test early and often.** "If fewer than 50% of players pass the first minute, the onboarding isn't good enough or the game isn't fun. It's better to know that early before you put in the effort to make 50 more levels" [S8]. He runs video playtests daily. But he warns: "a designer can rely too much on metrics and lose the original vision" [S8].
7. **Timeboxing.** Blumgi Merge was built in "exactly 30 minutes a day, no more, no less" for two months. After each sprint they wrote down "the exact challenge we were on and what the next step was". A playable prototype plus mockup took "one 'week equivalent' of work" [S4]. Today's tools: "You can spend one week on a prototype, get data, and decide whether to continue or stop" [S9].
8. **Killing projects** is standard practice, learned at Madbox: "sometimes you have to kill games and jump to the next one. It's part of the game" [S3]. Madbox kept "only the ones that could be profitable on a larger scale" [S2].

---

## 2. Verified table of every Blumgi game on Poki

Selection rule: `'Blumgi' in developers`, which returns 13 games including `swingo`. This matches his own count. Paintball is "the 10th Blumgi game" [S1]. The Killed post says "After eleven successful games" (Aug 2025, after Merge) [S3]. The interview says "I've released 12 games so far on Poki" (Apr 2026, before Splash) [S8].

### 2a. Performance (dataset, as of 2026-09-29)

| # | Game | Released | Days | Total votes | Rating (up %) | Votes/day | Qtr median v/d | RTI | Qtr pct | Rank by votes /1,503 | Homepage pos. |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Blumgi Rocket | 2021-11-05 | 1,789 | 910,865 | 4.19 (79.7%) | 509.1 | 75.6 | **6.73** | 89 | 95 | – |
| 2 | Blumgi Ball | 2022-02-23 | 1,679 | 412,425 | 4.20 (80.0%) | 245.6 | 34.0 | **7.23** | 87 | 228 | – |
| 3 | Blumgi Castle | 2022-08-18 | 1,503 | 425,863 | 4.29 (82.2%) | 283.3 | 93.8 | 3.02 | 77 | 222 | – |
| 4 | Swingo (× Gesinimo × Venturous) | 2022-12-05 | 1,394 | 316,292 | 4.29 (82.3%) | 226.9 | 49.3 | 4.60 | 82 | 297 | – |
| 5 | **Blumgi Slime** | 2023-02-16 | 1,321 | **1,032,676** | 4.25 (81.3%) | **781.7** | 80.3 | **9.74** | 97 | **79** | **18** |
| 6 | Blumgi Bloom | 2023-08-03 | 1,153 | 120,798 | 4.57 (89.2%) | 104.8 | 82.4 | 1.27 | 62 | 562 | – |
| 7 | Blumgi Dragon | 2023-12-04 | 1,030 | 229,132 | 4.25 (81.2%) | 222.5 | 106.0 | 2.10 | 74 | 377 | – |
| 8 | Blumgi Soccer | 2024-03-25 | 918 | 225,455 | 4.58 (89.5%) | 245.6 | 60.7 | 4.04 | 85 | 379 | – |
| 9 | Blumgi Racers (× Venturous) | 2024-08-30 | 760 | 84,708 | 4.23 (80.6%) | 111.5 | 63.0 | 1.77 | 60 | 678 | – |
| 10 | Blumgi Paintball (× Puya) | 2024-10-17 | 712 | 103,722 | 4.58 (89.4%) | 145.7 | 49.0 | 2.97 | 75 | 611 | 121 |
| 11 | Blumgi Merge | 2025-04-14 | 533 | 163,161 | 4.58 (89.6%) | 306.1 | 100.6 | 3.04 | 82 | 470 | – |
| 12 | Blumgi Bounce | 2025-12-02 | 301 | 84,748 | 4.35 (83.8%) | 281.6 | 94.5 | 2.98 | 82 | 677 | **15** |
| 13 | Blumgi Splash | 2026-05-22 | 130 | 10,998 | 4.36 (84.0%) | 84.6 | 176.2 | **0.48** | 32 | 1,213 | – |

Catalogue totals (dataset):
- 4,120,843 votes, which is 1.06% of all votes on Poki.
- Median per game: 225,455 votes, 245.6 votes/day and RTI 3.02.
- Median votes per game ranks **9th of 45** developers that have 8 or more games. Every co-developer gets full credit for a shared game.

### 2b. Design anatomy (dataset `controls`, `description`, `categories`, `mobile_orientation`; S10 for Soccer)

The dataset `intro` field for Merge ("before space runs out") and Splash ("propelling a watercraft") contradicts the developer description. It looks auto-generated, so the `description` field is used here.

| # | Game | Core mechanic (dataset description) | Controls (dataset) | Verb class | 2P? | Structure and rewards | Mobile orient. | Categories |
|---|---|---|---|---|---|---|---|---|
| 1 | Rocket | Rocket car on hilly tracks. "The longer you hold down the rocket button, the more powerfully you will be propelled"; slow-mo; mid-air flips | W/S or ↑/↓ drive, Space rocket (alt A/D) | 2 keys + hold-release boost | No | Levels to the finish line; unlock vehicle skins | landscape | Skill, Platform, Car, Driving, Games for Boys |
| 2 | Ball | Basketball physics puzzle with a slingshot throw and a twist: "teleporting directly next to your ball" | Click-drag-release; Space teleport | Drag-release + 1 twist | No | Levels; points unlock "9 unique … characters … designed after animals" | landscape | Sports, Skill, Platform, Basketball, Ball, Games for Boys |
| 3 | Castle | Artillery: "sink your enemies into the water". Hold to set power, release. Special weapons include "the famous teleporting basketball from its sibling game Blumgi Ball" | A/D aim + hold/release Space. 2P: E/R + A vs ←/→ + Space | Aim + hold-release | **Yes** (local) | Level cleared when every creature is gone; "a brand new cool character every few levels" | landscape | Action, Skill, Shooting, Arcade, 2 Player, Ball |
| 4 | Swingo | "can only move around using a grappling hook"; reach the fruit | Click-drag-release | Drag-release | No | Levels; points unlock animal characters | landscape | Skill, Platform, Arcade |
| 5 | Slime | "can only move around by jumping … the longer you hold it down, the higher"; touch the checkered platform | Hold and release click | **One button** hold-release | **Yes** (2 Player, 1v1 tags; intro: "Play solo or with a friend") | Levels; "Each stage will introduce something fun and quirky" | portrait | Games for Girls, Skill, Platform, Arcade, 2 Player, Slime, Difficult, 1v1 |
| 6 | Bloom | Rope cutting: "slice the ropes holding all the little seeds" so they drop into soil | Mouse or swipe to snip | Swipe-cut | No | Puzzle levels | landscape | Brain, Mouse, Strategy, Puzzle, Arcade |
| 7 | Dragon | "a single tap … fires a fireball, while another tap teleports you to the fireball's location"; arena battles to rescue dragons | Click/Space/tap | One button (tap-tap) | **Yes** (local co-op) | Arena battles | portrait | Action, Skill, Multiplayer, Arcade, 2 Player, Co-op |
| 8 | Soccer | "Hold down the action button, adjust your angle … release"; watch "the number of balls remaining" | Click-hold aim, release | One button hold-release | No | "Worlds" of levels. Steam version: "100 Short Levels", "No stories, intros, or complex menus" [S10] | portrait | Sports, Action, Soccer, Penalty |
| 9 | Racers | Platform racing where "your car can fly"; beat the clock | W/↑ speed, S/↓ brake, A/D position, Space fly, R restart | 4+ keys (most complex) | No | Levels with bronze/silver/gold medals; unlock cars | both | Racing, Skill, Platform, Car, Driving |
| 10 | Paintball | Team vs team: "paint the arena in your color" by walking, bombs, guns and skills | W/A/D move, S bomb (on-screen buttons on touch) | Platformer movement | **Yes** (local co-op or versus) | Matches; ranked ladder "to Diamond Rank"; hats and faces | portrait | Action, Skill, Platform, Strategy, Multiplayer, Shooting, Christmas, Arcade, Gun, 2 Player, Color |
| 11 | Merge | "combine slimes to make them stronger … fight waves of monsters … through the dungeon" | Mouse or tap to buy, merge, fight | Tap | No | Merge-power progression; single screen; "a real ending" [S4] | both | Adventure, Mouse, Monster, Idle, Slime, Merge |
| 12 | Bounce | Basketball: "Hold to build strength and release to shoot" | Click or tap, hold, release | One button hold-release | **Yes** (local) | "Play casually to relax or challenge yourself for the perfect shot" (level count not stated) | both | Skill, Basketball, 2 Player, Ball, Slime |
| 13 | Splash | "launch blobs to knock other blobs into the water"; "use slides and platforms" | Click-hold aim, release | One button hold-release | No | Levels ("Each level is a playful challenge") | both | Skill, Platform, Arcade, Slime, New |

Counts across the 13 games (dataset):
- **Verb:** 8 of 13 use charge-or-drag and release as the main verb (Rocket's boost, Ball, Castle, Swingo, Slime, Soccer, Bounce, Splash). The other 5 are Bloom (swipe), Dragon (tap-tap), Merge (tap), and Racers and Paintball (keyboard movement).
- **2P:** 5 of 13 have local 2-player.
- **Desktop orientation:** "both" for all 13.
- **Mobile orientation:** the first 4 games and Bloom are landscape-only. Slime, Dragon, Soccer and Paintball are portrait. All 4 games since Aug 2024 are "both".
- **Level counts** are not published on any Poki page (checked the live pages for Slime, Rocket and Merge). The only published count is the Steam version of Soccer, with "100 Short Levels" [S10].

---

## 3. What performed best, and why

### Winners and laggards (dataset)
- **Top tier:**
  - **Slime:** 1,032,676 votes, 781.7 votes/day, RTI 9.74, 97th percentile of its quarter, still on the homepage at #18 after 3.6 years.
  - **Ball:** RTI 7.23.
  - **Rocket:** 910,865 votes, RTI 6.73.
  - Then **Swingo** (4.60) and **Soccer** (4.04).
  - Slime and Rocket together hold **47.2%** of all Blumgi votes.
- **Bottom tier:**
  - **Splash:** RTI 0.48, 32nd percentile, 130 days old. It is the only Blumgi game below its cohort median.
  - **Bloom:** 1.27.
  - **Racers:** 1.77.
  - **Dragon:** 2.10.
- **Merge is the exception.** Loïc: "It's by far my most successful game on Poki and still doing super well after several months" [S4]. In the interview it is "one of my most successful games" [S9]. By votes it is only 8th of 13 (163,161), although it is 3rd by votes/day (306.1, behind Slime and Rocket).
  - **Inference:** his measure of success is revenue and playtime. Merge's web-fit result was "+10 min playtime" [S4], and a long idle session earns far more ad time per player than a vote count shows. Votes understate games with long sessions.
- **Ratings run against volume.** Within Blumgi, rating vs votes has Spearman −0.48, while across the whole dataset it is +0.30 (n = 1,475 games with 1,000+ votes).
  - The best-rated games are Soccer, Paintball and Merge at 4.58 and Bloom at 4.57, all in the 95th to 96th rating percentile.
  - The two biggest games are 4.19 (Rocket) and 4.25 (Slime), in the 27th to 38th percentile. Slime is also tagged "Difficult Games".
  - **Inference:** broad-reach, slightly frustrating skill games collect more votes, and more down-votes, than gentle, polished ones.

### Why (Loïc's explanation first, then what the data adds)
- **His explanation:** "there is a direct relationship between simplicity and success. It is always my simplest games, often the ones I made the fastest, that make the most money" [S8]. Also: "My most successful games are the simplest ones (Blumgi Merge and Blumgi Slime)" and "I definitely see a pattern of low skill / high reward in my best-performing games" [S4].
- **The data mostly agrees.** Games whose main verb is charge-or-drag and release have median RTI **4.32** (n=8). The other verbs have **2.10** (n=5). The two most complex control schemes, Racers (4+ keys) and Paintball (WAD + bomb), sit at 1.77 and 2.97.
  - Caveat: the release-verb games are mostly early releases, so this is confounded with timing.
- **Simplicity is necessary, not sufficient.** Four one-button release games range from RTI 9.74 (Slime) to 0.48 (Splash).
  - **Inference:** the winners combine a single verb with (a) a mainstream theme on a big Poki shelf (cars and driving, basketball, soccer) and (b) a clearly new twist (Ball's teleport, Rocket's hold-to-boost with slow-mo).
  - Splash reuses the charge-release verb from Castle, Soccer and Bounce, and repeats Castle's "knock them into the water" goal. It has the weakest early traction in the catalogue.
- **Laggards match his own warnings:**
  - **Racers** is skill-demanding driving with many inputs. That is the same failure mode as the killed Blumgi Chase, where "Players couldn't drive properly" [S3]. It also overlaps his own Rocket, which is another car platformer.
  - **Bloom** is a rope-cutting puzzle, and puzzle is a weak shelf: 2024+ `Puzzle Games` median RTI is 0.48 (dataset, n=154).
- **Theme shelves (dataset, 2024+ median RTI by category):**
  - Basketball 2.96 (n=7), Soccer 2.74 (n=17), 2 Player 1.67 (n=36), Car 1.33 (n=42), Skill 1.04, Platform 1.04, Puzzle 0.48, Merge 0.25 (n=58).
  - Blumgi's sports and car games sit on strong shelves.
  - Merge's RTI of 3.04 is an outlier in a weak, crowded category.

### Is traction per new game falling, flat, or rising?
- **Relative to cohort, it is falling.**
  - Median RTI by batch: games 1–4 (2021–22) **5.67** → games 5–8 (2023 to Mar 2024) **3.07** → games 9–12 (Aug 2024 to Dec 2025) **2.98** → Splash **0.48**.
  - Spearman of release order vs RTI: −0.63 across all 13, and −0.52 without Splash (dataset).
- **In absolute votes/day it is roughly flat.** Median votes/day by batch: 264.5 → 234.1 → 213.7. Merge (306.1) and Bounce (281.6) are among his best absolute launches. Spearman of order vs votes/day without Splash is −0.25.
- **Still well above the typical game.** 12 of 13 beat their quarter median, sitting between the 60th and 97th percentile.
- **Loïc's own explanation:** "When I joined Poki, there were less games on the platform … Now, there are stricter quality metrics" [S9]. And "the audience is becoming even more 'TikTok-like.' Concepts that worked a few years ago might have too much friction now" [S9].
- **Inference:** the Blumgi formula now produces solid games (about 3× the cohort median) rather than breakouts (6–10×). Whether Splash recovers is unknown. Its low score may partly reflect where it sits in Poki's rollout.

### Does the brand cross-linking show?
- **His claim** [S7]: "When I release a new game, they benefit from a visibility bonus and the entire catalog receives new players … The more games I release, the more this dynamic accelerates." Also: "Create links between the games so that when players discover one, they discover the others, and thus create a snowball effect?"
- **Visible cross-linking (dataset):**
  - **Naming:** 12 of 13 titles are "Blumgi X". Swingo, a co-developed game, is the exception.
  - **Developer lists:** each game's `developer_games` field lists all its siblings.
  - **In-game crossover:** Castle ships Blumgi Ball's teleporting basketball as a weapon.
  - **Recurring slime mascot:** 4 of 13 are tagged Slime Games (Slime, Merge, Bounce, Splash). Blumgi owns 4 of the 15 Slime Games on Poki, including #1 by votes.
  - **Sibling links in descriptions:** 12 of 13 have them. This is Poki's standard FAQ template, though, found in 732 of 1,503 descriptions.
- **Homepage:** Blumgi holds **3 of 145** desktop-homepage slots (Bounce #15, Slime #18, Paintball #121). That ties the maximum for any developer; 8 developers have 3.
- **What the data can and cannot show.** A snapshot cannot test the snowball claim. What it does show:
  - **For:** old games keep strong lifetime traction. Rocket (2021) has 509 votes/day. Slime is still promoted, and its build was updated on 2026-09-25 (`version_last_updated`).
  - **Against:** the brand does not guarantee a launch (Splash, RTI 0.48). And the one non-"Blumgi"-titled game, Swingo, still reached RTI 4.60, so the brand name is not needed for traction either.
  - **Inference:** cross-linking probably adds to the catalogue rather than creating hits. The catalogue's value comes from its long tail: "My first game still makes money today" [S9].

---

## 4. Design philosophy, and the lessons from the killed game and from Merge

### Stated philosophy (quotes)
- **Simplicity over depth:** "On Poki, complexity is a 'no-go.' If the UI is complex or they don't understand the goal instantly, there is zero engagement. Complexity doesn't mean deep though, that's where I tripped myself up" [S8]. "Simple stuff is hard to make. Making something simple that is also enjoyable is a skill in itself" [S9].
- **Essentialism in art:** "I look for efficiency - a kind of 'essentialism.' I'm very interested in logo design, where you express a lot with very little." In a small window "the art has to be readable. It's almost like a logo: few colors, high contrast, and very graphic. It removes the cognitive friction" [S9]. His inspirations are Japanese mascots, Oink Games and Famicase cartridge art [S2].
- **Small games as a business strategy:** "A positive production time / perceived value ratio." "I would spread the risk across several games while keeping them technically simple as I'm not a good programmer and get bored quickly" [S7]. "My strategy was to ship games fast to build a 'passive income' stack" [S9].
- **The archipelago:** "I like to compare Blumgi to an archipelago where each game is an island, and side by side, they create something bigger and more visible in the midst of the ocean" [S7]. "Blumgi Games are high-quality micro-games, coming together like islands, creating a gaming archipelago" [S6].
- **Surprise over difficulty:** "I try to base the experience on surprises and rewards rather than just difficulty. Challenge filters players based on their skill-level" [S9]. "Low effort, high reward." / "Exactly." [S9].
- **Let players find their own path:** "In Blumgi Slime … A player can play it safe, or they can try to be as efficient as possible … giving players the tools to find their own path makes them feel smart" [S9]. On a Stickman Hook exploit: "we left it in because it made the player feel like they had discovered a secret" [S9].
- **Onboarding is everything:** "It's like a TikTok audience - you have to be very direct … you only have a few seconds to convince the audience to play" [S8]. "You have to assume the audience has never played a game before. Some young players struggle with a mouse because they grew up on tablets" [S9].
- **Portrait plus landscape, mobile-first:** "the player ratio on Poki used to be 80% desktop and 20% Mobile; now it's 50/50 … I tend to make games with a mobile first attitude again … designing a game that works in both portrait and landscape modes. It's a nightmare to get the UI and the view right for both, but it's necessary" [S9]. Poki today: "Every game submitted to Poki needs to work in portrait, and our QA team tests for it" [P5].
- **One-button challenges:** "making a game with only one button because I know the audience likes to 'zap' through games" [S8].
- **Caution:** "never leave your job until you've tested the waters" [S9].

### Lessons from the killed game, Blumgi Chase [S3]
Context: Chase ran "more than a year" with Joachim Leclercq. "I restarted it multiple times … I felt very demotivated." He "never succeeded" at the Player Fit Test with it [S4] and "struggled for months to hit the minimum target with no success" [S4]. It is also very likely the game behind "I failed on a recent game I made last year because I tried to make the game 'deeper'" [S8]. That link is an **Inference** from the timing.

1. **A pitch document instead of a prototype.** "For the first time, I started with a pitch game design document instead of building a prototype … My cool ideas on paper, just weren't fun once I implemented them."
2. **No pre-production.** "I skipped a proper pre-production step, and that was a huge mistake. I carried design issues all the way to the end."
3. **Too much skill for the audience.** "way too skill-demanding for Poki players. Playtests went terribly, no matter which control scheme I tried. Players couldn't drive properly, kept crashing into walls, falling off cliffs, and never really understood the goal."
4. **Over-scoped.** "Because we were two on the project, I doubled the game's scope (at least…) and quickly got lost in complexity."
5. **Kill it and move on.** "sometimes you have to kill games and jump to the next one."

### Lessons from Blumgi Merge, made with his son [S4]
- **The concept was fitted to the audience, not "designed" for depth.** Tom's vision: "super easy to play, and the player gets stronger and stronger. You merge slimes, they beat monsters, you level up. That's it." Loïc objected: "where's the challenge? The risk/reward? Players will get bored fast." The result: "First test. First day. Exactly Tom's vision. BIM! The game passed the test", with "only a few clean monsters, the rest were doodle placeholders".
- **Test the gameplay loop before the art.** "you can get such strong engagement time with a game that's far from perfect and still WIP visually, as long as the gameplay loop is solid."
- **Daily video playtests.** Over 5 days, "Playtime went from 03:49 to 07:50 minutes". At that point "we had only invested about 2 weeks of full-time work", followed by "one more week finishing". The web fit test then showed "crazy metrics (+10 min playtime)".
- **Alignment makes everything easier.** "If a game is aligned with the audience from the start, everything becomes way easier."
- **One direction for every feature.** "Make the player feel more and more powerful at their own pace." All features reinforced it. "I think Poki players love experiences where they feel more and more powerful step by step."
- **One screen, rich content, a real ending.** "the entire game experience fit in a single screen. You are never cut off from the gameplay." The simple loop "allowed me to spend a lot of time designing nice monsters and polishing". "We even made a real ending."
- **Casual players want a gentle ride.** "some casual players are not looking for a deep experience. They just want to kill time in a rewarding way, without much focus, and enjoy progressing at their own pace."
- **One regret:** "I regret not adding sound."
- Loïc describes the web fit test as run "with 10 000 players". Poki's docs today describe it as ~7 days on real category pages, measured "against category averages" [P4].

---

## 5. The "Blumgi formula": a recipe we can follow

Each item notes where it comes from. The whole recipe is an **Inference** built from the sources and dataset above.

| Element | Recipe | Evidence |
|---|---|---|
| **Input** | **One main verb**: hold or drag, then release, on a physics body, where holding sets the power. Add **at most one twist verb** (teleport, boost, fly). The same input works on mouse, touch and Space. No virtual joystick. | 8 of 13 games use this verb, median RTI 4.32 vs 2.10 for the rest (dataset). Stickman Hook: "one button, touch to hook, release to fly" [S8] |
| **Goal** | Readable in one second: reach the platform, hoop, goal, fruit or finish line. Several ways to solve each level; tolerate exploits. | dataset descriptions; [S9] "find their own path" |
| **Content** | About **100 short levels, roughly 1 hour in total**. Introduce a new element or surprise every few levels. Don't build content until the first minute holds at least 50% of players. | "100 Short Levels" [S10]; "playable for around one hour" [S5]; Slime: "Each stage will introduce something fun and quirky" (dataset); 50% first-minute rule [S8]. **Inference:** about 36 s per level on average (60 min / 100) |
| **Session target** | Clear Poki's player fit test: "3+ minutes average playtime, with 25%+ of plays over 3 minutes". Aim for "5+ min average playtime" and "65%+ conversion to play". The Poki average is "around 70% conversion and 6+ minutes". | [P4] |
| **Rewards** | Unlock a character or skin every few levels. Use rewarded ads for unlocks, not interruptions. | Ball's 9 animal characters; Castle's "a brand new cool character every few levels"; Rocket skins; Racers cars; Paintball hats and faces (dataset); "rewards unlocked via ads" [S5] |
| **Art** | Flat 2D vector animation, "few colors, high contrast, and very graphic", with one expressive mascot. Readable in a small window. Cheap to produce, with high perceived value. | [S9], [S7] |
| **Start** | Straight into gameplay: "No stories, intros, or complex menus. Just launch and play!" Small build. | [S10], [S8] |
| **Orientation** | **Mobile portrait and landscape** from day one. | All 4 releases since Aug 2024 are "both" (dataset); [S9]; [P5] |
| **2-player** | Add cheap local same-device 2P or versus when the verb maps to one key per player (Castle: E/R + A vs arrows + Space). | 5 of 13 Blumgi games. Poki-wide 2024+ `2 Player Games` median RTI 1.67 (dataset). Within Blumgi, 2P games have median RTI 2.98 vs 3.54 for the rest (n=5 vs 8), so there is no internal proof that 2P helps |
| **Progression feel** | The player gets "more and more powerful step by step". Prefer surprise to difficulty. | [S4], [S9] |
| **Scope** | 1–2 people. Prototype in about 1 week. The simplest game (Merge) took about 3 weeks full-time plus part-time help. Timebox the work (30-minute sprints; write down the next step). | [S4], [S9] |
| **Cadence** | Median **140.5 days (about 4.6 months)** between releases. Range 48 to 232 days. 13 games in 1,659 days. The longest gap (232 days, Merge to Bounce) covers the killed Chase. | dataset `release_date` gaps |
| **Pipeline** | Video playtests (10 recordings each), then player fit test (500 players), then web fit test (about 7 days), then final review (1–2 weeks), then "roughly 2 to 3 months" to global release. | [P4], [P3] |
| **Kill rule** | If a week-one prototype can't pass the first-minute and player-fit gates after a few iterations, cut it. Never start from a design document. | [S3], [S9] |
| **Sound** | Include light sound, since he regretted leaving it out. | [S4] |

### What we must NOT copy (overlap that Poki can decline)
Poki's rules:
- Final review checks "Whether the game is unique enough within the categories it falls into" [P3].
- Games get declined when "The portfolio is covered. Sometimes a good game overlaps too much with what's already on Poki in its categories" [P2].
- The clone test lists "Core mechanics: Copied loop, goals, and inputs", "Art style: Near-identical visuals, colors, themes" and "Characters: Same designs, animations, silhouettes" [P1].
- "When a genre or trend gets crowded, we may decline additional similar submissions" [P1].

Blumgi (and Loïc's Stickman Hook) already occupy these verb-and-theme combinations. Avoid them:

| Occupied combination | Existing game(s) |
|---|---|
| Hold-to-charge jump with a blob or slime character; reach the platform | Blumgi Slime (1.03M votes; homepage #18) |
| Grappling-hook or rope swing through levels | Swingo, Stickman Hook (7.89M votes, #3 on Poki) |
| Basketball physics: slingshot + teleport, or hold-release shot | Blumgi Ball, Blumgi Bounce (homepage #15) |
| Soccer physics puzzle with limited shots | Blumgi Soccer |
| Car platformer with hold-to-boost or flying car time trials | Blumgi Rocket, Blumgi Racers |
| Artillery or launching to knock enemies or blobs into water | Blumgi Castle, Blumgi Splash |
| Cutting ropes to drop objects onto a target | Blumgi Bloom |
| Tap to shoot and teleport to the projectile | Blumgi Dragon (Ball's teleport too) |
| 2P territory-painting platformer | Blumgi Paintball |
| Merging slimes to fight monster waves | Blumgi Merge. The `Merge Games` category also has 82 games with 2024+ median RTI 0.25 (dataset) |

Also avoid:
- The look: a flat pastel slime or animal mascot, island branding, a "Studio + one noun" naming series. It would read as a Blumgi imitation under P1's art and character tests.
- His documented mistakes: a design document before a prototype, skipping pre-production, skill-heavy driving controls, and doubling scope because there are two of us [S3].
- Assuming the formula still breaks out on its own. His newest one-button physics-level game (Splash) sits at RTI 0.48 (dataset).

**What to take instead (Inference):** copy the **process** and the **shape of the product**:
- one release verb plus one twist;
- about 100 short levels;
- unlocks every few levels;
- logo-like art;
- both orientations;
- cheap local 2P;
- week-one kill gates.

Apply that shape to a **verb and theme that neither Blumgi nor Stickman Hook uses**, on a shelf with healthy 2024+ traction.
