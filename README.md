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