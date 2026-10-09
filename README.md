# Capstone project
# Solarpunk Field Guide: Capstone Project Log (Modules 1–3)

**Author:** Anitra French
**Course:** GIT 414/515, Production Website Capstone
**Repository:** https://github.com/ajfrenc5/Capstone-project
**License:** Code licensed under the GNU General Public License v3.0 (see `LICENSE`)

This README is my running log of the Solarpunk Field Guide capstone. It records what I built, why I made each decision, how I tested it, and where I used AI assistance.

The Solarpunk Field Guide is a living archive of low-tech tools, mutual aid, and solar culture. It gathers open hardware schematics, community workshop templates, and artwork that connects ecological restoration with human technology.

The site is built with hand-written HTML and a single shared stylesheet (styles.css), using Google Fonts (Anta for body text, Press Start 2P for headings).

----------------------------------------------------------------------------------------------------------------------------------------------------
Planning:Topic and scope

Site idea: a curated, multi-page introductory field guide and resource hub. It introduces newcomers to the core principles and aesthetics of the Solarpunk movement and to hands-on, real-world renewable practices: energy, fabrication, regenerative food systems, and local community resilience models.

HTML/CSS fit: as a curated reference site, it only needs to display instructional text, images, semantic tables, and diagrams. It needs no database, client-side scripting, or user logins. Everything the site does is "display curated content clearly and let people navigate it," which HTML and CSS handle natively.

Content risks I identified:

Art, diagrams, and schematics need proper licensing and attribution. I planned to use Creative Commons work with credit.
DIY electronics and low-tech instructions need to be technically accurate and safe.
Project brief
Purpose: explain Solarpunk principles, aesthetics, DIY renewable practices, and community resilience models.
Audience: designers, sustainability advocates, DIY makers, hobbyist gardeners, homesteaders and off-grid households, community organizers, amateur radio operators, students, and curious readers looking for an accessible, structured introduction to Solarpunk.
Primary tasks: learn core principles, compare DIY systems, follow project checklists, use community links and resources, and view art and design.
Constraints: plain HTML and CSS only. No JavaScript, user logins, or databases.
Content inventory

I listed 12 content items. All were marked "Missing" because none had been written or sourced yet.

ID	Content item	Format	Source	Risk or note
C1	Overview text	Text	Self-written	Needs to be written clearly
C2	Site guide text	Text	Self-written	Needs to be written
C3	Aesthetic introduction	Text	Self-written	Needs to be written
C4	Art showcase images	Image	Creative Commons artists	Must verify open licenses and credit artists
C5	DIY system summaries	Text	Self-written	Technical accuracy and safety
C6	Systems comparison	Table	Self-written	Must fit on small mobile screens
C7	Project checklists	Text	Self-written	Needs to be written
C8	Schematics and diagrams	Image	Open-source repos	Licensing and missing alt text
C9	Community models text	Text	Self-written	Needs to be written
C10	External community links	Link	Public websites	Needs link verification
C11	Global navigation	Link	Self-authored	Must work on mobile and desktop
C12	Footer notes	Text	Self-written	Needs proper attribution format
Site map and page requirements
Home: introduces Solarpunk principles, core philosophy, and a site guide.
Gallery: displays Solarpunk visual art and design concepts with artist credit.
DIY Systems: explains off-grid energy, low-tech tools, and gardening projects, with comparison tables and safety notes.
Community Resilience: covers tool libraries, mutual aid, and repair cafés, with links to external resources.
Wireframes and behavior annotations

I made responsive wireframes in Figma: SolarPunk Field Guide wireframes

Header: links sit in a horizontal row on desktop and stack into a single column on mobile, with hamburger lines for alternate navigation.
Cards: multi-column grids on desktop collapse to one column on mobile.
Comparison table: full width on desktop; scrolls horizontally on phones so words don't get squished.
Images: scale down automatically so they never overflow phone screens.
Acceptance criteria
Responsive: under 768px, navigation links stack in one column so mobile users can tap them. (Test: DevTools at 320px.)
Responsive: under 600px, the comparison table scrolls horizontally so text isn't cut off. (Test: DevTools at 375px.)
Accessibility: pressing Tab shows a visible focus outline on interactive links. (Test: manual keyboard tabbing.)
Accessibility: text contrast against backgrounds is at least 4.5:1. (Test: axe DevTools.)
Browser fallback: if custom fonts fail to load, system fonts display. (Test: disable web fonts.)
Performance: Google Lighthouse mobile score is at least 90. (Test: Chrome Lighthouse.)
Metadata: every page has a unique <title>. (Test: inspect page source.)
Release quality: zero syntax errors. (Test: W3C HTML validator.)

----------------------------------------------------------------------------------------------------------------------------------------------
CSS Architecture

I built the CSS foundation the rest of the project depends on.

Readiness: CSS inventory from my planning package

Before writing CSS, I turned my planning package into a CSS inventory:

Repeated components: the header menu, content blocks used across Home, Gallery, and DIY pages, the DIY comparison table, step-by-step project lists, and image containers with artist credits and license notes.
Foundational decisions: text contrast of at least 4.5:1, system font fallbacks, consistent spacing, max-width containers, subtle borders, and a visible keyboard focus outline.
Layout needs: grids that collapse to one column on mobile, a header that moves from horizontal to stacked, a scroll wrapper for the comparison table under 600px, and fluid image sizing.
States: focus, current page across the four pages, and hover/active feedback.
Print needs: DIY project checklists and system summaries should print cleanly as reference sheets.
Biggest risk: the side-by-side comparison table breaking the layout on small screens.
Practice: refactoring a messy stylesheet

Before refactoring my own CSS, I practiced on a provided messy stylesheet:

Removed duplicate header and .site-header blocks that declared the same padding and background.
Replaced repeated hardcoded values (
#8c1d40, 
#ffc627, 24px, 12px, 8px, 4px) with :root tokens.
Shortened .site-header nav ul li a to .site-header nav a, and merged the :hover and [aria-current="page"] rules so they share declarations.
Reduced selector specificity in those two places.
Collapsed duplicated header, button, card, and callout rules without changing the visual result.
Tested at desktop (over 700px) and mobile (700px and under) widths.
Organization and cascade
The stylesheet is organized with native cascade layers, from broadest to narrowest: @layer reset, base, layout, components, utilities, overrides;
Later layers override earlier layers regardless of selector specificity, so my selectors stay flat (mostly single classes) and I don't need !important in screen styles.
reset normalizes browser defaults and sets box-sizing: border-box.
base holds the design tokens in :root and default styles for bare HTML elements.
layout holds page-level containers and wrappers: .site-container, .site-header, .site-main, .grid-cards, .table-scroller, .site-footer.
Design tokens

All tokens are declared in :root and named by purpose rather than appearance (for example, --color-primary instead of --color-green):

Color: surface, text, primary, accent, border, warning, link, and focus tokens.
Type: --font-base (Anta), --font-heading (Press Start 2P), --line-height-base: 1.6, --line-height-heading: 1.4.
Spacing: --space-1 through --space-16.
Shape and elevation: radius scale, --border-width, --shadow-subtle, --shadow-raised.
Layout: --container-max: 72rem, --measure-text: 65ch.
Components
Primary navigation (.site-nav-list, .site-nav-link) with padded touch targets and hover and current-page states.
Action button (.button) with locally scoped variables (--button-bg, --button-fg, --button-border, --button-hover-bg), styling <a> and <button> the same way.
Art card (.art-card) for the gallery.
Comparison table (.comparison-table) inside a .table-scroller for horizontal scrolling on small screens.
Callout alert (.callout-alert) with scoped --alert-accent and --alert-bg so color variants can be swapped without changing its structure.
Utilities and states
Utilities: .visually-hidden, .eyebrow, .cluster.
States: :hover, :active (a 1px press on buttons), :focus-visible (a 3px outline with a 2px offset), [aria-current="page"], and :target (an outline flash when an in-page link jumps to a section).
Print support

An @media print block hides the header, footer, and buttons, removes backgrounds and forces black text, unwraps the table scroller so tables print flat, avoids page breaks inside cards, tables, and callouts, and prints external link URLs beside their link text.

Refactoring
Consolidated duplicate .button, .btn, and button rules into a single .button component.
Separated page structure (layout layer) from component presentation (components layer).
Module 2 testing
Narrow (320–375px): header wraps cleanly, the table scrolls inside its container, and cards drop to one column.
Wide (1200px+): content caps at 72rem and centers.
Keyboard: every link and button shows the visible focus ring.
Print preview: navigation and buttons are hidden, backgrounds are removed, and link URLs print.

--------------------------------------------------------------------------------------------------------------------------
Responsive Layout Systems

In Module 3 I extended my Module 2 architecture into a responsive layout system, building on it rather than replacing it.

Cleanup before starting
Removed the duplicate font load. Fonts were loading twice, through the HTML <link> and a CSS @import. I deleted the @import, which also delayed rendering. I verified that both fonts still load.
Removed inline styles. I moved the site title's inline font styles into a .site-brand class (components layer) and the footer's inline justify-content into a .site-footer-inner class (layout layer). The page no longer has inline styles, so all styling runs through cascade layers.
Corrected the footer license. The footer linked to Creative Commons, which didn't match my repository license. It now reads "Code licensed under GNU GPLv3" and links to the LICENSE file on GitHub.
Part 1: Responsive foundation
Fluid gutter: I added --gutter: clamp(1rem, 0.5rem + 2vw, 2.5rem). The side spacing is never tighter than 1rem on small screens, grows with the viewport, and stops at 2.5rem on wide screens. The rem portion keeps it responsive to zoom and font size.
Container: .site-container uses inline-size: min(100% - (var(--gutter) * 2), var(--container-max)) with margin-inline: auto. It fills the screen minus the gutters, caps at 72rem, and uses logical properties.
Print: I updated the print rule to reset inline-size: 100% so it matches the new container.
Part 2: Advanced Grid patterns
Art card grid: repeat(auto-fit, minmax(min(100%, 17.5rem), 1fr)). Cards reflow from three to two to one column with no media queries. I replaced the original fixed 280px minimum with min(100%, 17.5rem) so a card can never overflow a narrow or zoomed screen, and rem keeps the cards proportional to the user's font size.
Community workshop schedule: fit-content(10rem) 1fr on a <dl>. The date column sizes to its longest date up to a 10rem cap, and dates stay aligned across all rows. This complements the card grid: that grid decides how many columns fit, while this one sizes a column to its content. I used <dl> to pair each <time> with its event details.

I considered a grid placing the intro beside the safety notice and decided against it. I added the Community section to the home page for now. The nav links are placeholders for separate pages I plan to build later.

Part 3: Subgrid

The art cards use subgrid: grid-row: span 3; grid-template-rows: subgrid; row-gap: 0;. Each card borrows three rows from the parent grid (title, description, footer), so these line up across every card in a row even when one title wraps to two lines.

While doing this I found and removed dead .art-card-body rules left over from my Module 2 markup cleanup. They targeted a wrapper that no longer existed, so the cards had lost their padding and footer alignment.

Part 4: Container-query component

The event schedule is a reusable container-query component:

The .event-schedule-wrap wrapper is a named container: container: event-schedule / inline-size.
The default layout stacks each date above its event details.
@container event-schedule (inline-size >= 30rem) switches to the two-column fit-content(10rem) 1fr grid.

I chose a container query rather than a media query because the schedule's layout depends on the space it has, not the screen size. On a future Community page it may sit in a narrower column, where a viewport media query would keep two columns on a wide screen and squeeze the event details.

Part 5: Content-driven breakpoints

I found my breakpoints by testing in DevTools responsive mode from 320px upward and noting where the content actually broke, not by device sizes. Breakpoints are written in em so they respond to zoom and font size.

Breakpoint	What I observed	What changes
26em (~416px)	All four nav links first fit on one row at about 410–420px. Below that they wrapped into uneven rows.	Below 26em the nav is a 2×2 grid. At 26em and up it is a single row.
60.5em (~968px)	The full comparison table first fit without scrolling at 965px. The wide Press Start 2P headers were forcing the scroll.	Below 60.5em the table headers use Anta to reduce scrolling. At 60.5em and up they use Press Start 2P.
None	Spacing looked good from 320px up and never felt cramped.	No breakpoint needed; the clamp() gutter and spacing tokens scale fluidly.

These connect directly to my planning package. My Module 1 acceptance criteria guessed at round numbers: stack the nav under 768px and scroll the table under 600px. Testing the real content showed different points. The nav only needs to change below about 416px, and with the wide pixel font the table actually needed to scroll all the way up to about 965px. My CSS inventory had already named the comparison table as the biggest layout risk, and testing confirmed it.

Part 6: User preferences

I added a prefers-reduced-motion: reduce query:

The :target highlight becomes a static outline, so users still see where a link took them, without the animation.
The button's 1px press shift is removed.
Color transitions are kept, because a color change is not movement.
Part 7: Feature and fallback strategy
Subgrid is wrapped in @supports (grid-template-rows: subgrid). The fallback, written first, is a flex column where the paragraph grows to keep footers aligned at the bottom of each card.
Container query: the stacked schedule is the default, so browsers without container query support still get a layout that is readable at any width.
Bug found and fixed

My reduced-motion block had ended up inside the @container block because of a missing closing brace. That left the components layer unclosed and trapped the utilities, overrides, and print sections inside it. I added the missing brace and moved the reduced-motion query out on its own.

AI disclosure

Module 1: AI-assisted planning templates. I used AI to brainstorm and format the required planning templates. I considered its table structure, simplified criteria wording, and template setup. I verified and changed the output by setting every content inventory item to "Missing," to accurately show that no assets had been written or sourced yet.

Module 2: Gemini. I used Gemini as a collaborative web design assistant to format the cascade layer scaffolds, validate token naming syntax, generate mock table rows for the prototype, draft initial refactoring comparison tables, review my work, and explain failure points.

Module 3: Claude (Anthropic).

 Because the course did not include direct instruction on these techniques, I used Claude as a step-by-step tutor. It audited my files against the assignment's required parts, explained each CSS technique (clamp(), min(), minmax(), fit-content(), subgrid, container queries, @supports, and preference queries), and gave me one step at a time with the exact code to change.
Output considered: CSS and HTML snippets, testing procedures, the event placeholder content, explanations, and draft wording for my layout notes and code comments.
Verification: I made every change in my own files, tested each one in the browser and DevTools, and chose my breakpoints from my own observations of where the content broke. I decided against one suggested layout (placing the intro beside the safety notice) and chose a different second grid. Claude identified the missing closing brace, and I fixed it in my file.
What changed: Claude found several problems in my existing code: the duplicate font import, dead .art-card-body rules, a fixed 280px grid minimum, inline styles, and a footer license that didn't match my repository. I fixed all of them and built the responsive features described in Module 3.

-----------------------------------------------------------------------------------------------------------------------
Media and Typography

In Module 4 I added the site's first real media (a logo, three illustrations, and an icon) and rebuilt the typography system. I documented where every asset came from directly in the HTML, so the provenance travels with the code.

Asset inventory and provenance

Every asset has an ASSET: comment right above it in the HTML that names the file, its source, its license or ownership, its purpose, and optimization notes.

Licensing correction: before Module 4, my art cards had placeholder license lines ("CC BY-SA 4.0 · Open Source Design," "CC0 Public Domain · Solarpunk Commons," "CC BY 4.0 · Open Agriculture Lab"). Those described artwork that didn't exist. When I added the real illustrations, I removed those footers, because the images are my own AI-generated work and the old lines would have given false license information.

Images I sourced and then dropped: I also downloaded 17 photos from Wikimedia Commons (amateur radio, beekeeping, pottery, woodworking, and others) and planned an image credits list using each file's "Use this file" attribution. I later decided not to use them and removed them from the repository, so none of them appear on the site.


Dimensions: all three illustrations are 1248×832 JPGs. Every <img> has width and height attributes that match the file's real pixel size.
Logo: the header logo uses the 192×192 version, displayed at 32×32. That's six times the display size, so it stays sharp on high-resolution screens. At first I pointed it at the 512×512 file by mistake, then switched it to the 192 file and corrected the comment to match.
Loading: the Gallery images use loading="lazy" and decoding="async", so they don't download until the reader scrolls near them. The Home hero is the first thing on screen, so it uses fetchpriority="high" instead of lazy loading.
Fluid sizing: my reset layer sets img, svg { max-inline-size: 100%; block-size: auto; }, so images never overflow narrow screens.
Icon sizing: the logo is sized in rem (2rem) and the SVG icon in em (1.5em), so both scale with zoom and text size.
File size (recorded, not yet fixed): the comments record each original size: 593 KB, 678 KB, and 694 KB. I did not add srcset/sizes, <picture>, WebP, or compression in Module 4. The site uses the same composition for each image at every width (a single illustration inside a card or beside the hero text), so there was no art-direction reason for <picture>, but the file sizes were still a known performance issue.
Alt text and alternatives

I decided each image's purpose before writing its alt text:
Informative images get alt text that describes only what's actually drawn:
Micro-grid: "Cottages with solar panels on green roofs, linked by cables to a central pavilion."
Cooling arcades: "Shaded courtyard with curving arches, lattice canopies, and hanging plants around a central pool."
Wick irrigation: "Garden bed cut away to show clay pots linked by rope wicks beneath rows of leafy plants."
Decorative logo: alt="". The link text "Solarpunk Hub" already names the link, so describing the logo would make screen readers repeat it.
Decorative SVG: the heart-handshake icon has aria-hidden="true" and focusable="false", because the heading text "Community Workshops" carries the meaning.
Other media: the site has no audio, video, animation beyond the :target highlight from Module 3, or embeds, so captions, transcripts, and embed titles don't apply.
Typography system

I rebuilt the type system with three fonts, each with one job, all set through tokens in :root:

css
--font-base: "Space Grotesk", system-ui, sans-serif;  /* body text */
--font-heading: "Anta", system-ui, sans-serif;         /* h1–h4 */
--font-brand: "Press Start 2P", system-ui, monospace;  /* site name + buttons */
Why I changed it: Press Start 2P is a wide pixel font that was hard to read as a heading font, and Anta was hard to read as body text. I asked for a futuristic but highly legible sans-serif and chose Space Grotesk for body text. Anta moved to headings, and Press Start 2P is now limited to the site name and buttons.
Type scale: body text is 1rem, and headings use clamp() so they grow smoothly with the screen, for example h1 is clamp(1.25rem, 2.5vw + 0.5rem, 1.75rem).
Line height: --line-height-base: 1.6 for body text and --line-height-heading: 1.4 for headings.
Line length: prose is capped at --measure-text: 65ch.
Spacing: body and headings use letter-spacing: -0.02em to tighten Space Grotesk and Anta slightly. The brand and buttons reset to 0, and their pixel font is set to a smaller 0.75rem with 1.6 line height so buttons don't overflow on phones. The site name is 1rem, placed after the shared rule so it wins.
No faux bold: Anta and Press Start 2P only come in weight 400, but my headings, buttons, site name, and table headers were asking for bold. Browsers fake bold by smearing the letters, so I set all of those to font-weight: 400.
Fallbacks: each stack falls back to system-ui and then a generic family, so the page stays readable if Google Fonts fails to load.

Fonts load with one <link> to Google Fonts in each page's <head>, with preconnect hints for fonts.googleapis.com and fonts.gstatic.com so the connection starts early.
display=swap shows the fallback font immediately and swaps in the web font when it arrives, so text is never invisible while fonts load.
Space Grotesk is requested only in the weights I use (400–700).
A comment above the link lists all three fonts and the job each one does.
Layout-shift note: with swap, text can reflow slightly when the web font replaces the fallback, because the fonts have different widths. I limited the risk by keeping the widest font (Press Start 2P) to short, small text (the site name and buttons).
Layout stability
Every <img> has width and height, so the browser reserves the correct space (3:2 for the illustrations, 1:1 for the logo) before the file downloads, and content below doesn't jump.
The logo box is fixed at 2rem × 2rem with flex-shrink: 0, and the SVG icon at 1.5em × 1.5em, so neither can collapse or push the text around.
The hero loads with high priority, so the largest image on Home isn't delayed.
Fixes along the way
Stray } in styles.css: an extra brace after the .comparison-table th rule was closing the components layer early. The browser then threw away my whole utilities layer, so .eyebrow, .cluster, and .visually-hidden stopped working. I removed it.
Missing line-height tokens: when I replaced the typography tokens, I accidentally deleted --line-height-base and --line-height-heading, so the page fell back to the browser's default line spacing. I restored them.
Removed the 60.5em table-header breakpoint: my Module 3 breakpoint only existed because the pixel font made the table headers too wide. With Anta for headers, it's no longer needed, so table headers now use Anta at every width.
Rebrand: I renamed the site from "Solarpunk Field Guide" to "Solarpunk Hub" in the page title, header, hero text, and footer.
Header markup: I fixed the brand link so it closes right after "Solarpunk Hub," keeping the navigation outside it.
Mockups

I updated my Figma file so it matches the live site: a grayscale wireframe page and a mockup page with my real colors and fonts, each showing all four pages at desktop (1440px), tablet (768px), and mobile (390px). The Home mockup led to the new hero layout, with the text and the micro-grid illustration side by side on wide screens and stacked on narrow ones.

Module 4 checks
Refreshed the page after each change and confirmed the logo and "Solarpunk Hub" sit side by side, the site name and buttons are in Press Start 2P, the navigation and body text are in Space Grotesk, and table headers are in Anta at every width.
Checked the header markup (lines 19–25) and confirmed the logo comment names the file that's actually loaded.
Confirmed every image has width/height matching its real pixel size, and recorded each file size in its comment.
Confirmed the utilities layer works again after removing the stray brace.

Known limitations carried forward: the three illustrations are 593–694 KB with no responsive sizes or compression, and font swapping can cause small text reflow.

Module 4 AI disclosure
Tools: Gemini and Claude (Anthropic).
Gemini: I used Gemini to generate the site logo and the three illustrations (neighborhood micro-grid, passive cooling arcades, and wick irrigation). I wrote the prompts, chose the results, and labeled every one as AI-generated in its asset comment.
Claude: I used Claude as a step-by-step guide. It explained concepts, suggested code snippets and comment wording, recommended Space Grotesk when I asked for a futuristic but legible sans-serif, explained how to credit Wikimedia Commons images, updated my Figma wireframes and mockups to match my site, and reviewed my files for errors.
What I decided: I chose which fonts did which job (Press Start 2P for the site name and buttons, Anta for headings), chose to remove the breakpoint instead of rewriting the note, decided to drop the Wikimedia photos, and decided which images were informative or decorative.
Verification: I made every change in my own files and checked each one in the browser. Claude found the stray brace, the missing line-height tokens, the faux-bold weights, and the outdated logo and font comments, and I fixed each one myself.
What I didn't do: responsive image sets, <picture>, and image compression were not done in this module, so this log doesn't claim them.

---------------------------------------------------------------------------------------------------------------
Accessibility Audit and Remediation Log

In Module 5, I audited my capstone site for accessibility, fixed the problems I found, and retested each fix. I started with an automated WAVE scan of my single-page site, then fixed shared parts of the page (headings, page title, skip link) before splitting the site into four pages so every new page would inherit those fixes. I finished with one testing session covering keyboard use, zoom, reflow, text spacing, contrast, and the accessibility tree, and documented everything in my audit report.

Baseline WAVE scan (Home): 0 errors, 0 contrast errors, 1 alert (skipped heading level), AIM score 10/10. I saved screenshots of the Summary and Structure tabs as "before" evidence.
Fix 1, skipped heading level: The Safety Notice heading was an h3 directly after the page's h1. I changed it to an h2, added aria-labelledby so the <aside> landmark is announced by name, and set font-size: 1rem in CSS to keep the original look. Retest: WAVE showed 0 alerts, the Structure tab showed h1 then h2, and the ARIA count went from 3 to 4.
Fix 2, page title: The title still read "Solarpunk Field Guide · CSS Architecture Prototype," left over from an earlier assignment. I changed it to a page-first title ("Home · ..."). I screenshotted the browser tab before the change.
Fix 3, skip link: Pressing Tab first landed on the logo, so keyboard users had to pass five links on every page. I added a "Skip to main content" link as the first element in <body>, gave <main> the id main-content, and styled the link to stay off-screen until it receives focus. Retest: the link appears on the first Tab, and Enter moves focus to the main content.
Report setup: I built my audit report in Google Docs using my instructor's model template, with real heading styles so the document outline is navigable.

I sketched layouts for four pages (Home, Tech Sovereignty, Community Resilience, Gallery / Media) and turned them into Figma wireframes and mockups.
I renamed the site Solarpunk Hub, rebuilt the Home hero (heading, two buttons, hero image), added a "What is solarpunk?" intro panel, and updated font roles: Anta for headings, Press Start 2P for the site name and buttons, and Space Grotesk for body text.
October 6–7: Page split and remaining fixes
Fix 4, table caption: The comparison table had header cells and scope attributes but no name. I added a <caption> describing the table. It now lives on the Tech Sovereignty page.
Fix 5, logo link: The logo linked to href="#", which did nothing and could not take users home from other pages. I changed it to index.html.
Page split: I built tech-sovereignty.html, gallery.html, and community-resilience.html, moving existing sections out of index.html. Every page has a unique title, one h1, the skip link, and aria-current="page" on its own nav link.
I checked my CSS for a reported missing closing brace in the event-schedule container query. My current file was already correct, so I made no change.

Test|Page(s)|	Result
WAVE	Home, Tech Sovereignty, Gallery	0 errors and 0 contrast errors on all three. 1 alert per page ("redundant link": logo and Home both link to index.html), reviewed and kept as a standard convention.
Keyboard	Tech Sovereignty	Pass. Order: skip link → logo → four nav links → footer link. Visible focus on every stop; Shift+Tab works with no keyboard trap.
Zoom 200%	Tech Sovereignty	Pass.
Reflow	Tech Sovereignty	Pass at 375px: only the table scrolls sideways, inside its own keyboard-focusable box (allowed exception for data tables). 320px width retest pending.
Text spacing	Home (local copy)	Pass. Line height 1.5, paragraph spacing 2em, letter spacing 0.12em, word spacing 0.16em applied with a bookmarklet; no clipped or overlapping text.
State contrast	Site-wide tokens	Focus outline 
#2d6a4f on 
#f4f6f0: 5.86:1 (needs 3:1). Current-page link 
#2d6a4f on 
#e9ede4: 5.38:1 (needs 4.5:1).
Accessibility tree	Tech Sovereignty table	"System" header: role columnheader, name "System." Table: role table, named from its caption.

I filled in my audit report: test scope, out of scope, test environment, evidence table, tool limitation, remediation log, conformance summary, and AI disclosure, then placed my screenshots with captions.
Remediation summary
No	Issue	WCAG	Priority	Fix	Retest
1	Skipped heading level in Safety Notice	1.3.1	Medium	h3 → h2, added aria-labelledby	WAVE 0 alerts; outline h1 → h2
2	Outdated, non-descriptive page title	2.4.2	Medium	Unique, page-first titles	Each tab shows its own page name
3	No skip link	2.4.1	High	Skip link targeting #main-content	Visible on first Tab; Enter jumps to content
4	Data table had no name	1.3.1	Medium	Added <caption>	Accessibility tree: table named from caption
5	Logo link went to #	2.4.4	Low	href="index.html"	Logo returns to Home
Tool limitation

WAVE gave my Home page a perfect 10/10 score at baseline while missing four problems I found by hand: the skip link, the outdated title, the unnamed table, and the broken logo link. Automated tools can't judge focus order, alt-text accuracy, or how content behaves at different zoom levels, and the accessibility tree shows what a screen reader receives without being a real screen reader test.

Out of scope
Community Resilience was built but not formally tested.
The site has no forms, audio, video, embeds, or login, so those checks are not applicable.
The prefers-reduced-motion rule exists, but no current link triggers the animation it controls, so motion was not tested.
Remaining limitations and next steps
Test Community Resilience with the same checks.
Test with a screen reader (NVDA or VoiceOver) and in Firefox and Safari.
Test on a physical mobile device.
Add a "(opens in new tab)" notice to the footer license link.
Rerun WAVE and contrast checks after future visual changes.

AI disclosure
I used Claude (Anthropic) as an AI assistant in Module 5.
Purpose: Claude walked me through the audit step by step, explained the WCAG criteria behind each check, suggested which tests to run. Claude also helped me draft the wording of my audit report and this README from my test results. 
Verification: I made every code change myself, ran every test myself (WAVE, keyboard, zoom, reflow, text spacing, WebAIM Contrast Checker, Chrome DevTools accessibility tree), and took all of the screenshots. When Claude reported a missing CSS brace, I checked my file, found it was already correct, and did not apply another change.

---------------------------------------------------------------------------------------------------------------------------
Discoverability, Metadata, and Structured Content

In Module 6, I made my capstone easier for people and machines to understand outside the visible page. I gave every page an accurate title and description, chose preferred URLs, added a social link preview and a small piece of structured data to Home, checked my image context, and validated everything on the live site. I also wrote down which search claims I won't make, because my evidence doesn't support them.

1. Planning: metadata inventory (Readiness)

Before changing any code, I made an inventory connecting each page to its purpose, its main user task, and what is actually visible on it.

Page|	File|	Primary user task
Home	index.html	Learn what solarpunk is and choose where to go next
Tech Sovereignty	tech-sovereignty.html	Compare DIY resilience systems by function, complexity, cost, and maintainability
Community Resilience	community-resilience.html	Find upcoming hands-on community workshops and their dates
Gallery / Media	gallery.html	Browse visual concepts of solarpunk design ideas

While auditing the pages, I found three things worth noting:
My Home title was Home · Solarpunk Hub, which doesn't say what the page is about.
None of my pages had a meta description.
Two page intros promise more than the page shows. Community Resilience mentions "places, events, and networks" but only lists workshops, and Gallery / Media mentions "media" but only has images. I wrote my descriptions to match what is really on each page, not what the intros promise.
2. Image text fix
The Neighborhood Micro-Grid card on the Gallery page said "energy routing diagrams," but the image is an illustration of cottages, not a diagram. I changed one word in gallery.html so the nearby text matches the image:
Commit: Update micro-grid card text to match illustration

3. Titles, descriptions, and canonical links (all four pages)
I replaced the <title> line in each page with a title, a meta description, and a canonical link. The titles and descriptions are the options I chose from AI-drafted alternatives during planning.

Page	Title	Change
Home	What Is Solarpunk? Start Here · Solarpunk Hub	Changed (matches the visible "What is solarpunk?" section)
Tech Sovereignty	Tech Sovereignty · Solarpunk Hub	Kept
Community Resilience	Community Resilience Workshops · Solarpunk Hub	Changed (workshops are the main content)
Gallery / Media	Gallery / Media · Solarpunk Hub	Kept (media is planned; I'll retitle it if I don't add any)

Each page's canonical points to itself with a full https:// URL. For Home, I chose the shorter URL without index.html, because the page loads at both addresses:


4. Social preview tags (Home)
I added Open Graph tags to Home, the page people would share to introduce the site. The values match the visible page. Open Graph uses property= instead of name=, and the image must be a full URL so other platforms can fetch it.
og:url matches my canonical exactly, so the two agree.
Commit: Add page metadata, canonicals, and Home social tags

5. Structured data (Home)
I added a small JSON-LD block describing the site's name and home address. Both are true and visible on the page: "Solarpunk Hub" appears in the header and footer.
What I chose not to add: I did not use the Event type for the workshops on Community Resilience. They are example events I made up for the capstone, so marking them as events would tell search engines that real events exist.
An honest limit: Google's site-name documentation says site names are not supported at the subdirectory level. My site lives in the /Capstone-project/ folder, so this markup is valid and accurate, but I don't expect it to change how my site name appears in Google.
Commit: Add WebSite structured data to Home

6. Links and headings
Every page has one <h1> and an <h2> for each main section. All internal links are real <a href> links with descriptive text, so they can be crawled and make sense out of context. Home also links to the two main sections through its "Explore Tech Sovereignty" and "Find community resources" buttons. I considered adding links inside the page content between related topics, such as from the Solar Caddy table row to the Solar Caddy Repair Café workshop, but decided not to in this version.

7. Image context
Image|	Alt decision|	Nearby context
neighborhood-microgrid.jpg (Home hero, Gallery card, social image)	Informative	Home <h1>; Gallery <h3> Neighborhood Micro-Grid
passive-cooling-arcades.jpg	Informative	Gallery <h3> Passive Cooling Arcades
subsurface-wick-irrigation.jpg	Informative	Gallery <h3> Sub-Surface Wick Irrigation
circuit-tree-icon-192x192.png (logo)	Decorative, alt=""; the link text names it	Site name beside it
Heart-handshake icon (inline SVG)	Decorative, aria-hidden="true"	<h2> Community Workshops

All filenames are descriptive and hyphenated, and every <img> has width and height.

8. Canonical, robots, and sitemap decisions
Canonical: applies now. Each page has a self-referencing canonical. A canonical is a signal to search engines, not a command.
Robots: not needed. No page uses noindex, which I confirmed in the page source. A robots.txt would have to live at the root of ajfrenc5.github.io, outside this repository.
Sitemap: deferred to release. All four pages are linked from the main nav on every page, so they can be found through ordinary links. I'll add a sitemap once the page list is final.
9. Validation (live site, October 9, 2026)
Check|	Tool|	Result
Metadata is published	View Page Source, all 4 pages	Title, description, and canonical on lines 6–8; Home Open Graph on lines 10–19 and JSON-LD on lines 21–29
HTML validity	W3C Nu HTML Checker, all 4 pages	"No errors or warnings to show" on every page
Structured data syntax	Schema Markup Validator	1 WebSite item, 0 errors, 0 warnings
Structured data eligibility	Google Rich Results Test	"No items detected," page crawled successfully (expected, since WebSite isn't a rich result type)
Social preview	Discord link preview	Site name, title, description, and image displayed correctly; Discord chose a small thumbnail

These checks show my metadata is published, my HTML is valid, my structured data is valid Schema.org, and at least one platform reads my preview tags correctly. They don't measure ranking, traffic, or shares.

10. Claims I'm not making
That my structured data will make "Solarpunk Hub" appear as a site name in Google.
That my new titles and descriptions will improve my ranking or control my search snippets. Google can rewrite both.
That my social tags will increase shares or traffic.
That my canonicals force Google to choose my preferred URL.
11. Carry forward to Module 7
If I resize or rename neighborhood-microgrid.jpg during performance work, I need to update og:image and its width and height, then retest the social preview.
If my site's URL ever changes, I need to update all four canonicals, og:url, and the JSON-LD url.
I'll rerun the W3C, Schema Markup, Rich Results, and social preview checks during release testing.
Open items: decide the Gallery / Media title and fix the Community Resilience intro.
AI disclosure

I used Claude (Anthropic) as a guide throughout Module 6.

Purpose: to review my HTML files, explain the concepts, draft options, and check my screenshots as I worked.
What the AI produced: two or three options for each page title and meta description; the Open Graph values; the JSON-LD block; wording options for an HTML comment; my commit messages; and drafts of my planning inventory, my deliverable document, and this log, written from my decisions and evidence.
How I verified it: I checked every title and description against what is actually visible on each page. I inspected the live page source for all four pages and ran the W3C Nu HTML Checker, Schema Markup Validator, Google Rich Results Test, and a Discord link preview myself. The AI's statement that Google doesn't support site names for subdirectory sites was checked against Google's own site-name documentation.
What I decided and changed: I chose the final titles and descriptions and kept two existing titles. I changed "diagrams" to "concepts" on the Gallery page. I picked a more conversational comment for the Open Graph block, decided not to add contextual links, and decided against Event structured data because my workshops are examples. I made every code edit myself in VS Code and pushed through GitHub Desktop.