# AJ Ordaz: the full analysis (solo developer, 9 live games on Poki)

Prepared 2026-09-29. Scope: every AJ Ordaz game on Poki today, the two that were removed, and everything AJ has said in public about how he works (his YouTube titles and descriptions, itch.io and Steam).

## How to read this

- **Votes are not plays.** Votes = `up + down` thumbs. They are the best available proxy for how many players a game has had in total. **Votes/day (v/d)** = votes / max(days since release, 7) is the proxy for current traction. Neither one measures playtime or revenue. That matters here: AJ calls A Cleaning Story "my best launch ever" [Y1], but its votes do not show that (section 3).
- **RTI (cohort-relative traction index)** = a game's votes/day divided by the median votes/day of all Poki games released in the same calendar quarter. Rows with the 2019-03-11 migration date are left out of the cohorts. RTI 1.0 is typical for the quarter. **Qtr pct** = the share of same-quarter games with lower votes/day. RTI is the fairest way to compare games of different ages. Raw votes/day favours young games: the quarter median rises from 49.3 (2022Q4) to 172.2 (2026Q3). This uses the same method as `blumgi.md`, so the numbers can be compared directly.
- **Dataset gap:** `developer contains 'Ordaz'` returns **8** games from `poki/games.jsonl`. All 8 list `la-petite-avril` in `developer_games`, but that game is missing from the dataset because it is not in Poki's sitemap. I fetched its live page today with the same crawler (`crawl.py`) and saved it to `analysis/ajordaz_la_petite_avril.json`. It is labelled **[live fetch]** wherever it is used. It is *not* included in any cohort median, which all come from the 1,503-game dataset.
- All numbers come from `analysis/ajordaz_analysis.py`, and its output is `analysis/ajordaz_analysis.txt`. Today = 2026-09-29.
- **Inference:** marks my own interpretation. Everything else is either quoted from a source or computed from the dataset.

### Sources

| Key | URL | Date |
|---|---|---|
| Y1 | https://www.youtube.com/watch?v=Ym_1UrzF2Us "3 Games in 6 Months: What I Learned Making Games for Poki" (local `yt_ajordaz_3games6months.txt`, which has no SOURCE line. I confirmed the URL from the channel listing and re-fetched it into `yt_ajordaz_video_descs_3.txt`). There is no transcript, only the title and description. | 2025-09-13 |
| Y2 | https://www.youtube.com/@AJOrdaz/videos (the 30 most recent video titles plus the channel description, `sources/yt_ajordaz_channel_videos.txt`) | fetched today |
| Y3 | https://www.youtube.com/watch?v=Hrcu9BxtX8g "I Never Planned to Make Cozy Games… Until This Happened!" | 2025-11-08 |
| Y4 | https://www.youtube.com/watch?v=YYk4N6naFR8 "My Year as an Indie Game Dev: Successes, Failures, and $$$ Revealed!" | 2024-12-30 |
| Y5 | https://www.youtube.com/watch?v=bVBwZTfgZFo "The Business of Indie Game Development: A Look at My 2023 Earnings" | 2023-12-29 |
| Y6 | https://www.youtube.com/watch?v=jkIFhFUUst0 "testing my new INDIE GAME on Poki!" (Cannon Blast soft launch) | 2023-12-15 |
| Y7 | https://www.youtube.com/watch?v=AsKarubyRxw "Cannon Blast! - Play on Poki - Trailer" | 2024-01-24 |
| Y8 | https://www.youtube.com/watch?v=sPGpLuLck8Y "…Surprise Launch of A Pretty Odd Bunny: Roast it!" | 2024-05-27 |
| Y9 | https://www.youtube.com/watch?v=ZITHd0YRMpM "Rediscovering Passion… Devlog #12" | 2024-04-29 |
| Y10 | https://www.youtube.com/watch?v=6U-Nm3T2n2M "Why I Pulled Out of Steam Next Fest 2024" | 2024-06-13 |
| Y11 | https://www.youtube.com/watch?v=FxRAiPiFmcw "This is How 3 Months of GAME DEV Looks Like!" | 2024-10-13 |
| Y12 | https://www.youtube.com/watch?v=sWk6wea1fvo "…This Week on Poki" (first episode) | 2024-11-02 |
| Y13 | https://www.youtube.com/watch?v=4GijlSFxa1g Ranch UFO trailer | 2025-06-07 |
| Y14 | https://www.youtube.com/watch?v=rr-VUpzdI80 Nekopirate: Quest for Gold trailer | 2025-06-24 |
| Y15 | https://www.youtube.com/watch?v=RJY0Y-aBBJw Trapped in the Dollhouse launch trailer | 2026-07-10 |
| Y16 | https://www.youtube.com/watch?v=F2KSWE37qhM Trapped in the Dollhouse "Blue House UPDATE" | 2026-09-01 |
| Y17 | https://www.youtube.com/watch?v=U0xsDrZNPpE Lidle Legend trailer; https://www.youtube.com/watch?v=Z0NK15SSOJw Roast it! trailer | 2024-10-09; 2024-05-08 |
| I1 | https://itch.io/profile/ajordaz | fetched today |
| ST1 | https://store.steampowered.com/app/1470380/ (A Pretty Odd Bunny) | Steam release 2021-11-11 |
| ST2 | https://store.steampowered.com/app/2267970/Nekopirate/ | "Coming soon" |
| PK | https://poki.com/en/g/la-petite-avril (live fetch). https://poki.com/en/g/cannon-blast and https://poki.com/en/g/nekopirate both return **HTTP 301 → /en/adventure** (curl today) | today |
| D1 | https://developers.poki.com/guide/what-we-look-for | today's copy |
| D2 | https://developers.poki.com/guide/content-player-safety | today's copy |
| D3 | https://developers.poki.com/guide/player-fit-test | today's copy |
| D4 | https://developers.poki.com/guide/post-release-updates | today's copy |
| D5 | https://developers.poki.com/guide/web-engine | today's copy |

The video descriptions are saved in `sources/yt_ajordaz_video_descs_{1,2,3}.txt`. None of the ~33 Poki blog posts in `sources/` mention "Ordaz" (grep). **Poki has never featured him in a case study.**

---

## 1. Who he is (sources only)

- **A solo developer from Venezuela, who also teaches.** "I'm AJ Ordaz, a solo indie game developer from Venezuela crafting colorful, feel-good games with heart, humor, and a splash of weirdness" [Y14; almost the same wording in Y13]. The channel description says: "I'm AJ, I'm a teacher and indie game developer. I make games using Construct 3 and share the process via weekly devlogs, tutorials and more" [Y2].
- **Construct, since Construct 2.** On A Pretty Odd Bunny: "Yes, started in C2 and finished in C3" [I1]. The Dollhouse trailer is tagged "#construct3" [Y15]. His channel includes Construct 3 tutorials such as "How to add SAVE & LOAD features in Construct 3", "Easy CHECKPOINTS system in Construct 3" and "How to support MULTIPLE SCREEN sizes?" [Y2]. Poki describes Construct 3 as "focused on 2D games and fast prototyping", notes that it "keeps export size small" and "works very well on mobile", and lists an empty project at "342KB zipped" [D5].
- **Background in premium platformers.** His itch.io account was registered "Jul 22, 2014". It lists La Petite Avril (2023), A Pretty Odd Bunny and Nevado - Bark & Run, all tagged Platformer [I1]. A Pretty Odd Bunny came out on Steam on "Nov 11, 2021". Publisher "2Awesome Studio", price "$4.99", "80 levels in 4 unique worlds", "78% of the 19 user reviews" positive, 9 languages [ST1]. His video descriptions also link it on Nintendo Switch, Xbox, PS4/PS5, Android and iOS [Y4, Y5]. A free itch.io "first chapter" had "25 challenge-filled levels" and a Patreon ask for Chapter 2 [I1].
- **Nekopirate is his long-running passion project.** It is a "story driven action-platformer" with "Over 40 hand-crafted levels", still "Coming soon" on Steam [ST2]. It was "currently in development" in Dec 2023 [Y5]. In Apr 2024 he talked about "losing passion for a project" and coming back "to bring Nekopirate to life" [Y9]. In Jun 2024 he pulled out of Steam Next Fest because the demo "just didn't feel perfect enough" [Y10].
- **He is open about money** but gives no numbers I can check: "My 2023 Earnings" [Y5], "Successes, Failures, and $$$ Revealed!" (2024) [Y4] and an Android earnings video [Y2]. No transcripts were available, so **I cite no revenue figures.**
- **He studies Poki openly.** He ran a "This Week on Poki" series on his own channel: "Welcome to the first episode of This Week on Poki! In this new weekly series, we'll dive into the hottest, must-play games that dropped on Poki" [Y12]. **Inference:** this doubles as structured market research, and it comes right before his switch to Poki-native concepts in 2025.

---

## 2. Verified table of his Poki games

### 2a. Performance (dataset, as of 2026-09-29; La Petite Avril from the live fetch)

| # | Game | Released | Days | Total votes | Rating (up %) | Votes/day | Qtr median v/d | RTI | Qtr pct | Rank by votes /1,503 | Homepage pos. |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | A Pretty Odd Bunny | 2022-10-17 | 1,443 | **71,210** | 4.36 (84.0%) | 49.3 | 49.3 | 1.00 | 49 | 728 | – |
| 2 | La Petite Avril **[live fetch]** | 2023-08-16 | 1,140 | 57,122 | 4.03 (75.8%) | 50.1 | 82.4 | 0.61 | 31 | ~811* | – |
| 3 | A Pretty Odd Bunny: Roast it! | 2024-05-08 | 874 | 65,288 | 4.33 (83.3%) | 74.7 | 57.3 | 1.30 | 58 | 768 | – |
| 4 | Lidle Legend | 2024-10-09 | 720 | 13,032 | 4.30 (82.6%) | 18.1 | 49.0 | 0.37 | 24 | 1,187 | – |
| 5 | Ranch UFO | 2025-05-21 | 496 | 12,049 | **4.47 (86.8%)** | 24.3 | 100.6 | 0.24 | 19 | 1,197 | – |
| 6 | Nekopirate: Quest for Gold! | 2025-06-24 | 462 | 8,110 | 4.32 (82.9%) | 17.6 | 100.6 | 0.17 | 12 | 1,282 | – |
| 7 | A Cleaning Story | 2025-09-09 | 385 | 18,123 | 4.11 (77.8%) | 47.1 | 92.6 | 0.51 | 30 | 1,104 | – |
| 8 | Veggie Merge | 2026-06-05 | 116 | 1,599 | 3.80 (70.0%) | 13.8 | 176.2 | **0.08** | 2 | 1,459 | – |
| 9 | **Trapped in the Dollhouse** | 2026-07-09 | 81 | 28,885 | 3.88 (72.0%) | **355.0** | 172.2 | **2.06** | **63** | 993 | **51 / 145** |

\*The rank La Petite Avril would have if it were added to the 1,503 dataset games.

**Catalogue totals (dataset + live fetch):**
- **275,418 votes** across 9 live games. The 8 games in the dataset have 218,296 votes, which is **0.056%** of all dataset votes.
- Median per game: **18,123 votes, 47.1 votes/day, RTI 0.51**. **Only 2 of 9 games beat their quarter median** (Roast it! 1.30, Dollhouse 2.06). A Pretty Odd Bunny sits exactly at it (1.00).
- The average up share is 80.4%. The median across all Poki games is 82.7%.
- Dollhouse is the **only** AJ game on today's desktop homepage (position 51 of 145).

### 2b. Design anatomy (dataset `description`/`controls`/`categories`/`mobile_orientation`, plus the trailers cited)

| # | Game | Core mechanic | Controls (dataset) | Structure and rewards | Mobile orient. | Genre and categories |
|---|---|---|---|---|---|---|
| 1 | A Pretty Odd Bunny | Stealth platformer. "Every level has a pig you must catch without being seen by other members of your bunny community" | A/D move, W jump, S crouch (3 keys) | "dozens of colorful but dangerous levels in different unique worlds, collect hidden coins, unlock extra challenges". The Steam original has "80 levels in 4 unique worlds" [ST1]. It is his own premium IP, ported | landscape | Platform. Platform, Animal, Puzzle, Crazy |
| 2 | La Petite Avril | Platformer. "Each level represents a different time in Avril's life". The intro says the levels are "inspired by pregnancy" | A/D move, Space/K/Z jump and fly, X/L throw flower or hold to push (3 actions, 7 keys) | Linear levels, "help of some friends along the way". On itch.io since 2023 [I1] | landscape | Platform. Games for Girls, Adventure, Platform |
| 3 | A Pretty Odd Bunny: Roast it! | Same stealth verb as #1, plus roasting pigs | A/D, W, S | "20 levels", hidden sausages, "hidden secret at the end". It was a "surprise" launch and "my most successful launch so far" [Y8] | landscape | Platform. Platform, Animal, Puzzle, 2 Player, Crazy |
| 4 | Lidle Legend | Idle-style RPG loop. Fight weaker monsters → get stronger → beat a boss → coins → "permanently make your character hit harder" | WASD, mouse or tap to move; Space to attack | Boss ladder plus cosmetics ("weapons and pets") | both | Adventure. Action, Adventure, Idle |
| 5 | Ranch UFO | Platform shooter: "rescue your beloved cow from an alien abduction" | WASD or arrows, W/Space jump, click to shoot | "Over 25 levels on Earth and Space", "30 unlockable Hats", "Frantic boss fights" [Y13]. Collect "3 adorable ducks" | both | Shooting. Action, Platform, Shooting |
| 6 | Nekopirate: Quest for Gold! | Coin-collecting platformer with attacks | A/D, W jump, click or Space to attack | "25+ handcrafted levels", "a collection of pirate hats" [Y14]. Coins, cans, "the one and only crown". **Inference:** a Poki spin-off of the Steam Nekopirate [ST2] | both | Platform. Action, Adventure, Platform, Cat |
| 7 | A Cleaning Story | Cleaning satisfaction sim: "scrub, soap, and wash carpets until they sparkle … reveal the adorable designs hiding underneath, whether it's fluffy bunnies or hilarious brainrot characters" | Click or tap to choose; click and hold to move tools (**one input**) | "running a tidy-up business … across various maps" (intro). Still updated as of 2026-06-04. Tagged Christmas Games | both | Simulation. Mouse, Christmas, Simulation, Easy |
| 8 | Veggie Merge | Merge-and-serve: merge crops, "Serve visiting customers", "expand your farm by unlocking new land" | Click or tap; click and hold to merge (one input) | Order-fulfilment economy, land unlocks. Last updated 2026-06-12, one week after release | both | Puzzle. 9 categories incl. Merge, Idle, Farm, Food |
| 9 | Trapped in the Dollhouse | Point-and-click "horror puzzle" escape: "Explore every room, hunt for clues, solve puzzles, and track down the keys" | Controls field empty. The description says "Click or tap to play!" (one input) | "Explore over 10 rooms" and "don't free the doll!" [Y15]. **Content update after 55 days** (version 2026-09-02): "5 NEW ROOMS … unlock the True Ending" [Y16] | both | Brain. Games for Girls, Brain, Hidden Object, Puzzle, New, Horror |

### 2c. Games that are no longer on Poki (survivorship)

| Game | Evidence | Status today |
|---|---|---|
| **Cannon Blast** | "just soft launched on Poki … my first casual game … It went from idea to launch in less than 6 months which is a record for me", "over 50 levels, 4 Worlds" [Y6]. An "action-puzzle game" with cannons, a boss per world and a collectible crew [Y7] | `/en/g/cannon-blast` → 301 to /en/adventure [PK]. The unlinked slug text "cannon-blast" remains in 6 of his game descriptions (dataset) |
| **"nekopirate"** (separate slug) | Unlinked slug text "nekopirate," appears in the "other games" list of 5 descriptions. That includes **Ranch UFO**, whose list does *not* name Quest for Gold (dataset) | `/en/g/nekopirate` → 301 to /en/adventure [PK] |

**Inference:** AJ has had at least **11** titles on Poki, and 2 of them have gone. The live catalogue therefore flatters his hit rate. I cannot tell whether "nekopirate" was an earlier soft-launch build of the same IP or a different game.

---

## 3. Performance ranking, and what explains it

### 3a. Ranking by cohort-relative traction (RTI)

1. **Trapped in the Dollhouse: 2.06** (355.0 v/d, 63rd pct of 2026Q3, ranks 248th of 1,471 dated games by v/d)
2. A Pretty Odd Bunny: Roast it!: 1.30
3. A Pretty Odd Bunny: 1.00
4. La Petite Avril: 0.61
5. A Cleaning Story: 0.51
6. Lidle Legend: 0.37
7. Ranch UFO: 0.24
8. Nekopirate: Quest for Gold!: 0.17
9. Veggie Merge: 0.08 (2nd pct of 2026Q2, ranks 190th of 197 games released in 2026 by v/d)

By **total votes** the order is different, because older games have had longer to collect votes: A Pretty Odd Bunny (71,210) > Roast it! (65,288) > La Petite Avril (57,122) > **Dollhouse (28,885 after 81 days)** > Cleaning Story (18,123) > the rest. After 81 days Dollhouse already has **more total votes than any AJ release after Roast it! (2024-05-08)**, including Cleaning Story at 385 days old.

### 3b. Platformers vs Poki-native concepts

| Group | Games | Total votes | Median votes | Median v/d | Median RTI | Up share |
|---|---|---|---|---|---|---|
| Platformers (premium IP or platformer lineage) | APOB, La Petite Avril, Roast it!, Ranch UFO, Nekopirate QfG | 213,779 (**77.6%** of his votes) | 57,122 | 49.3 | 0.61 | 81.7% |
| Poki-native casual concepts | Lidle Legend (idle), Cleaning Story, Veggie Merge, Dollhouse | 61,639 | 15,578 | 32.6 | 0.44 | 75.9% |

(dataset plus the live fetch. Cannon Blast, which would be a casual concept, is gone and is not counted.)

The platformer group does not win simply because it is older. The table hides **two separate effects**:

- **Premium-lineage platformers worked in 2022–2024. Poki-made platformers failed in 2025.** APOB (1.00), La Petite Avril (0.61) and Roast it! (1.30) sat at or near their cohort median. Ranch UFO (0.24) and Nekopirate QfG (0.17) collapsed. Among the **43 platform games released 2025+** (genre or category), the median is 103.3 v/d and RTI 0.80. Ranch UFO ranks **39th of 43** and Nekopirate QfG **41st of 43** (dataset).
  - **Inference, why:** APOB and Roast it! have a genuine hook: a "carrot-allergic bunny who likes to eat pigs" [I1], in a stealth game tagged "Dark Humor" on Steam [ST1]. Ranch UFO and Nekopirate QfG are generic premises: rescue the cow, collect coins, find the crown. Poki's guidelines name "Originality: … Clear differentiation matters most in crowded genres" and "Web-first: designed for the web as a primary platform" [D2]. On accessibility, Poki warns that "Not all players can use standard keyboard inputs such as WASD" and encourages "mouse only input" [D2]. All five platformers are keyboard-first with 3 actions (move, jump, and crouch, attack, shoot or throw), and the three older ones are landscape-only on mobile.
- **Poki-native concepts are high-variance.** Their RTIs are 0.08, 0.37, 0.51 and 2.06. Simple one-input controls are **not enough**: Veggie Merge and Dollhouse share the same click/tap input and differ by a factor of 26 in RTI. What separates them is **the shelf and the twist**.

### 3c. Each Poki-native concept against its own shelf (dataset, releases 2025+ unless noted)

| AJ game | Comparison shelf | n | Shelf median v/d | Shelf median RTI | AJ game | Where it sits |
|---|---|---|---|---|---|---|
| **Dollhouse** | Horror OR Escape (category or genre), incl. Dollhouse | 16 | 202.8 | 1.93 | 355.0 / RTI 2.06 | **6th of 16**, beats 67% |
| Dollhouse | Horror Games only | 8 | 306.7 | 2.45 | – | 4th of 8 |
| Dollhouse | Hidden Object | 7 | 46.3 | 0.52 | – | 2nd of 7 |
| Dollhouse | Brain Games genre | 27 | 78.1 | 0.75 | – | 4th of 27 |
| Dollhouse | Games for Girls | 46 | 231.4 | 2.10 | – | 16th of 46 |
| Dollhouse | All 2025+ releases | 408 | 127.5 | 1.00 | – | 102nd of 408 (beats 75%) |
| A Cleaning Story | Titles containing clean, wash or scrub, 2024+ | 8 | 93.8 | 0.56 | 47.1 / RTI 0.51 | 6th of 8 |
| A Cleaning Story | Simulation genre | 71 | 135.7 | 1.00 | – | 54th of 71 |
| Veggie Merge | Merge Games | 41 | 27.2 | **0.25** | 13.8 / RTI 0.08 | 29th of 41 |
| Veggie Merge | Merge Games released in 2026 | 15 | 76.0 | 0.44 | – | 13th of 15 |
| Veggie Merge | Idle Games | 57 | 80.1 | 0.77 | – | 54th of 57 |
| Lidle Legend | Idle Games, 2024+ | 85 | 56.0 | 0.77 | 18.1 / RTI 0.37 | 74th of 85 |

What the shelves show (dataset):
- **Horror and escape is a strong shelf.** Its median RTI is 1.93, against 1.00 for the typical game. The breakouts next to Dollhouse: **Hide and Paint** (OnRush, released 2026-07-07, two days before Dollhouse, tagged Games for Girls, Hidden Object and Escape) at 2,975.4 v/d, RTI 17.28, homepage #61. **Backrooms Recovery** at RTI 10.01. **Escape From Spider** (Emolingo) at RTI 4.06. The closest match in concept is **Exhibit of Sorrows** (mtsai, 2025-03-10): "explore the eerie museum, solve puzzles, and collect keys" with "once-playful dolls". It has RTI 2.92 and a **4.63** rating, and sits at homepage #75.
  - **Inference:** Dollhouse entered a shelf with a proven precedent in point-and-click doll horror, and it lands at about the shelf median: RTI 2.06 against 1.93, and below the closest analog's 2.92.
- **Dollhouse's weak spot is sentiment.** Its up share is 72.0%, the **6th percentile** of all 1,503 games. The 2025+ horror and escape median is 81.2% (dataset).
  - **Inference:** players click on it but a noticeable minority dislike it. Possible causes are puzzle friction (no hint system is mentioned) or the scare level. Poki rules out "Sustained scary themes" for its all-ages audience [D2], so AJ's "cute horror" framing [Y16] is the allowed route, but it may leave some horror fans wanting more. This is the most obvious lever for moving it from roughly 2× to 5× or more.
- **Merge is a weak, crowded shelf.** The 2025+ Merge median RTI is 0.25, and 15 merge games came out in 2026 alone. Poki warns: "When a genre or trend gets crowded, we may decline additional similar submissions: overlapping games fragment the audience and drag each other's performance down" [D2]. Veggie Merge is a standard merge-and-serve loop with no stated twist. It did about as badly as the shelf predicts.
- **Cleaning can break out, but not the way AJ built it.** The cleaning leaders are Robo Cleaner Simulator (Camu, RTI 6.42), Power Wash Cleanup (Camu, 4.98) and School Cleaning (Finz, 2.63). Two of the three are 3D and two are tagged Idle. A Cleaning Story is mouse-only, not tagged 3D or Idle, and sits just below the shelf median (0.51 vs 0.56). Kuyi Mobile's Cleanup Crew is lower still at 0.22 (dataset).

### 3d. "Best launch ever" vs the vote data

- AJ, 4 days after the dataset's release date for the game: "From a big flop with Nekopirate to my best launch ever with A Cleaning Story" [Y1]. In May 2024 he said the same of Roast it!: "my most successful launch so far" [Y8].
- In the dataset, Cleaning Story's lifetime rate is 47.1 v/d (RTI 0.51), which is below Roast it! at 74.7 v/d (RTI 1.30). Among the three 2025 games in Y1 its order does match what he says: Cleaning Story 47.1 > Ranch UFO 24.3 > Nekopirate QfG 17.6 v/d.
- **Inference:** "best launch" most likely refers to early playtime or revenue in the Poki dashboard, which votes do not capture. Or the game started strong and faded. This dataset is one snapshot, so it cannot tell these apart. A mouse-only chill game may also draw fewer thumbs per play than an action game. **Treat votes as a floor on reach, not as a revenue signal.**

---

## 4. The strategy shift, cadence, and lessons

### 4a. "What players want vs what I want"

AJ describes the shift himself:
- 2023-12: Cannon Blast is "my first casual game and also the first one I develop in a short period of time … less than 6 months which is a record for me" [Y6].
- 2025-09: "how I changed my strategy, what I learned about making games for the web, and how listening to your audience can make all the difference … Should game developers focus on what they want to make, or what players want to play?" [Y1].
- 2025-11: "I never thought I'd make cozy and relaxing games… until A Cleaning Story changed everything. After that unexpected success, I decided to take things a step further and started working on not one, but two new cozy indie games … what inspired me to switch from platformers to cozy experiences" [Y3]. **Inference:** Veggie Merge ("a relaxing merge game") is probably one of the two. Dollhouse is horror, so it is not.

Timeline (dataset release dates; source dates in brackets):

| Phase | Releases | What he was making |
|---|---|---|
| **Porting phase** (2022-10 → 2023-08) | APOB (port of the 2021 Steam and console game), La Petite Avril (itch.io 2023 platformer) | Moving existing premium platformers onto Poki |
| **Mixed phase** (2023-12 → 2024-10) | Cannon Blast (soft launch 2023-12, now removed), Roast it! (sequel made for Poki), Lidle Legend (idle) | Poki-first versions of his own IP, first casual tests. Nekopirate Steam work stalls [Y9, Y10] |
| **Research phase** (2024-11) | – | "This Week on Poki" weekly series [Y12] |
| **Pivot phase** (2025-05 → 2026-07) | Ranch UFO, Nekopirate QfG, **A Cleaning Story**, Veggie Merge, **Dollhouse** | Faster cadence. Moves from platformers to one-input concepts on Poki shelves (cleaning, merge, horror escape) |

**Cadence (dataset):**
- 9 live releases across 1,361 days. The median gap is 189 days, but the pace changed sharply:
  - **2022-10 → 2024-10:** 4 live releases, with gaps of 303, 266 and 154 days.
  - **2025-05 → 2026-07:** 5 releases in 414 days. The gaps after Ranch UFO are 34, 77, 269 and 35 days (median **56**). Two pairs came out about five weeks apart: Ranch UFO → Nekopirate QfG and Veggie Merge → Dollhouse.
  - For comparison, Blumgi's median gap is 140.5 days (blumgi.md).
- **Inference:** the ~5-week pairs, the "two new cozy indie games" in parallel [Y3], and "3 different games" in "6 months" [Y1] all suggest he now builds concepts side by side at roughly 2 months each. Before, a single game took "less than 6 months", and that was "a record" [Y6].

**Did the pivot improve results?**
- **The median did not improve, but he found his first near-hit.** His median RTI was 0.805 for 2022–2024 (1.00, 0.61, 1.30, 0.37) and **0.24** for 2025–2026 (0.24, 0.17, 0.51, 0.08, 2.06).
- The 2025 drop comes mostly from the two late platformers. Among the audience-led concepts, the results run from a flop (Veggie Merge 0.08) through a mid result (Cleaning Story 0.51) to his best-ever relative traction (Dollhouse 2.06).
- **Inference:** the pivot swapped a steady low-mid baseline for a portfolio of bets. That only pays off if he keeps running cheap experiments and invests in the winner. His 55-day content update to Dollhouse [Y16] is exactly that, and it follows Poki's advice: "a content update is a great way to attract new players and bring existing ones back" [D4].

### 4b. The Blumgi gap, in numbers (dataset)

| Metric | AJ Ordaz (9 live) | Blumgi (13) | Ratio |
|---|---|---|---|
| Total votes | 275,418 | 4,120,843 | **15.0×** |
| Median votes per game | 18,123 | 225,455 | **12.4×** |
| Best game | 71,210 (APOB) | 1,032,676 (Blumgi Slime) | 14.5× |
| Median RTI | 0.51 | 3.02 | 5.9× |
| Games above their quarter median | 2 of 9 | 12 of 13 | – |

- **AJ's entire catalogue is only ~1.2× one median Blumgi game** (275,418 vs 225,455).
- **Correction to "mid-tier":**
  - Among the **87 developers with ≥5 games**, AJ ranks **82nd by total votes** and 77th by median votes per game. The median developer in that group has **1,912,606** total votes, 7× AJ.
  - By median RTI he ranks **62nd of 78** developers with ≥5 dated games (the median developer is at 1.21, Blumgi at 3.02, 17th).
  - Only among **all 442 developer credits**, including one-game studios, is he mid-pack at **183rd**.
  - So among repeat Poki developers, his record is **lower-tier**, not mid-tier.
- **What that implies (Inference):** experience does not carry over on its own. AJ has shipped a premium platformer on Steam and consoles, is fluent in Construct 3, and runs a YouTube audience. The 3-games video has 28,507 views [Y1 local file] and the Dollhouse trailer about 23K [Y2]. Even so, most of his Poki games land below their cohort median. On Poki, concept and shelf choice outweigh craft: his best-rated game (Ranch UFO, 86.8% up) is one of his least-played.
- **Closest to a breakout: Trapped in the Dollhouse**, and it is the only candidate:
  - RTI 2.06 (his best), 355.0 v/d, and his only homepage slot (#51).
  - It already has his 4th-highest vote total after 81 days.
  - It is a live-ops title (Blue House update, True Ending).
  - In raw v/d it beats 11 of Blumgi's 13 games, but that is an age artefact. In RTI it is still below Blumgi's median of 3.02.
  - It is also well short of a true breakout. The top-decile 2026 release runs at 1,107.8 v/d, and Hide and Paint, released the same week, has 8.4× Dollhouse's v/d.

---

## 5. A replicable "AJ Ordaz formula", and its limits

| Element | What AJ does | Evidence | How to copy it |
|---|---|---|---|
| **Engine and footprint** | Construct 3, 2D, small builds. Every game supports desktop and mobile. Every release since 2024-10 supports **both** orientations on mobile | [Y2], [I1], [D5]. Dataset `mobile_orientation` | Use a 2D engine with a small export size. Ship both orientations from day 1. Poki: "Our audience is majority mobile" [D1] |
| **Shelf first, then twist** | Dollhouse = a proven horror, escape and hidden-object shelf (median RTI 1.93) + a distinctive pink "cute horror" look + a Games for Girls tag | Section 3c | Pick a shelf with 2025+ median RTI ≥1.5 (horror, escape, Games for Girls). Avoid saturated shelves (Merge 0.25, Puzzle 0.44, Idle 0.77). Add one twist you can explain in a single line. Poki: "a creative twist on familiar mechanics" [D2] |
| **One input** | Click/tap only for Cleaning Story, Veggie Merge and Dollhouse | Dataset `controls` | Necessary but not sufficient (Veggie Merge). Poki encourages "mouse only input" [D2] |
| **Short build cycles, parallel bets** | About 2 months per game since 2025. Pairs released ~5 weeks apart | Dataset gaps. [Y1], [Y3] | Budget 6–10 weeks per concept. Use Poki's player fit test ("average playtime over 3 minutes, and at least 25% of the 500 plays lasting over 3 minutes") to kill or keep ideas [D3] |
| **Double down on the winner** | Roast it! sequel to APOB. Dollhouse content update at day 55 | [Y8], [Y16]. Dataset `version_last_updated` | Plan content hooks such as new rooms or endings before launch. Poki looks for "room to expand — content hooks … or a roadmap" [D1] |
| **Own voice** | "heart, humor, and a splash of weirdness" [Y14]: pig-eating bunny, haunted dollhouse | [ST1], [Y15] | Keep it all-ages. Poki rules out "Sustained scary themes" and "Graphic violence" [D2]. APOB's Steam page promises "gorey action, blood, and a lot of severed pig's heads" [ST1]. The Poki description says only "secretly hunts and eats pigs" (dataset). **Inference:** the pitch was toned down for Poki |
| **Build in public** | Devlogs, earnings videos, "This Week on Poki" | [Y2], [Y4], [Y5], [Y12] | Useful for learning and community. There is **no evidence** that it moves Poki numbers |

**Limits of the formula**
1. **Low hit rate.** 2 of 9 live games beat their cohort median, and 1 of 9 exceeds 2×. At least 2 more titles were removed (Cannon Blast and "nekopirate"). Plan for roughly 1 in 5 concepts working. That is an inference from his record, not a Poki statistic.
2. **The ceiling is modest.** His best result, RTI 2.06, is still below Blumgi's *median* game (3.02) and about 1/8 of Hide and Paint (17.28) on the same shelf. The formula gets you "solid on a good shelf", not a breakout.
3. **Following trends has limits.** Veggie Merge copied a popular format onto a crowded shelf and came 190th of 197 2026 releases by v/d. Poki explicitly manages "Oversaturation" [D2]. "What players want" means *a strong shelf plus something new*, not the current top genre.
4. **Sentiment risk on audience-led concepts.** Up share fell from ~82–87% on his platformers to 70–78% on the pivot games. Dollhouse sits at the 6th percentile. Broader appeal came with lower satisfaction, and the rating may cap how much Poki promotes it (Inference).
5. **Data caveats.** Votes are not plays, and they are not revenue (see the Cleaning Story "best launch" mismatch). Dollhouse is only 81 days old. Launch promotion inflates the votes/day of young games, and RTI only partly corrects for this. This is a single snapshot with no time series. La Petite Avril comes from a live fetch outside the dataset. None of AJ's videos had transcripts, so his own numbers and reasons are known only from titles and descriptions.
