# Poki rules: pipeline, requirements, business terms (as of 2026-09-29)

**Scope.** This file describes how a game gets onto Poki today and what it has to satisfy. It is built from all 44 pages of the Poki developer docs (developers.poki.com/guide; the site's sitemap.xml lists exactly these 44 pages, checked 2026-09-29), plus five Poki blog posts: *What it takes to build games for the web in 2026* (5 Jun 2026), *How to Build a Great Browser Game*, *Creating higher success rates with playtests* (OnRush), *Poki at GDC 2024: Introducing Poki Playtesting*, and *How We Made Cannon Clash Load Fast*. The docs are the rules. The blog posts are context and worked examples. When they disagree, the docs win, and each disagreement is flagged in §7.

**How to read citations.** Short verbatim quotes are in "double quotes", followed by the source URL. Numbers from the crawl are cited as `dataset:` with the computation. Anything that is my reasoning rather than a source statement is marked **Inference:**.

---

## 1. The pipeline, step by step

### 1.0 Overview (durations and gates)

| # | Stage | What is measured | Pass bar / gate | Duration | Limits / notes | Source |
|---|---|---|---|---|---|---|
| 0 | Request P4D access | Application form | "we'll reach out to give you access to Poki for Developers" | n/a | The form requires links to previously released games ("Can you provide us with links to those games?Required"), genres, and engines | https://developers.poki.com/guide/share |
| 1 | Add your game | Content moderation of every uploaded version | Must clear moderation before any test | n/a | "Each uploaded version passes a content moderation check before it can be tested." The build "doesn't need to be finished" | https://developers.poki.com/guide/how-testing-works, https://developers.poki.com/guide/adding-your-game |
| 2 | Playtesting | 10 recorded sessions per test (video, inputs, console, duration, country, device) | Gate: "Player fit tests unlock once you've watched 10 recordings" | "first results often arrive within minutes" | "you can run as many as you like, at any stage". Audience is chosen by category and device | https://developers.poki.com/guide/how-testing-works, https://developers.poki.com/guide/playtesting |
| 3 | Player fit test | Playtime histogram across **500 players** (playtime only, no C2P) | "Healthy result: 3+ minutes average playtime, with 25%+ of plays over 3 minutes" | "~5 hours per test" | "Up to 2 tests per day". "Requires a thumbnail". You choose a category and the mobile orientations | https://developers.poki.com/guide/how-testing-works, https://developers.poki.com/guide/player-fit-test |
| 4 | Web fit test | CTR, average time on page, C2P (to first `gameplayStart()`), "weighted equally", each scored 0–5 against category benchmarks | "A 3 means you're at or above the category average." Passing is automatic: "Pass, and it's automatically submitted for the final review." No numeric pass cutoff is published | "roughly 7 days" (how-testing-works) **or** "about 3 to 5 days" (web-fit-test page); see §7 | "~10,000 players". You can suggest "up to four" categories. "Once started, a test runs its full course and can't be stopped." Repeatable | https://developers.poki.com/guide/web-fit-test, https://developers.poki.com/guide/glossary, https://developers.poki.com/guide/reading-results |
| 5 | Final review | Human review of results and of the game: "quality, originality, and fit within our categories" | Game must be "in line with our quality guidelines, including originality and craft" and "unique enough within the categories it falls into" | "Decision within 1 to 2 weeks" | A no is final for that game: "It is therefore not possible to publish your game on the Poki platform." | https://developers.poki.com/guide/how-testing-works, https://developers.poki.com/guide/final-review |
| 6 | Agreement | Contract | Legal prepares it | n/a | "Poki offers you an agreement and our legal team prepares the contract for your game." | https://developers.poki.com/guide/release-process |
| 7 | QA | Build checked against the requirements | Pass the QA report items | Iterative | "If it's not quite ready, you receive a QA report detailing what's needed to pass … QA continues until you're through." | https://developers.poki.com/guide/release-process |
| 8 | Soft release | Conversion to play, engagement, errors, monetization, feedback | "aim for at least 1 ad per daily active user, with a healthy split between midroll and rewarded videos" | Scheduling "typically takes 1-2 weeks". Soft release itself "should take around 2-3 weeks" | "cannot be skipped". Shown only on category pages: "We're not promoting the game on our homepage or localized homepages during this phase." The animated thumbnail is added here | https://developers.poki.com/guide/release-process |
| 9 | Global release | Promotion system reacts to performance | n/a | "usually … 2 - 3 weeks to move from soft release to global release" | "a significant push for around 2 weeks" plus "a fire icon on your thumbnail" | https://developers.poki.com/guide/release-process |
| 10 | Afterwards | Ongoing | n/a | n/a | Keep fixing, optimizing, and shipping content updates (§4.5) | https://developers.poki.com/guide/post-release-updates |

**End-to-end timing.** Testing takes hours for playtests, about 5 h per player fit test, about 7 days for a web fit test, and 1–2 weeks for final review ("A web fit test runs for approximately 7 days, and the final review takes 1 to 2 weeks", https://developers.poki.com/guide/how-testing-works). After a green light: "the road from agreement to global release takes roughly 2 to 3 months" (same URL; repeated on https://developers.poki.com/guide/final-review).
**Inference:** from a test-ready build, the fastest realistic path to global release is roughly 3–3.5 months: about 1 day of playtest/PFT iteration, 1 week of web fit test, 1–2 weeks of review, then 2–3 months of release process. Every failed test adds iteration time.

### 1.1 Targets beyond the minimums
- The thresholds are floors: "The thresholds above are the minimum to move forward. Games that do well on Poki usually clear a higher bar." (https://developers.poki.com/guide/how-testing-works)
- The recommended targets are "65%+ conversion to play" and "5+ min average playtime (10+ for management and simulation games)". For context, "the average game on Poki reaches around 70% conversion and 6+ minutes of playtime. Treat these numbers as a floor, not a finish line." (https://developers.poki.com/guide/how-testing-works)
- On the player fit test page: "3 minutes is the bar to advance, not the target for success; stronger games average 5+ minutes" (https://developers.poki.com/guide/player-fit-test)
- Unity's C2P penalty: "Unity games carry extra build weight, which is why they typically land around 60 to 65% even when well optimized" (https://developers.poki.com/guide/reading-results)
- A developer's rule of thumb, not Poki policy: "Generally, a conversion rate above 70% is solid, and anything above 80% is exceptional." Cannon Clash reached "81% conversion to play" in its web fit test at "2.4 MB download size with only 76 requests" (https://poki.com/blog/how-we-made-cannon-clash-load-fast-and-boosted-conversion)

### 1.2 Stage mechanics worth knowing
- **Playtests.** "Each playtest gets you 10 video recordings, together with the button inputs the player made during the tests and the console output." Players opt in through a "Mystery Tile" (https://developers.poki.com/guide/playtesting). The 2026 blog says "10 to 20 recordings" and "Developers can upload multiple builds per day" (https://poki.com/blog/building-web-browser-games-2026).
- **Reading the player fit test.** "Most players in the first two columns? Players quit early" points to onboarding or load time. "A peak in the middle columns? … possibly content depth, possibly a hook." (https://developers.poki.com/guide/player-fit-test)
- **Web fit test rules** (https://developers.poki.com/guide/web-fit-test):
  - Placement: "We place your game in multiple categories that fit it."
  - Mid-test bugs: "Found a bug mid-test? Upload a new version and email developersupport@poki.com to swap the version being tested."
  - SDK: C2P counts visitors who "reached your first gameplayStart() event, so make sure it's implemented before you start".
  - Ads: "commercialBreak() and rewardedBreak() aren't required yet … placeholder ads show and no revenue is made during the test."
  - Multiplayer: "test traffic is limited, so filling lobbies can be tricky. Connect to your existing servers if you have a player base, or add bots to fill open spots."
  - After passing, the game waits in limbo: "your game stays live, it's unpromoted, and it doesn't earn anything".
- **Diagnostics matrix** (https://developers.poki.com/guide/reading-results):
  - "Good playtime, low CTR in web fit": fix the thumbnail.
  - "Good CTR, low conversion to play": fix file size and load speed.
  - "Players arrive and convert, but leave quickly": "Thumbnail overpromises, or early difficulty wall".
- **Iteration policy.** "Every test is free and repeatable." If a game isn't a fit: "keep the risks low, don't over-invest, and bring us the next idea. Plenty of Poki success stories didn't pass on the first try." (https://developers.poki.com/guide/reading-results)
- **Curation scarcity.** "Every game on Poki is hand-picked. We keep daily releases limited, so each game gets a real shot at being seen." (https://developers.poki.com/guide/working-with-poki). Poki reported "227 new game releases" in 2025 (https://poki.com/blog/2025-at-poki-a-year-in-review).
  - `dataset:` 197 live games have release_date between 2026-01-01 and 2026-09-28. That is 197 / 272 days = 0.72 per day, about 5.1 per week.
  - `dataset:` 211 live games have a 2025 release_date, against 227 announced. **Inference:** the gap is probably games removed since, or a date-field quirk.
  - `dataset:` 44 of those 197 games from 2026 (22.3%) have "first game on Poki" in the description. This is a lower bound for games from debut developers, because not every description carries the phrase.

---

## 2. What Poki looks for, and what it declines

### 2.1 The three baseline signals and the five extras
Source: https://developers.poki.com/guide/what-we-look-for.

**Baseline:**
- **Quality**: "mainly looking at the UX/feel and the core game loop".
- **Player fit**: "Would they like to play this game and have fun?"
- **Tech**: "fast load times, stable frame rates, and a lean file size across devices and engines".

**Beyond the basics:**
- **Originality**: "Clones of existing hits don't stand out to players and won't be promoted".
- **Depth and replayability**: "a satisfying core loop that opens up over time".
- **First impression**: "players decide in seconds".
- **Cross-device feel**: "Our audience is majority mobile, so a desktop-only game is at a disadvantage".
- **Room to grow**: "content hooks, systems that support updates, or a roadmap/update plan shared at submission".

**How they are weighed:** "None of these … is a checklist with a pass mark; we weigh them together, and a game that's exceptional on one dimension can make up for lacking in another."

### 2.2 Why games are declined at final review
Source: https://developers.poki.com/guide/reading-results.

- **Originality and craft:** "We look for original games with a clear sense of human creativity, polish, and authorship. Using AI and other tools to accelerate development is fine; games that feel heavily tool-assisted or rapidly assembled are not. Downloaded templates and repackaged APKs don't qualify as original work."
- **Content:** "We avoid anything even slightly shocking, and we deliberately err on the safe side."
- **Portfolio overlap:** "The portfolio is covered. Sometimes a good game overlaps too much with what's already on Poki in its categories."

Additional quality reasons (https://developers.poki.com/guide/content-player-safety): "Buggy or broken gameplay", "Excessive load size or poor performance", "Confusing UX, or poor and inconsistent graphics".

Two rules cannot be negotiated: "misused IP and adult themes mean immediate rejection, and strong metrics never override the quality guidelines." Poki also says: "we can't always go into detail about why a game was declined." (https://developers.poki.com/guide/content-player-safety)

### 2.3 Clones, originality, "adds to diversity"
Source: https://developers.poki.com/guide/content-player-safety.

- "Direct copies and clones are never accepted; they violate our Terms & Conditions. Games inspired by known genres and ideas are welcome, as long as they contribute something new."
- Clone test, on six dimensions:

| Dimension | ❌ Clone | ✅ Inspired |
|---|---|---|
| Art style | "Near-identical visuals, colors, themes" | "Reimagined style or a completely different theme" |
| Core mechanics | "Copied loop, goals, and inputs" | "A unique mechanic, twist, or genre blend" |
| Progression & economy | "Same structure, pacing, monetization" | "Original level flow and progression logic" |
| UI, icons, audio | "Replicated layout, colors, or audio cues" | "A distinct interface with custom assets" |
| Characters | "Same designs, animations, silhouettes" | "Original characters, no IP infringement" |
| Name & thumbnail | "Intentionally similar to ride search terms" | "Presentation focused on your own content" |

- Parody: "Games that walk the parody line may be taken down on legal request or limited in marketing. Templates and asset flips with little modification don't qualify as original work either."
- Diversity bar: "we reserve the right to decline any game that lacks originality or doesn't add to the diversity of the platform, even if it functions well — as a quick check, 'adds to diversity' means offering a mechanic, setting, or angle not already well-represented on Poki, not just a variation on an existing hit."
- What Poki loves to see: "Originality: fresh gameplay ideas, or a creative twist on familiar mechanics. Clear differentiation matters most in crowded genres." Also "Web-first: designed for the web as a primary platform, not a mobile port", "Polish", and "Wholesome and inclusive".

### 2.4 Trends and oversaturation
Source: https://developers.poki.com/guide/content-player-safety.

- "Staying on top of trends is part of making great web games, and we fully encourage it. … They're not an excuse for rushed, low-effort, or repetitive content."
- What they want from a trend game: "Something unique added to the trend, not a collection of memes, viral challenges, or tropes without meaningful gameplay underneath." And: "Games that feel too derivative may be declined even when they function well".
- Oversaturation: "We actively manage variety on the platform. When a genre or trend gets crowded, we may decline additional similar submissions: overlapping games fragment the audience and drag each other's performance down. Approach a trend from a fresh angle that evolves it".
- Blog context: "Implementing trends like Italian brainrot can be powerful, but they should enhance the gameplay, not just be a visual addition". The blog's examples are Sprint League (trend-inspired modes built around one core mechanic) and Diva Hair Salon (a physics game inside the dress-up trend) (https://poki.com/blog/what-makes-high-quality-browser-game).

### 2.5 AI-assisted production
Source: https://developers.poki.com/guide/content-player-safety.

- Golden rule: "AI should empower, not shortcut."
- "before your game enters a player fit or web fit test, it should reflect your unique perspective and meaningful improvements beyond the base tooling."
- Pre-submit checks: "No AI watermarks or prompt text visible anywhere", "All dialogue reviewed", "Everything is playtested. No untested generated content ships."
- Ownership: "Be able to show how and which tools were used, and to provide an overview of your creation process, prompts, and iterations on request."
- The Do/Don't table forbids, among others, "'Mario-style' prompts to dodge originality. AI art doesn't make a clone original" and "misleading art that isn't the game" in thumbnails.

### 2.6 Art-direction signal (blog, not a rule)
- "games with bright and colorful 2D or 3D object assets tend to garner more average plays and longer term success. Games with muted color palettes, pixel art or dark colours have a harder time standing out." (https://poki.com/blog/what-makes-high-quality-browser-game)
- "your core gameplay loops should be optimised for short player sessions." (same URL)

---

## 3. Technical requirements and quality guidelines

### 3.1 Hard requirements
Source: https://developers.poki.com/guide/requirements-quality.

1. "Desktop, mobile, and tablet support. … On mobile, cover the full screen in portrait or landscape, or both for the best experience. Force mobile control schemes on tablets."
2. "16:9 aspect ratio. Your game must scale to cover the full canvas. Scale proportionally to 640x360, 836x470, or 1031x580."
3. "Incognito support. … wrap localStorage operations in a try/catch. Your game must stay playable."
4. "No external requests. Poki blocks all external requests by default. Bundle fonts, assets, and libraries into your build."
5. "No branding or external ads. Remove splash screens and outgoing links; your studio logo is welcome on the loading screen."
6. "No ad block prevention. Your game must stay playable with an ad blocker active."

Read the Terms & Conditions for developers before uploading (https://developers.poki.com/guide/adding-your-game).

### 3.2 File size and load time
- **Budget:** "for a good web game the initial download should not exceed 5MB and 8MB in total." (https://developers.poki.com/guide/web-engine)
- "Players tend to move to another game if loading takes more than 10 seconds … Keep the initial download even smaller with progressive loading." (https://developers.poki.com/guide/requirements-quality)
- Progressive loading: "download only the essentials first (menu, tutorial, first stage) and fetch the rest in the background … one of the most important techniques for success on the web. Drop-off during loading is brutally underestimated." Also show a loading bar (https://developers.poki.com/guide/easy-access).
- Cost per megabyte: "For every extra megabyte a person has to download to play your game, you're going to lose a couple percent of players." (Erik Dubbelboer, https://poki.com/blog/building-web-browser-games-2026)
- Case study: Stickman Hook's "WebGL port that was 40MB and had a median loading time of 29.5 seconds" gave "50% conversion to play". Rebuilt in HTML5, it was "6MB … 3.7 seconds … 72%" (https://poki.com/blog/what-makes-high-quality-browser-game).
- Cannon Clash techniques (https://poki.com/blog/how-we-made-cannon-clash-load-fast-and-boosted-conversion):
  - Draco-compressed GLB, "3.88 MB … reduced to just 387 KB".
  - Basis textures, "406 KB down to 46.3 KB".
  - MP3 audio with tuned bitrates.
  - Fewer files: models batched into one GLB, and one UI atlas.
  - Async loading of non-critical assets.
  - Shaders pre-warmed by rendering all materials once in the first frame.
  - Simplified colliders.
  - Themed loading screen with a progress bar.
  - Poki serves gzip/Brotli automatically: "if you are hosting on Poki that's being taken care automatically".
- The Inspector shows "the loading time and file size" and warns about "Image Optimization" (https://developers.poki.com/guide/inspector).

### 3.3 Mobile, portrait and landscape, screen layout
- "A big share of all Poki gameplays are on mobile … Your game can run landscape only, portrait only, or both, but we strongly advise supporting portrait: portrait-playable games see more players enter gameplay on average, and become eligible for Gamebar Display ads" (https://developers.poki.com/guide/easy-access)
- The 2026 blog goes further: "Asking them to rotate their phone is a conversion killer … Every game submitted to Poki needs to work in portrait, and our QA team tests for it." It adds that UI must avoid "phone notches and Poki's own interface elements rendered on top of the game" (https://poki.com/blog/building-web-browser-games-2026). See §7 for the conflict with the docs.
- `dataset:` share of live games that support portrait on mobile (mobile_orientation ∈ {portrait, both}):
  - All 1,503 games: (735 + 145) / 1,503 = **58.5%**.
  - Released 2025-01-01 or later: (333 + 25) / 408 = **87.7%**.
  - Released 2026-01-01 or later: (173 + 9) / 197 = **92.4%**. Only 10 of those 197 are landscape-only and 5 are not on mobile.
  - Rows with null release_date (likely in soft launch): 31 of 32 are "both".
  - **Inference:** portrait support is now close to mandatory in practice.
- Poki Pill overlay: default `movePill(0, 24)`. Size is "46px × 62px on screens narrower than 1211px" and "92px × 64px on screens 1211px wide or wider". It "can't move … lower than 50% of the game area" (https://developers.poki.com/guide/sdk-html5).
- Inspector: a "Desktop and Mobile Mode" toggle (QR code for testing on a real device) and "Scaling Tests" for popular devices (https://developers.poki.com/guide/inspector).
- Fullscreen is case by case. The usual criteria are "Online or local multiplayer modes", "An open world setting", and "Find-the-difference and hidden object games" (https://developers.poki.com/guide/your-game-page).

### 3.4 Input, controls, accessibility
- "Keyboard support: for keyboard-controlled games, implement ESC or spacebar for pause/resume." Also "Adaptive controls: display appropriate control schemes (mobile controls on mobile/tablets, keyboard instructions on desktop)." (https://developers.poki.com/guide/requirements-quality)
- "Players should navigate with mouse and keyboard alike: WASD or arrows through menus, space or return for the primary button." (https://developers.poki.com/guide/engagement)
- Accessibility: "we encourage supporting alternative control methods like mouse only input, drag steering, auto acceleration, or customizable keys." (https://developers.poki.com/guide/content-player-safety)
- Stop page scrolling. Requirement: "prevent game viewport scrolling from affecting the parent page". The snippet calls `preventDefault` on ArrowUp, ArrowDown, Space, and wheel (https://developers.poki.com/guide/requirements-quality, https://developers.poki.com/guide/sdk-html5).
- Blog evidence:
  - Players "had no idea what a space bar was". The fix was to show a keyboard image with the key highlighted (https://poki.com/blog/building-web-browser-games-2026).
  - OnRush found players' mouse leaving the game area and "clicking another game thumbnail unintentionally". Locking the mouse "bumped the engagement from 2 minutes to 10 minutes almost overnight" (https://poki.com/blog/higher-success-rates-with-playtests).

### 3.5 Performance
- Tech check covers "stable frame rates" (https://developers.poki.com/guide/what-we-look-for). "Excessive load size or poor performance" is a common reason to decline (https://developers.poki.com/guide/content-player-safety).
- Unity runtime tips: "Pool your game objects", "Spread CPU-intensive actions over multiple frames", "raycast once every 10 frames" (https://developers.poki.com/guide/sdk-unity).
- WebGPU: "As of June 2026, devices with WebGPU support account for around 68% of players on Poki … treat WebGPU as an enhancement rather than assume it is available to every player." WebGL "remains widely supported, including on many older Android devices" (https://poki.com/blog/building-web-browser-games-2026).

### 3.6 SDK events (required for web fit test and every release)
Sources: https://developers.poki.com/guide/sdk-overview, https://developers.poki.com/guide/requirements-quality, https://developers.poki.com/guide/sdk-html5.

- **Load:** add `<script src="https://game-cdn.poki.com/scripts/v2/poki-sdk.js">`, call `PokiSDK.init()`, and load the game even if init fails.
- `gameLoadingFinished()`: "Required to track loading and show your conversion to play."
- `gameplayStart()`: "must fire on the player's first input (not on load)".
- `gameplayStop()`: "must fire on any gameplay interruption (pause, menu open, level end, cutscene)".
- **No doubles:** "SDK events should not fire twice in succession", e.g. "a gameplayStart() cannot follow another gameplayStart()".
- **Nothing during ads:** "It should not be possible to fire any SDK events during midrolls or rewarded videos."
- `commercialBreak()`:
  - "must fire only when exiting a pause and heading back into gameplay". Closing a pause menu into gameplay is correct. Going from gameplay into level select is wrong.
  - Edge case: "'Dress-up' games may fire commercialBreak() when swapping clothing categories."
  - The docs recommend "calling commercialBreak() before every gameplayStart(), whenever the player has shown intent to continue playing". "Not every commercialBreak() triggers an ad".
- `rewardedBreak()`:
  - "fire on the player's explicit choice to watch an ad for a reward. Make it clear beforehand that an ad is coming."
  - Only grant the reward on `success`.
  - "A rewarded break resets the ad timer".
- **Event order:**
  - Startup: `gameLoadingFinished → gameplayStart`.
  - Death and restart, next level, pause/unpause: `gameplayStop → commercialBreak → gameplayStart`.
  - Death and revive: `gameplayStop → rewardedBreak → gameplayStart`.
  - A menu-only ad (e.g. unlocking a skin) needs no stop/start around it.
- **During ads:** "Make sure that audio and keyboard input are disabled during commercial breaks".
- **Other SDK calls:**
  - `shareableURL()` and `getURLParam()`: URL params are prefixed with `gd`.
  - `movePill()`.
  - `openExternalLink()`.
  - `measure()` for Game Events.
  - `login()`, `getUser()`, `getToken()` for accounts.
  - Defold also exposes `happy_time(value)`.
  - Upload builds via the "poki-cli" (https://developers.poki.com/guide/sdk-overview).
- **The dashboard these events unlock:** Playing Users, Engagement, Earnings, an "Error Scanner" (past 24 h, updated hourly), and Player Feedback (https://developers.poki.com/guide/sdk-overview).

### 3.7 Ads and monetization rules
Sources: https://developers.poki.com/guide/requirements-quality, https://developers.poki.com/guide/monetization, https://developers.poki.com/guide/how-monetization-works.

**Only Poki ads, only ads:**
- "In-app purchases are not available. Poki's ad system is the only form of monetization."
- "No internal purchases: remove any in-game UI elements for purchasing currency or disabling advertisements."
- Third-party ad systems "will not pass review".

**Ad frequency is Poki's job:**
- "do not implement internal ad timers, rely on Poki's system to manage ad frequency".
- "One-per-reward: don't require players to watch multiple consecutive videos for a single reward."

**Rewarded-button hierarchy (all mandatory):**
- "there must always be a standard continue button as an alternative to a 🎬 rewarded one".
- "standard and reward options appear simultaneously".
- "standard button equal or larger size than reward button".
- "standard button positioned next to or above reward button".
- "rewarded buttons cannot use green color".
- "all reward buttons include prominent 🎬 icons".

**No reward-walling:** "Rewarded videos are an optional extra, never a gate. If a player has to watch an ad to progress, it isn't a reward, and it won't pass review."

**Ad blockers:** "When a blocker is detected during a rewarded break, don't grant the reward". Also: "avoid displaying custom 'ad blocked' messages".

**Economy design:**
- "Dual economies such as gems-plus-coins are a mobile pattern built to drive in-app purchases … grind is one of the fastest ways to lose a web player."
- "one understandable currency, clear rewards, and no secondary currencies".

**Rewarded patterns that work:**
- "A helping hand": revives, level skips, hints, stat boosts, speed-ups.
- In-game economy: multipliers and direct coin unlocks.
- Customization: cosmetics and feature unlocks.
- "Unlimited rewarded videos are allowed, but set limits that protect your balance and progression." Use dynamic, time-limited offers, plus "weekly and seasonal unlocks".

**Midrolls vs rewarded:**
- Midrolls run "between levels, after a game over, when leaving a pause".
- Portrait support unlocks "Gamebar Display ads, a mobile format in the title bar that earns extra without any work from you".
- "Prioritize fun If players aren't engaged, no ad strategy will save the numbers."

**Soft-release monetization target:** "at least 1 ad per daily active user" (https://developers.poki.com/guide/release-process).

**Proving rewarded offers:** use Game Events to measure offer `visible`/`interact`. "Do not send measure() events that duplicate ad impressions or completions." (https://developers.poki.com/guide/game-events)

### 3.8 External links and privacy policy
- "Any buttons that open external links … are required to fire the following SDK rather than directly leading to the URL. PokiSDK.openExternalLink('URL');" (https://developers.poki.com/guide/requirements-quality)
- "If your game links externally (even for analytics exemptions), include an in-game, accessible Privacy Policy UI and provide us a hosted policy URL (no Google Doc links)." (same URL)

### 3.9 Saving, cloud save, user accounts
- **Save system (required):** "implement progress saving where appropriate, or clearly inform players when progress won't be saved upon exit." (https://developers.poki.com/guide/requirements-quality)
- **Cloud gamesaves** (https://developers.poki.com/guide/accounts):
  - Automatic for logged-in users: "no extra SDK calls or setup are required".
  - Synced from "localStorage and IndexedDB".
  - Exclude local-only data by prefixing it with `poki_ignore`.
  - **Limit:** "The gamesave payload must not exceed 1MB after gzip compression. If a player's save exceeds this limit, cloud gamesaves are automatically disabled for that player".
- Blog context: saves survive "browser cookie purges (Safari on mobile is particularly aggressive about clearing storage from iframed content)" (https://poki.com/blog/building-web-browser-games-2026).
- **User accounts** (https://developers.poki.com/guide/accounts):
  - `login()`: call "Only … in response to a user interaction that requires an account; avoid calling it automatically on game load". A successful login triggers "a full page refresh", and the call rejects after 45 s.
  - `getUser()` returns `{username, avatarUrl}`. It "Throws an exception if User Accounts is not enabled, or if the user has opted out".
  - `getToken()` returns a JWT that "expires after 1 minute". Verify it server-side at `https://user-vault.poki.com/auth/verify-token` with an `X-Poki-Team-Api-Key` (from your account manager) to get an immutable per-game `user_id`.
- **External account systems are banned:** "No email-based logins, no Google or Facebook sign-in." (https://developers.poki.com/guide/external-resources-policy)

### 3.10 Localization
- The requirements list localization as "recommended for text-heavy games" (https://developers.poki.com/guide/requirements-quality).
- Preparation: keep "all text in one place (a single .json file, for example)".
- Genres that benefit most: "story games, clicker and idle games, quiz games, and anything where mechanics, items, or powerups are explained through text".
- **Language priority:**
  1. EFIGS, and "We recommend adding Turkish to this first batch".
  2. CJK "when you're confident it's worth it".
  3. "Brazilian-Portuguese, and Russian".
- Best display: "detect the player's browser language and serve the game in it automatically". (https://developers.poki.com/guide/localization)
- Languages can be added after release (https://developers.poki.com/guide/post-release-updates).

### 3.11 Easy access, onboarding, engagement scope
- "Streamlined entry: minimize UI screens and menus, ideally placing players directly into gameplay"; "ensure all cutscenes and introductory sequences are skippable"; "design tutorials that are visual and intuitive rather than text-heavy" (https://developers.poki.com/guide/requirements-quality)
- From https://developers.poki.com/guide/easy-access:
  - "Skip the menu. For first-time players especially, skip splash screens, title screens, and level selects."
  - "A safe beginner environment" (in Subway Surfers "players can't die during onboarding").
  - "Explain with visuals … English text excludes a lot of our global audience."
  - "Introduce gradually."
- **Session design:** "Web players have shorter sessions and return less often than mobile players, so the first session carries most of the weight. Quick, satisfying, repeatable loops of around 3 minutes perform best, and about an hour of content is usually the right scope". Also: "Keep gameplay continuous … games where the player can constantly perform an action outperform games with waiting and downtime." The page's other advice is to congratulate the player, set short- and long-term goals, and ramp difficulty gradually (https://developers.poki.com/guide/engagement).
- Blog: "Web players behave more like TikTok viewers than Steam users … Text-based tutorials fail. Pop-up instructions fail." For a survivor-like game, it suggests starting the player with "the most crazy abilities for … 10 seconds … then take them all away" (https://poki.com/blog/building-web-browser-games-2026).
- Cannon Clash cut its intro animation after playtests showed "players were eager to dive into gameplay right away" (https://poki.com/blog/how-we-made-cannon-clash-load-fast-and-boosted-conversion).

### 3.12 External resources policy
Source: https://developers.poki.com/guide/external-resources-policy.

**Not allowed:**
- Runtime requests to "Google Fonts, externally hosted images or audio, or code libraries on external CDNs like jsDelivr".
- "In-game chat systems".
- "External account systems. Games must not collect personal information."

**Possible exceptions (approval required):**
- "Multiplayer servers: externally hosted game servers are fine once approved by Poki."
- Analytics are "reviewed case by case. Google products (including Google Analytics) cannot be approved."
- Leaderboards are reviewed case by case.

**Approval process:** request it under "Settings → CSP" with the exact links and their use. You must also provide a live privacy policy, "linked inside the game", and then re-upload the build. "Poki can't review or provide example privacy policies".

### 3.13 Content and player safety
Source: https://developers.poki.com/guide/content-player-safety.

- **Why it's strict:** the audience includes kids, and advertisers must be comfortable: "every game needs to be something an advertiser is comfortable placing their brand next to."
- **Out of scope:**
  - "Bullying, abuse, stereotypes, or sexism".
  - "Graphic violence, including open or infected wounds and visible body fluids".
  - "Sustained scary themes".
  - "Sexual content or inappropriate clothing".
  - "Cheating, gambling, alcohol, tobacco, or other offensive material".
- **Fixable vs final:** "light dating mechanics, suggestive jokes, or violent scenes, can often be removed or reframed". "Adult themes and misused IP are rejected immediately."
- **Moderation:** every new version is moderated before testing.
- **Player interaction:** "Chat systems … games can't include them … An emoji system works well".
- **Usernames:** for multiplayer games with username input, "implement strict profanity filtering using the provided bad words list (expand it further for your games)" (https://developers.poki.com/guide/requirements-quality).
- **Player-created content:** no explicit UGC moderation rule was found in the docs. AUDS's stated use case is "Player-built levels shared by code" (§4.6).
  - **Inference:** shared UGC should be structured (levels or tiles, not free text), so it doesn't turn into a messaging channel.

### 3.14 Web engine guidance
Source: https://developers.poki.com/guide/web-engine, unless noted.

- Poki's framing: "HTML5 technology is much stronger for web games and many of the following engines are purpose built for web compared to Unity whose web export needs work."
- The key metric is the empty-project size against the 5 MB initial / 8 MB total budget.

| Engine | Empty project (as stated) | 2D / 3D | Multiplayer (as stated) | Licence | Poki SDK integration | Poki notes |
|---|---|---|---|---|---|---|
| **Defold** | "1.03MB" | 2D-focused; 3D via glTF | Nakama, PlayFab, Colyseus, WebSockets | "completely open source … free" | Official; "Defold is an official Poki partner engine" (https://developers.poki.com/guide/sdk-defold) | Listed first with "🫶" as "Official partner of Poki". Examples: Monkey Mart, Car Parking Jam |
| **Construct 3** | "730KB … unzipped, and 342KB zipped" | 2D; basic 3D | Built-in WebRTC P2P; Colyseus, Firebase, Photon, PlayFab | Paid subscription, no royalties | Community addon by Ossama Jouini | "one of the most accessible engines". Examples: Blumgi Slime, OvO Dimensions, Idle Ants |
| **Unity** | "around 11MB" without optimisation | 2D and strong 3D | Asset Store plug-ins | Free under €100k, then paid | Official template + C# class | "Due to its large initial file size, Unity games are overall less well-suited for the web." C2P "typically … 60 to 65%" (https://developers.poki.com/guide/reading-results). WASM export saves "roughly 30%" (https://developers.poki.com/guide/sdk-unity) |
| **BabylonJS** | "about 132KB compressed" | 3D-first | Colyseus, Netlib | Apache 2.0 | via HTML5 SDK | Temple Run 2, Tunnel Rush |
| **Godot** | "10MB" compressed | 2D and 3D | Plug-ins | "open source … licenses are free" | Community plugin by vkrishna, "works for Godot 3.4 and above" (https://developers.poki.com/guide/sdk-godot) | "For exclusive export to the web, we recommend using the latest version of Godot 3.5." Same blob issue as Unity; lazy-loading is in progress (https://poki.com/blog/building-web-browser-games-2026) |
| **PlayCanvas** | "300kb" | 2D and 3D | Multiple back-ends | Open-source engine, subscription features | via HTML5 SDK | "doesn't compile to WebAssembly, it sidesteps the blob problem entirely" (https://poki.com/blog/building-web-browser-games-2026). Venge.io, Cannon Clash |
| **PixiJS** | "130KB" | 2D renderer (3D via Pixi3D) | Colyseus examples | MIT | via HTML5 SDK | Subway Surfers, Stickman Hook |
| **Phaser** | "290KB" | 2D | Colyseus, Firebase, Socket.io, Nakama | MIT | "official Poki Phaser plugin" that auto-fires events and auto-requests commercialBreak (https://developers.poki.com/guide/sdk-phaser) | Stick Merge, Raft Wars |
| **Cocos Creator** | "709kb" | 2D and 3D | Third-party | Free | Community plugin by vkrishna, "Cocos Creator 3.4.0 and above only" | Merge Arena |
| **Stencyl** | "500KB" | 2D only | "does not support online multiplayer" | Web free | n/a | "limited functionality for portrait orientation". Level Devil |
| **GameMaker** | "450-550kb" | 2D | Native plus extensions | Pro licence needed to commercialise | Extension by YellowAfterLife | Retro Bowl |
| **Three.js** | "151KB" (122 KB Brotli) | 3D library | DIY | MIT | via HTML5 SDK | No native touch or scaling, so "These need to be programmed in". Narrow.One |
| **LayaAir** | "2.1MB" | 2D and 3D | HTTP/WebSocket | MIT | via HTML5 SDK | Parkour Race |
| **Wonderland** | "3.2 MB (1.6 MB gzipped)" | 3D only | Any web framework | Free to $120k/yr, then 10% royalty | via HTML5 SDK | "not a good fit for 2D games" |
| **GDevelop** | not listed on the web-engine page | 2D | n/a | Open source | "GDevelop has a built-in Poki export option" (https://developers.poki.com/guide/sdk-gdevelop) | n/a |

Blog summary (2026): "Unity is the most widely used engine among developers on our platform … That makes conversion to play lower for Unity games than for web-native alternatives." Also: "Construct is another strong web-native option. Phaser and PixiJS sit at the framework end" (https://poki.com/blog/building-web-browser-games-2026).

**Unity mandatory-ish settings** (https://developers.poki.com/guide/sdk-unity):
- "Explicitly Thrown Exceptions Only", compression "Disabled", "Name Files As Hashes" ON, Strip Engine Code ON, Managed Stripping "high".
- Enable Data Caching.
- LZ4 asset bundles, crunch compression "92", mono audio.
- The Unity index.html is rewritten on upload. Custom HTML must sit inside `<!-- poki include body -->`.

**Inspector** (https://developers.poki.com/guide/inspector): QA Module Checklist, Event Log, file size and load time, Desktop/Mobile mode, Scaling Tests. Warnings cover "External Resources", "Image Optimization", and "Unexpected Behavior Detected".

---

## 4. Business terms and developer tools

### 4.1 Deal types and exclusivity
Sources: https://developers.poki.com/guide/revenue-deal-types, https://developers.poki.com/guide/working-with-poki.

- **Web exclusive** (the preferred model):
  - Exclusive on "Browser / open web", "Discord", "YouTube Playables" ("Discord and YouTube Playables run HTML5 in a browser, so they count as web").
  - Yours to publish elsewhere: "Steam", "Mobile app stores", "Consoles".
  - "By default, exclusive deals run for 5 years."
  - What Poki invests: marketing, "top-tier ad partners and brand deals", and a revenue share on the players it brings.
  - Caveat: "The specifics above (the 5-year term, the revenue share, the exact investment) are indicative. The real terms depend on the game and are set out in your agreement."
  - "you can't publish the same game on other web portals or aggregators".
- **Non-exclusive:** "For games already live on other web platforms, or with a more niche or short-term fit for our audience, we can offer a one-time flat license fee instead, with no revenue share."
  - **Inference:** a game already on CrazyGames, itch web builds, etc. loses the rev-share and marketing path.

### 4.2 Revenue split
"If a user comes to your game directly, through bookmarks, search, social media or through your own community, you get 100% of the revenue for that user. If a user comes to your game through Poki.com, or through a marketing effort from Poki, then Poki splits the revenue 50/50 with you" (https://developers.poki.com/guide/working-with-poki).

### 4.3 Payouts
- "Poki pays out via wire transfer or PayPal, in your preferred currency". Billing is set under "Team settings → Billing", and "Billing information can't be changed during a payment cycle".
- "The lever you control is performance: engagement drives ad impressions, and correctly implemented SDK events make sure every opportunity counts." (https://developers.poki.com/guide/payouts-billing)
- The docs don't publish the payment-cycle length or a minimum payout.

### 4.4 P4D platform
- Two team roles: "Developer", and "Developer Support", which has no access to earnings after release.
- Game tabs: Versions (Inspector and Preview), Playtests, Settings, Thumbnails.
- "Suggested categories & description: Here you can pick up to four categories". Poki rewrites the description for SEO.
- "Once a game is live on Poki, all thumbnail updates will need to be reviewed by our team." (https://developers.poki.com/guide/p4d-platform)

### 4.5 Post-release expectations
Source: https://developers.poki.com/guide/post-release-updates.

- "When you spot a bug or performance problem, fix it fast".
- "better tech, engagement, or monetization metrics across the board make your game eligible for more promotion".
- "Once your game has been live for a while, a content update is a great way to attract new players and bring existing ones back. New characters, levels, worlds".
- "For anything bigger than routine updates, like a major content drop, a sequel, or a change in direction, talk to your Poki contact first."
- Updates follow the QA flow: "upload a new build and request a review. Once approved, the developer support team will publish your updated version." (https://developers.poki.com/guide/release-process)
- Submission-time signal: "a roadmap/update plan shared at submission" (https://developers.poki.com/guide/what-we-look-for).

### 4.6 Tools and what they enable

| Tool | What it enables | Key constraints | Source |
|---|---|---|---|
| **Game Events** (`PokiSDK.measure(category, what, action)`) | Progress funnels (`start`/`complete`/`fail`), interaction events (`visible`/`interact`), custom events, and saved custom Funnels in P4D, compared across versions. Ad playback is tracked automatically | "Do not use / or ^" in values. For one attempt, send complete or fail, "never both". Don't duplicate ad events. Usable before release: "During development and testing, it can help validate player flows" | https://developers.poki.com/guide/game-events, https://poki.com/blog/game-events-new-tool-for-understanding-your-players |
| Game Events case studies | Satisbox Mini Games reordered content by drop-off and average session went "from 4:50 to 5:43" then "6:23". Smash Room tested three openers at the 3-minute mark ("Glass: 33.7%", "Cake: 27.4%", "Phone: 23.8%"). Stickman Fury found a bug after stage 56 | n/a | https://poki.com/blog/game-events-new-tool-for-understanding-your-players |
| **Player device report** | "an overview of the various hardware and devices currently used by players on Poki. It is updated daily." (September 2026 edition) | Charts load client-side ("Loading report data…"). The numbers were **not** captured in this crawl | https://developers.poki.com/guide/player-device-report |
| **AUDS** (Arbitrary User Data Store) | "Your game sends data to AUDS and receives a short code in return. Any player with that code can retrieve the data". Use cases: "Player-built levels shared by code", "Leaderboards", "Turn-based or asynchronous multiplayer state". Also public counters via `_increment` | "AUDS is currently a prototype, and your game needs to be live on Poki to use it." The create call returns a `secret` that "is never returned again". List `limit` max 100. The example shows `expires_in: 31536000` (1 year) | https://developers.poki.com/guide/auds |
| **Netlib** (`@poki/netlib`) | "A peer-to-peer library for web games using WebRTC data channels for direct UDP connections". "No server costs", "No double implementation", "Lower latency". Built-in lobby system with filtering. TURN fallback. Poki hosts signaling, STUN and TURN "for free" | "Netlib is still under development and considered a beta … the API can change." Open source, and doesn't require Poki. Defold integration by IndieSoft | https://developers.poki.com/guide/netlib |
| **User accounts + cloud saves** | Cross-device progress with no integration. Optional identity via JWT to your own backend | 1 MB gzip save cap; token lasts 1 min | https://developers.poki.com/guide/accounts |
| **Playtesting / fit tests** | Free, repeatable, audience chosen by category | See §1 | https://developers.poki.com/guide/playtesting |
| **Inspector / poki-cli** | QA checklist, event log, device scaling; CLI uploads from CI | n/a | https://developers.poki.com/guide/inspector, https://developers.poki.com/guide/sdk-overview |

**Inference:** Netlib (free P2P with lobbies) plus AUDS (share codes and leaderboards) lets a small team ship light multiplayer, async multiplayer, or level-sharing without running servers. But the web fit test's limited traffic means real-time multiplayer needs bots to pass (§1.2).

---

## 5. Thumbnail and game page guidance

### 5.1 Static thumbnail (required before the player fit test; drives CTR)
Source: https://developers.poki.com/guide/game-thumbnail.

- **Spec:** "Deliver a full-bleed* square of at least 628x628px. We apply the rounded corners on our end." "No borders, padding, or letterboxing."
- **Content:**
  - "Show what's inside … Include your main character in their default skin".
  - "One clear foreground object … not a collage".
  - "Give it motion", e.g. mid-jump.
  - "Keep a series together".
- **Legibility:**
  - "Design for small tiles too".
  - "Avoid text … Poki's own tests show players prefer text-free thumbnails".
  - "the Poki playground background is #83FFE7, so avoid colors too close to it".
- **Effect on metrics:** the thumbnail's "main job is click-through rate". "C2P is mostly a technical story". On mobile, "the thumbnail is displayed once more after the player clicks", so a mismatch hurts.
- **Update rules:** changes are free during development "unless a web fit test is running". After passing the web fit test, changes "need sign-off". "After release, we only change thumbnails when the game ships a substantial content update".
- **AI rule:** "Match the art style of the actual game … Don't: … misleading art that isn't the game" (https://developers.poki.com/guide/content-player-safety).
- **Soft release:** thumbnail A/B tests are run during soft release (https://developers.poki.com/guide/release-process).

### 5.2 Animated thumbnail (required before global release; added in soft release)
Source: https://developers.poki.com/guide/your-game-page.

- **Spec:**
  - "1080 x 1080 or higher", "1:1 (square)".
  - "50fps or higher", "4 to 6 seconds".
  - Audio "Muted", format ".mp4", "Max file size 100MB".
- **Content:**
  - "Focus on gameplay".
  - "Minimal text".
  - "2 to 3 scenes of about 1 to 2 seconds each".
  - "Start from your static artwork and animate from there".
  - "center your action since the square crop trims the edges".
  - "Remove the cursor".
- The requirements page repeats: "all games must include both static and animated thumbnails for global release" (https://developers.poki.com/guide/requirements-quality).

### 5.3 Game page
- Description: "Tell us a bit about the main game mechanic and what makes your game stand out. We'll use this as input while making sure your game has a search engine optimized description" (https://developers.poki.com/guide/p4d-platform).
- Name: must not be "Intentionally similar to ride search terms" (https://developers.poki.com/guide/content-player-safety).
- Fullscreen: case by case (§3.3).
- Unity loader: "add up to 4 images to the screenshots folder … they'll show up in the loader automatically" (https://developers.poki.com/guide/sdk-unity).

---

## 6. Poki-readiness checklist (35 verifiable items)

**A. Concept and content**

| # | Item (pass = yes) | How to verify | Source |
|---|---|---|---|
| 1 | The concept offers "a mechanic, setting, or angle not already well-represented on Poki" | Search Poki categories and the catalog for near-duplicates; write down the differentiator in one sentence | https://developers.poki.com/guide/content-player-safety |
| 2 | Passes the six-dimension clone test (art, core mechanics, progression/economy, UI/audio, characters, name/thumbnail) | Side-by-side against the closest 3 Poki games | https://developers.poki.com/guide/content-player-safety |
| 3 | No out-of-scope content (bullying, graphic violence or blood, sustained scary themes, sexual content, gambling, alcohol, tobacco); no third-party IP; no parody of a real title | Content review before the first upload (moderation checks every version) | https://developers.poki.com/guide/content-player-safety |
| 4 | No chat. Player expression is emoji-only. Username input, if any, has strict profanity filtering | Code review | https://developers.poki.com/guide/external-resources-policy, https://developers.poki.com/guide/requirements-quality |
| 5 | AI use is documented (tools, prompts, iterations). No watermarks or prompt text. All generated levels and dialogue are hand-reviewed and playtested | Keep a production log | https://developers.poki.com/guide/content-player-safety |
| 6 | A roadmap or update plan (content hooks, systems that support updates) is ready to share at submission | Doc exists | https://developers.poki.com/guide/what-we-look-for |

**B. Platform and technical**

| # | Item (pass = yes) | How to verify | Source |
|---|---|---|---|
| 7 | Works on desktop, mobile and tablet. Mobile controls are forced on tablets | Inspector Desktop/Mobile mode plus real devices | https://developers.poki.com/guide/requirements-quality |
| 8 | Playable in portrait on mobile (docs "strongly advise"; the 2026 blog says QA tests for it). UI stays clear of notches and the Poki Pill | Inspector Scaling Tests | https://developers.poki.com/guide/easy-access, https://poki.com/blog/building-web-browser-games-2026 |
| 9 | Desktop scales to 16:9 and covers the full canvas at 640x360, 836x470 and 1031x580 | Inspector Scaling Tests | https://developers.poki.com/guide/requirements-quality |
| 10 | Initial download ≤ 5 MB and total ≤ 8 MB | Inspector "file size"; browser Network tab | https://developers.poki.com/guide/web-engine |
| 11 | Progressive loading (essentials first) plus a visible loading bar. Load time well under 10 s | Inspector "loading time" on throttled mobile | https://developers.poki.com/guide/easy-access, https://developers.poki.com/guide/requirements-quality |
| 12 | Zero external requests. Fonts, assets and libraries are bundled. Any server, analytics or leaderboard is approved via Settings → CSP. No Google Analytics | Inspector "External Resources" warning is empty | https://developers.poki.com/guide/external-resources-policy |
| 13 | Playable in incognito (every localStorage call is wrapped in try/catch) | Test in a private window | https://developers.poki.com/guide/requirements-quality |
| 14 | Fully playable with an ad blocker. No custom "ad blocked" message. No reward when the ad fails | Test with uBlock | https://developers.poki.com/guide/requirements-quality |
| 15 | No splash screens, outgoing links or other ad SDKs. Studio logo appears only on the loading screen. Debug tools removed | Build review | https://developers.poki.com/guide/requirements-quality |
| 16 | Arrow keys, Space and mouse wheel don't scroll the parent page | Preview mode on a long page | https://developers.poki.com/guide/sdk-html5, https://developers.poki.com/guide/requirements-quality |
| 17 | Keyboard games pause and resume on ESC or Space, with correct SDK events. Menus are navigable with WASD/arrows and Space/Enter | Manual test plus Event Log | https://developers.poki.com/guide/requirements-quality, https://developers.poki.com/guide/engagement |
| 18 | Progress saves to localStorage/IndexedDB (or players are told it won't). Save payload < 1 MB gzipped. Caches use the `poki_ignore` prefix | Measure save size | https://developers.poki.com/guide/requirements-quality, https://developers.poki.com/guide/accounts |

**C. SDK integration**

| # | Item (pass = yes) | How to verify | Source |
|---|---|---|---|
| 19 | `gameLoadingFinished()` fires once, when loading completes | Inspector Event Log | https://developers.poki.com/guide/sdk-overview |
| 20 | `gameplayStart()` fires on first input (not on load). `gameplayStop()` fires on every pause, menu, level end, death and cutscene. Never two of the same in a row | Inspector Event Log | https://developers.poki.com/guide/requirements-quality |
| 21 | `commercialBreak()` fires only when heading back into gameplay (restart, next level, unpause). No SDK events fire during ads. Audio is muted and input disabled during ads | Event Log plus manual | https://developers.poki.com/guide/requirements-quality, https://developers.poki.com/guide/sdk-html5 |
| 22 | `rewardedBreak()` fires only on an explicit player choice. The reward is granted only on success, exactly once, and applied automatically | Manual | https://developers.poki.com/guide/sdk-html5, https://developers.poki.com/guide/requirements-quality |
| 23 | Every Inspector QA module is checked, and there is no "Unexpected Behavior Detected" warning | Inspector | https://developers.poki.com/guide/inspector |
| 24 | Game Events `measure()` covers at least the tutorial/level funnel and every rewarded offer (`visible`/`interact`) | P4D Game Events view | https://developers.poki.com/guide/game-events |

**D. Monetization UX**

| # | Item (pass = yes) | How to verify | Source |
|---|---|---|---|
| 25 | Every rewarded offer has a standard option shown at the same time, at equal or larger size, positioned next to or above it. The rewarded button is not green and carries a 🎬 icon | UI review | https://developers.poki.com/guide/requirements-quality |
| 26 | No reward-walling, no internal ad timers, one video per reward, no IAP or "remove ads" UI, single currency | Design review | https://developers.poki.com/guide/requirements-quality, https://developers.poki.com/guide/monetization |
| 27 | External links go through `PokiSDK.openExternalLink()`. If any external service is used, an in-game privacy policy links to a hosted URL (not a Google Doc) | Code review | https://developers.poki.com/guide/requirements-quality |

**E. First session and design**

| # | Item (pass = yes) | How to verify | Source |
|---|---|---|---|
| 28 | First-time players land directly in gameplay: no title, splash or level-select screen. All cutscenes are skippable | Playtest recordings | https://developers.poki.com/guide/easy-access, https://developers.poki.com/guide/requirements-quality |
| 29 | The tutorial is visual (images, gestures), not text. Mechanics are introduced gradually. The first level can't be failed, or failure is trivial | Playtests: no quits in the first minute | https://developers.poki.com/guide/easy-access |
| 30 | The core loop is about 3 minutes and continuous (no waiting). About 1 hour of content at launch | Design doc plus player fit test histogram | https://developers.poki.com/guide/engagement |
| 31 | All text lives in one file. If text-heavy: EFIGS + Turkish, with automatic detection of browser language | Code review | https://developers.poki.com/guide/localization |
| 32 | Multiplayer only: lobbies fill during the low-traffic web fit test (bots or existing servers). External servers are approved | Test with 1 human | https://developers.poki.com/guide/web-fit-test, https://developers.poki.com/guide/external-resources-policy |

**F. Store assets and metric gates**

| # | Item (pass = yes) | How to verify | Source |
|---|---|---|---|
| 33 | Static thumbnail: full-bleed square ≥ 628×628, no text, no border, one dynamic foreground subject (main character in default skin), contrast against #83FFE7, matches the game | Check at small tile size | https://developers.poki.com/guide/game-thumbnail |
| 34 | Animated thumbnail: .mp4, ≥ 1080×1080, 1:1, ≥ 50 fps, 4–6 s, muted, ≤ 100 MB, 2–3 scenes, no cursor, starts from the static art | File properties | https://developers.poki.com/guide/your-game-page |
| 35 | Metric gates. Player fit test: average > 3 min and ≥ 25% of plays > 3 min (target 5+ min; 10+ for management/sim). Web fit test: ≥ 3/5 on CTR, time on page and C2P versus the category, with C2P ≥ 65% (Poki average ~70%) | P4D results | https://developers.poki.com/guide/player-fit-test, https://developers.poki.com/guide/how-testing-works, https://developers.poki.com/guide/web-fit-test |

---

## 7. Discrepancies, gaps and caveats
1. **Web fit test duration.** "Takes roughly 7 days (sometimes longer when it's busy)" (https://developers.poki.com/guide/how-testing-works) vs "The test takes about 3 to 5 days" (https://developers.poki.com/guide/web-fit-test). Plan for 7.
2. **Recordings per playtest.** The docs say "10 recordings" (https://developers.poki.com/guide/playtesting). The June 2026 blog says "10 to 20 recordings" (https://poki.com/blog/building-web-browser-games-2026).
3. **Portrait.** The docs allow "landscape only, portrait only, or both" but "strongly advise" portrait (https://developers.poki.com/guide/easy-access). The June 2026 blog says "Every game submitted to Poki needs to work in portrait, and our QA team tests for it." Both the dataset trend (92.4% of 2026 releases support portrait) and the blog point toward treating portrait as required.
4. **No published web fit test pass cutoff.** Only "A 3 means you're at or above the category average". The metrics are "weighted equally".
   - **Inference:** a combined score around ≥ 3 is the practical target. A weak metric can probably be offset by others, but that is not stated.
5. **Final-review rejection is per game and final.** "It is therefore not possible to publish your game on the Poki platform." The content policy says "We only reconsider after significant improvement". So a "fixable" content or originality issue can be reconsidered, but a "no fit" verdict is final for that title.
6. **Deal terms are indicative.** The 5-year exclusivity and 50/50 split are "indicative … set out in your agreement". The payout cycle and minimum payout are not published.
7. **Player device report numbers** are loaded client-side and were not captured. Mobile share appears only as "majority mobile" (https://developers.poki.com/guide/what-we-look-for) and "A big share of all Poki gameplays are on mobile" (https://developers.poki.com/guide/easy-access).
8. **The P4D access form marks prior-game links "Required"** (https://developers.poki.com/guide/share).
   - **Inference:** a first-time team with no shipped games should bring a playable prototype or a jam game link.
9. **The GDC 2024 blog is dated.** It says "60 million players each month", and playtesting was then "exclusive, early access". Playtesting is now open to all P4D users (https://poki.com/blog/poki-at-gdc-2024-introducing-poki-playtesting vs current docs).
10. **Engine sizes are Poki's own "empty project" figures**, measured differently per engine (zipped, unzipped, compressed). They are not directly comparable.
