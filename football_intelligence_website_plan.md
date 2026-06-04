# Football Intelligence Website Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build Ashtryx into a global football intelligence website that people want to revisit because it is genuinely useful, fast, polished, and visually memorable. The first plan priority is product quality: sharp football intelligence, high visual energy, fast scanning, original analysis, reliable data presentation, and polished Motion-powered interactions around FIFA 2026, match analysis, and team/player data.

**Architecture:** Use a structured football-data product model rather than a simple blog, but design it mobile-first before expanding into a desktop command-center layout. Start with SEO-friendly pages for competitions, matches, teams, players, and articles, then connect API-backed stats through a cache-aware provider layer once the core site is live.

**Tech Stack:** Next.js, TypeScript, PostgreSQL, Prisma, Tailwind CSS, Motion, UI UX Pro Max design guidance, football data API, and Google Search Console.

## Live Data Sources

Use a source-per-service approach so the app can mix free and paid providers without tying the whole product to one vendor.

- **News / editorial context:** `The Guardian Open Platform`, `New York Times APIs`, `NewsAPI` for development or fallback use, and RSS feeds from trusted publishers where permitted. Use `GDELT` only for event monitoring, topic discovery, source clustering, and trend signals; do not treat it as clean editorial content.
- **Live football scores / fixtures:** `API-Football` / `API-SPORTS`, `SportsDataIO`, `TheSportsDB`, `SportMonks`, and official league or federation endpoints where available.
- **Weather / match conditions:** `Open-Meteo` or a similar free weather API.
- **Odds / betting context if added later:** a dedicated odds API such as `The Odds API` or another licensed provider with a usable free tier.
- **Alerts / incident monitoring if added later:** `GDELT` plus domain-specific public feeds, not scraped news HTML.

---

## Research Basis

- FIFA World Cup 2026 runs from June 11, 2026 to July 19, 2026, with official fixtures, venues, and host-city pages available from FIFA.
- WhoScored-style value comes from match centers, player ratings, team strengths/weaknesses, tactical profiles, lineups, live stats, and repeatable comparison pages.
- Website quality depends on original analysis, non-replicated pages, clear navigation, useful football data, strong mobile performance, trustworthy sourcing, and a distinctive editorial voice.
- Google Search guidance prioritizes helpful, reliable, people-first content; Ashtryx should not rely on thin AI-generated pages, copied summaries, or keyword-volume content without original football judgment.
- FIFA and other football rights holders claim ownership over marks, logos, event branding, platform content, photos, graphics, feeds, and API content; Ashtryx must define a rights-safe asset and data policy before using official badges, player photos, league logos, or proprietary data feeds.
- Football APIs such as `API-Football`, `SportsDataIO`, `SportMonks`, and official league endpoints can provide fixtures, results, standings, lineups, match stats, player stats, odds, and xG through JSON.
- GDELT is useful for monitoring global events, topics, entities, language, tone, and source clusters; it is not a substitute for clean sports reporting or original editorial work.
- UI UX Pro Max recommends a data-dense dashboard direction for analytics-heavy products: compact grids, KPI cards, data tables, chart zoom, row highlighting, smooth filtering, and strong contrast.
- Motion should be used for meaningful page load, state change, filtering, and chart interactions while respecting `prefers-reduced-motion`.

## Product Differentiation

Ashtryx must earn attention through a clear product angle before implementation expands.

- **Positioning:** football intelligence for fast match understanding, not another live-score clone.
- **Differentiator:** combine match state, tactical notes, form signals, player watchlists, and editorial judgment into concise "what matters now" views.
- **Against live-score apps:** avoid competing only on score speed. Compete on explanation, context, and readable decision signals.
- **Against analytics databases:** avoid overwhelming users with raw tables. Convert data into ranked insights, tactical summaries, and player/team narratives.
- **Against news sites:** avoid generic match previews. Build repeatable intelligence pages tied to entities: teams, players, fixtures, venues, groups, and tournaments.
- **MVP promise:** a user should understand a match, team, or player in under 90 seconds on mobile.

## UI/UX Direction

Use UI UX Pro Max as the design-system source for the first implementation pass.

- **Product feel:** premium football intelligence, not a generic sports blog. The interface should feel like a live command center for FIFA 2026, teams, players, and match decisions.
- **Primary pattern:** mobile-first intelligence feed that expands into a data-dense dashboard on tablet and desktop. Prioritize fixtures, match signals, team form, ratings, tactical notes, and article links above marketing copy.
- **Visual style:** modern sports analytics, compact but dramatic. Use strong section rhythm, large match moments, tight data cards, and clear hierarchy for scanning.
- **Color system:** use deep blue for data trust, bright blue for active states, amber for decisive calls and CTAs, light neutral surfaces for readability, and a small accent set for team/status differentiation. Avoid a one-note blue UI by adding controlled amber, green, red, and neutral states.
- **Typography:** test Fira Sans/Fira Code against at least two more distinctive brand pairings before finalizing. The chosen pair must preserve mobile readability, numeric clarity, and a premium sports identity.
- **Layout:** avoid a marketing landing page. On mobile, the home page opens as a prioritized match intelligence feed; on desktop, it expands into a usable dashboard with top matches, World Cup timeline, analysis cards, team form, player watchlist, and content cluster entry points.
- **Mobile-first rules:** design 375px wireframes before desktop. Replace wide tables with cards, accordions, sticky match context, horizontal stat chips, and drill-down panels. Do not ship a page whose primary value requires side-by-side desktop columns.
- **Charts:** use line charts for form trends, bar charts for ranking comparisons, radar charts for team/player profiles, and streaming/ticker patterns only for live match states.
- **Controls:** use tabs for page sections, segmented controls for competition/match filters, icon buttons for compact actions, and visible focus states for keyboard navigation.
- **Assets:** use real football-oriented imagery, venue/team/player placeholders, or generated bitmap assets where official assets are unavailable. Do not rely on abstract gradients alone.

## Rights-Safe Data And Asset Policy

Do not assume public availability means commercial reuse is safe.

- **Allowed by default:** original text, original generated or commissioned illustrations, neutral team/country text names, factual match dates/scores when sourced and attributed, and licensed API data within provider terms.
- **Review before use:** club badges, league logos, FIFA marks, tournament emblems, player headshots, broadcast images, scraped statistics, compiled databases, and official feed content.
- **Never scrape as a shortcut:** do not scrape WhoScored, FIFA, UEFA, Premier League, FotMob, Sofascore, or similar sites for data, ratings, images, logos, or page structures.
- **Provider contract check:** before enabling any paid or free API, record whether commercial display, caching, redistribution, attribution, logos, player images, and derived statistics are permitted.
- **Fallback asset system:** use text badges, country flags only where rights-safe, abstract kit-color placeholders, venue silhouettes, generated non-infringing football imagery, and licensed stock imagery.
- **Attribution:** show source attribution where required by API or content licences.
- **Legal review trigger:** if the site uses official logos, event marks, player photos, league branding, odds, or proprietary advanced stats, pause implementation for licence confirmation.

## Caching And Freshness Strategy

Live data must be useful without exhausting API quotas or misleading users with silent staleness.

- **Static content:** use SSG/ISR for articles, guides, team profiles, player profiles, and tournament context. Revalidate on editorial publish or scheduled intervals.
- **Fixtures and standings:** cache server-side with ISR or a persistent cache. Use longer TTLs when no matches are live and shorter TTLs on match days.
- **Live match data:** use a short TTL cache, stale-while-revalidate behavior, and visible `lastUpdated` timestamps. Never poll an upstream API directly from the browser.
- **Rate limits:** centralize provider calls through `src/lib/football/provider.ts`; enforce per-provider backoff, retries, timeout handling, and quota-aware degradation.
- **Fallbacks:** if an API fails, serve the latest cached snapshot with a visible stale-data label rather than empty modules.
- **Manual refresh:** allow editorial/admin refresh hooks later, but keep the public MVP automated and quota-safe.
- **Cache candidates:** start with Next.js fetch caching and ISR; add Redis, Vercel KV, Upstash, or edge cache only when live update volume requires it.

## Content Strategy

Content must be built around repeatable football intelligence, not a thin launch blog.

- **Editorial angle:** every article should answer what matters, why it matters, and what the data changes about the reader's understanding.
- **Content types:** schedule guides, venue guides, group/team previews, tactical explainers, player watchlists, match previews, match recaps, form reports, ratings explainers, and data-methodology notes.
- **Publishing cadence:** target 3-5 substantial pieces per week before launch, then increase around major tournament windows. Keep quality higher than volume.
- **Authorship:** use human-owned editorial judgment. AI assistance may support research drafts, outlines, or formatting, but final pages need human review, original conclusions, fact checks, and source links.
- **Depth standard:** each strategic article needs original commentary, internal links to relevant entities, cited sources, and at least one reusable data or insight module.
- **Cluster target:** replace the six-article launch set with 25-40 high-quality pages across tournament, team, player, venue, and explainer clusters before broad promotion.
- **Quality gate:** do not publish pages that are empty, generic, copied, unreviewed, or created only to target keywords.

## Motion System

Use the installed `motion` package for React/Next.js animations. Motion must make the site feel alive without damaging readability, accessibility, or Core Web Vitals.

- **Page entry:** stagger the first dashboard regions on load: match ticker, hero match panel, intelligence cards, then article links.
- **Navigation:** add quick cross-fade or slide transitions for tab and segment changes. Keep durations between 150ms and 300ms.
- **Data updates:** animate score, rating, form, and stat changes with subtle count or highlight transitions so users can see what changed.
- **Cards and tables:** use row hover highlighting, card lift/shadow feedback, and filter result transitions without causing layout shift.
- **Charts:** animate line/radar/bar chart entrance once, then use hover/tap tooltips and toggles for exploration.
- **Mobile:** prioritize tap feedback and section transitions. Do not depend on hover for important actions.
- **Reduced motion:** every Motion component must respect `prefers-reduced-motion`; disable stagger, parallax, and non-essential transforms for reduced-motion users.
- **Limits:** no infinite decorative animation except loading indicators. Avoid scroll-jacking, excessive parallax, bouncing icons, and animations longer than 500ms for normal UI.

## File Structure

Create these files during implementation:

- `package.json`: app scripts and dependencies.
- `src/app/page.tsx`: home dashboard.
- `src/app/layout.tsx`: root app layout, navigation, metadata base.
- `src/app/globals.css`: global styles and Tailwind entry.
- `design-system/MASTER.md`: UI UX Pro Max design-system source for colors, typography, motion, spacing, and component rules.
- `tailwind.config.ts`: executable design tokens for colors, typography, spacing, screens, radius, shadows, and chart/status values.
- `src/lib/football/cache.ts`: cache policy, TTL helpers, stale-data handling, and provider freshness metadata.
- `src/lib/football/licensing.ts`: provider and asset usage policy records.
- `src/lib/football/sources.ts`: source attribution metadata for API, editorial, and asset providers.
- `src/lib/motion/presets.ts`: shared Motion timing, easing, stagger, and reduced-motion helpers.
- `src/app/competitions/[slug]/page.tsx`: competition hub.
- `src/app/matches/[id]/page.tsx`: match center.
- `src/app/teams/[slug]/page.tsx`: team page.
- `src/app/players/[slug]/page.tsx`: player page.
- `src/app/articles/[slug]/page.tsx`: article page.
- `src/lib/data/seed.ts`: initial football data for FIFA 2026 and sample teams.
- `src/lib/football/types.ts`: shared football domain types.
- `src/lib/football/provider.ts`: football API abstraction.
- `prisma/schema.prisma`: persistent football data model.
- `src/components/football/*`: match, team, player, stat, and article UI components.
- `src/components/motion/*`: reusable animated section, stagger group, stat change, and tab transition wrappers.
- `src/app/privacy/page.tsx`, `src/app/terms/page.tsx`, `src/app/about/page.tsx`, `src/app/contact/page.tsx`: trust, transparency, and site-quality pages.

## Task 1: Create Product Roadmap Document

**Files:**
- Create: `football_intelligence_website_plan.md`

- [ ] Capture the goal, research basis, phased roadmap, page types, quality standards, content plan, data strategy, and launch checklist.
- [ ] Include source links to FIFA, WhoScored reference, and chosen football API candidates.
- [ ] Commit with `docs: add football intelligence roadmap`.

## Task 2: Scaffold The Web App

**Files:**
- Create: `package.json`
- Create: `src/app/page.tsx`
- Create: `src/app/layout.tsx`
- Create: `src/app/globals.css`

- [ ] Initialize a Next.js TypeScript app.
- [ ] Add Tailwind CSS, Motion, and base app structure.
- [ ] Build the first home page as a usable football dashboard, not a marketing landing page.
- [ ] Apply purposeful fonts globally and define CSS variables for the UI UX Pro Max color system.
- [ ] Verify with `npm run lint` and `npm run build`.
- [ ] Commit with `feat: scaffold football intelligence app`.

## Task 3: Create UI UX Pro Max Design System

**Files:**
- Create: `design-system/MASTER.md`
- Create: `tailwind.config.ts`
- Update: `src/app/globals.css`
- Update: `src/app/layout.tsx`

- [ ] Generate or write the Ashtryx design-system source using UI UX Pro Max recommendations for a football intelligence sports analytics dashboard.
- [ ] Define color tokens, typography, spacing scale, border radius rules, chart colors, status colors, and surface hierarchy in both `design-system/MASTER.md` and `tailwind.config.ts`.
- [ ] Test at least three typography directions and record the final choice with rationale for mobile readability, numeric clarity, and brand distinctiveness.
- [ ] Define reusable layout patterns for dashboard, match center, team/player profile, article, and legal/trust pages.
- [ ] Define component rules for cards, tables, tabs, segmented controls, stat badges, match tickers, chart panels, article cards, and trust pages.
- [ ] Define accessibility rules: contrast, focus rings, keyboard navigation, alt text, tap targets, no horizontal mobile scroll, and reduced motion.
- [ ] Verify design intent across 375px, 768px, 1024px, and 1440px viewport targets before implementing page details.
- [ ] Commit with `design: add Ashtryx UI UX Pro Max design system`.

## Task 3A: Produce Mobile-First Wireframes

**Files:**
- Create: `design-system/mobile-wireframes.md`
- Update: `design-system/MASTER.md`

- [ ] Define 375px-first wireframes for home, competition hub, match center, team page, player page, and article page.
- [ ] Convert desktop dashboard regions into mobile feed modules, accordions, drill-down cards, sticky match summaries, and horizontally scrollable stat chips where appropriate.
- [ ] Specify which tables collapse into cards and which chart interactions are available on touch screens.
- [ ] Define mobile information priority for each page: first screen, second screen, expandable details, and related links.
- [ ] Confirm no core page depends on desktop-only side-by-side panels to communicate its primary value.
- [ ] Commit with `design: add mobile-first football wireframes`.

## Task 4: Add Motion System

**Files:**
- Create: `src/lib/motion/presets.ts`
- Create: `src/components/motion/AnimatedSection.tsx`
- Create: `src/components/motion/StaggerGroup.tsx`
- Create: `src/components/motion/StatChange.tsx`
- Create: `src/components/motion/TabTransition.tsx`

- [ ] Define shared Motion presets for page entry, staggered reveals, tab changes, stat updates, hover feedback, loading skeletons, and chart entrances.
- [ ] Respect `prefers-reduced-motion` in every reusable animation wrapper.
- [ ] Keep normal UI durations between 150ms and 300ms; reserve longer timing only for first-view storytelling.
- [ ] Add Motion wrappers that can be reused by pages without scattering animation constants across the app.
- [ ] Add tests or implementation checks for reduced-motion behavior where practical.
- [ ] Commit with `feat: add motion interaction system`.

## Task 5: Define Football Domain Model

**Files:**
- Create: `src/lib/football/types.ts`
- Create: `prisma/schema.prisma`
- Create: `src/lib/data/seed.ts`

- [ ] Define core entities: `Competition`, `Season`, `Team`, `Player`, `Match`, `Venue`, `Standing`, `Lineup`, `MatchEvent`, `TeamStat`, `PlayerStat`, `Article`.
- [ ] Seed FIFA 2026, sample host cities, sample teams, and representative match data.
- [ ] Add computed fields for `rating`, `formScore`, `strengthTags`, `weaknessTags`, and `styleTags`.
- [ ] Verify seed data renders without an external API.
- [ ] Commit with `feat: add football domain model`.

## Task 6: Build Core Public Pages

**Files:**
- Create: `src/app/competitions/[slug]/page.tsx`
- Create: `src/app/matches/[id]/page.tsx`
- Create: `src/app/teams/[slug]/page.tsx`
- Create: `src/app/players/[slug]/page.tsx`
- Create: `src/app/articles/[slug]/page.tsx`

- [ ] Build competition hub pages with fixtures, standings, teams, latest articles, and tournament context.
- [ ] Build match center pages with preview, kickoff time, venue, form, head-to-head, lineups, stats, and tactical notes.
- [ ] Build team pages with squad, results, fixtures, style tags, strengths, weaknesses, and related articles.
- [ ] Build player pages with profile, stats, rating trend, strengths, weaknesses, and recent matches.
- [ ] Build article pages with SEO metadata, structured content, related entities, and internal links.
- [ ] Apply the UI UX Pro Max dashboard visual system to every public page instead of one-off page styling.
- [ ] Add Motion-powered section entry, tab transitions, stat updates, and chart reveals where they improve comprehension.
- [ ] Commit with `feat: add football intelligence page types`.

## Task 7: Add Data Provider Layer

**Files:**
- Create: `src/lib/football/provider.ts`
- Create: `src/lib/football/cache.ts`
- Create: `src/lib/football/sources.ts`
- Create: `src/lib/football/provider.test.ts`
- Create: `src/lib/football/cache.test.ts`

- [ ] Define a provider interface for fixtures, results, standings, teams, players, match stats, lineups, and player stats.
- [ ] Implement a seed-data provider first.
- [ ] Add adapter mappings for `API-Football`, `SportsDataIO`, `SportMonks`, and official/public league endpoints behind environment variables.
- [ ] Add a news provider abstraction for `The Guardian Open Platform`, `New York Times APIs`, and optional `NewsAPI` fallback.
- [ ] Add a separate event-monitoring abstraction for `GDELT` topic, entity, tone, and source-cluster signals.
- [ ] Implement cache policies for static profiles, fixtures, standings, live matches, articles, and news/event signals.
- [ ] Add visible freshness metadata: `lastUpdated`, `source`, `isStale`, and `refreshInterval`.
- [ ] Add quota-safe behavior: server-only provider calls, request timeouts, retries with backoff, stale snapshot fallback, and no direct browser polling of upstream APIs.
- [ ] Add optional adapters for weather and context data such as `Open-Meteo` and odds providers if those features are enabled.
- [ ] Test missing stats, postponed matches, duplicate players, timezone conversion, and failed API responses.
- [ ] Test stale cache fallback, provider timeout, rate-limit response, and match-day TTL behavior.
- [ ] Commit with `feat: add football data provider abstraction`.

## Task 7A: Add Rights And Source Governance

**Files:**
- Create: `src/lib/football/licensing.ts`
- Create: `docs/source-and-asset-policy.md`
- Update: `src/lib/football/provider.ts`

- [ ] Document allowed, review-required, and disallowed asset/data categories.
- [ ] Record provider terms to check before enabling each API: commercial display, caching, redistribution, attribution, logos, photos, and derived statistics.
- [ ] Add source metadata types for attribution, licence notes, cache permissions, and display restrictions.
- [ ] Replace official logo/player-photo assumptions with rights-safe placeholders unless a licence is confirmed.
- [ ] Add implementation guidance that forbids scraping competitor sites or official feeds outside permitted APIs.
- [ ] Commit with `docs: add football source and asset policy`.

## Task 8: Add Search, Trust, And Quality Foundations

**Files:**
- Create: `src/app/sitemap.ts`
- Create: `src/app/robots.ts`
- Create: `src/app/privacy/page.tsx`
- Create: `src/app/terms/page.tsx`
- Create: `src/app/about/page.tsx`
- Create: `src/app/contact/page.tsx`

- [ ] Add metadata, canonical URLs, Open Graph tags, and schema.org data for sports events, teams, players, and articles.
- [ ] Add sitemap and robots output.
- [ ] Add legal/trust pages that explain the site, editorial standards, contact path, privacy posture, and terms.
- [ ] Add quality checks for thin pages, duplicated sections, missing sources, empty stats, broken internal links, and poor mobile layout.
- [ ] Ensure every indexed page has useful football intelligence, original commentary, clear navigation, and a reason to exist.
- [ ] Keep commercial surfaces out of the first implementation pass unless they directly improve user experience.
- [ ] Commit with `feat: add search trust and quality foundations`.

## Task 9: Build Initial Content Cluster

**Files:**
- Create: `src/content/articles/*.mdx`

- [ ] Add FIFA 2026 schedule guide.
- [ ] Add FIFA 2026 host cities guide.
- [ ] Add World Cup qualification explainer.
- [ ] Add football ratings explainer.
- [ ] Add xG explainer.
- [ ] Add formations guide.
- [ ] Add team-preview templates for qualified or likely FIFA 2026 teams once data is available.
- [ ] Add player-watchlist templates focused on role, form, tactical fit, and tournament relevance.
- [ ] Add match-preview and match-recap templates that combine data signals with human editorial judgment.
- [ ] Add methodology notes explaining ratings, form score, source usage, freshness, and limitations.
- [ ] Add internal links from every article to relevant competition, match, team, or player pages.
- [ ] Build toward 25-40 substantial pages before broad launch promotion.
- [ ] Require human review, source links, and original conclusions before publishing any AI-assisted content.
- [ ] Commit with `content: add initial football seo cluster`.

## Task 10: Verification And Launch Checklist

- [ ] Run `npm run lint`.
- [ ] Run `npm run build`.
- [ ] Test mobile and desktop layouts for home, competition, match, team, player, and article pages.
- [ ] Test animated states on desktop and mobile: page load, tabs, filters, hover/tap, stat changes, and loading skeletons.
- [ ] Test `prefers-reduced-motion` and confirm non-essential Motion effects are disabled.
- [ ] Check for layout shift caused by animated cards, filters, charts, and images.
- [ ] Verify no indexed page is empty, under construction, copied, or generated without original commentary.
- [ ] Verify mobile-first usability at 375px for all core page types before desktop polish is considered complete.
- [ ] Verify live-data modules show source, freshness, stale state, and graceful fallback behavior.
- [ ] Verify API usage respects cache TTLs and does not poll paid/free providers directly from the browser.
- [ ] Verify source and asset policy before using logos, badges, player photos, official marks, or proprietary stats.
- [ ] Verify articles meet the content quality gate: human-reviewed, source-linked, original conclusions, and useful internal links.
- [ ] Verify sitemap, robots, legal pages, and metadata.
- [ ] Submit to Google Search Console after the core pages are useful, internally linked, and technically clean.
- [ ] Confirm the site is strong as a product: useful pages, clear navigation, fast rendering, original commentary, and polished football intelligence.
- [ ] Commit with `chore: verify launch readiness`.

## Assumptions

- The product targets global English-speaking football fans.
- FIFA 2026 is the first traffic wedge.
- WhoScored is used as a depth reference only; no scraping, copied content, copied rating formula, or brand imitation.
- The first version uses seeded data, then adds paid API integration after the site structure is stable.
- The first milestone is building a strong football intelligence product that earns repeat visits on its own merits.
- Mobile-first page value matters more than desktop density; desktop dashboards are an enhancement, not the base experience.
- Rights-safe assets and licensed data are required before using official football imagery, logos, marks, or proprietary feeds.
