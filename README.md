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

