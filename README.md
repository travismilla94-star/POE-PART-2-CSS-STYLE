# Ubuntu Paws Animal Rescue — Website Project

## Student Information
- **Full Name:** [Your Full Name]
- **Student Number:** [Student Number]
- **Subject:** [Subject Name and Code]
- **Group:** [Group, if applicable]

## Project Overview
Ubuntu Paws Animal Rescue is a fictional, volunteer-run non-profit organisation based in
Johannesburg, Gauteng, dedicated to rescuing, rehabilitating and rehoming abandoned and
injured animals. This repository contains the HTML, CSS and (in later parts) JavaScript
for a functional, responsive, SEO-friendly website built for this organisation as part of
the Website Development Project of Learning (PoE).

The organisation currently has no website and relies solely on a Facebook page, which
limits discoverability and does not support structured adoption, volunteer or sponsorship
enquiries. This website addresses that gap.

## Website Goals and Objectives
- Increase adoption enquiries by giving the shelter's available animals an online presence.
- Grow the volunteer and foster-carer base through an accessible enquiry process.
- Raise donation and sponsorship income by clearly communicating how funds are used.
- **KPIs:** number of adoption enquiries per month, volunteer/sponsor sign-ups, and
  overall page visits, tracked from launch.

## Key Features and Functionality
- Responsive navigation menu linking every page on the site.
- Homepage with a hero section and calls to action to adopt, volunteer or donate.
- About Us page covering the organisation's history, mission, vision and team.
- Services page listing adoptable animals and the rescue/rehabilitation process.
- Enquiry page with a form covering adoption, volunteering and sponsorship enquiries.
- Contact page listing two physical locations (main shelter and foster care office)
  with a general contact form.

## Timeline and Milestones
| Milestone | Description | Status |
|---|---|---|
| Part 1 | Project planning, proposal, HTML structure | Complete |
| Part 2 | CSS styling and responsive design | Complete |
| Part 3 | JavaScript functionality and final testing | Planned |

## Part 1 Details

### Sitemap
```
Homepage (index.html)
 ├── About Us (about.html)
 ├── Services (services.html)
 ├── Enquiry (enquiry.html)
 └── Contact (contact.html)
```
All five pages share a common header, navigation menu and footer. The navigation
menu links to every page and highlights the current page with an `active` class.

### File and Folder Structure
```
ubuntu-paws/
├── index.html
├── about.html
├── services.html
├── enquiry.html
├── contact.html
├── css/
│   └── style.css
├── js/
│   └── main.js
├── images/
│   └── (sourced/licensed images)
├── documents/
│   └── (supporting documents, e.g. researched content)
└── README.md
```

## Part 2 Details
This section maps directly onto the Part 2 brief ("Designing the Visuals: CSS
Styling and Responsive Design") so each requirement is easy to check against
what was actually built.

### 2.1 External stylesheet
All styling lives in one external file, `css/style.css`, linked from every
HTML page's `<head>` with `<link rel="stylesheet" href="css/style.css">`.
Filenames follow a consistent lower-case, hyphenated naming convention
throughout the project (`style.css`, `hero-mobile.svg`, `favicon.svg`, etc.).

### 2.2 Base style
A reset at the top of the stylesheet (`*, *::before, *::after { box-sizing:
border-box; margin: 0; padding: 0; }`) removes inconsistent browser defaults.
Base font family, size, colour and line-height are set once on `body` and
inherited everywhere. A `:root` block defines the full colour scheme
(`--color-primary`, `--color-secondary`, etc.) and spacing scale
(`--space-xs` to `--space-xl`) as CSS custom properties, so every margin,
padding and colour in the file references one of a small set of values
instead of repeating magic numbers — this is also what keeps selector counts
low (see 2.4/2.5 below): most components reuse the same handful of variables
rather than each needing its own bespoke declarations.

### 2.3 Typography styles
`font-family`, `font-size`, `font-weight`, `line-height` and `letter-spacing`
are all set explicitly on `h1`/`h2`/`h3`/`p`. Two Google Fonts are used —
Poppins for headings, Nunito Sans for body text — loaded via `<link>` tags.
A typographic scale is defined once as custom properties (`--fs-sm` through
`--fs-2xl`) and reused by every heading and text element, with `clamp()` on
the two largest sizes so headings scale smoothly across breakpoints instead
of jumping abruptly.

### 2.4 Layout structure
- **CSS Grid:** the page shell (`header`/`main`/`footer`) is laid out with
  `display: grid` and `grid-template-areas` on `<body>`. The homepage hero
  becomes a two-column grid (`grid-template-columns: 1.1fr 1fr`) from 900px
  up. The contact page uses `grid-template-areas` to place the location
  cards beside the message form on wider screens. Card collections
  (highlights, animals, team members, locations) all use
  `display: grid` with `grid-template-columns` that change per breakpoint.
- **Flexbox:** the header uses `display: flex` with `justify-content:
  space-between` and `align-items: center` to position the logo and nav.
  Buttons and form rows use `flex-direction`, `align-items` and `gap` to
  align icons with text.

### 2.5 Visual styles
Cards and buttons use `background-color` (and gradient `background`),
`border`/`border-top`, `border-radius` and `box-shadow` for depth. Every
interactive element has all three required pseudo-class states:
- `:hover` — nav pills highlight, buttons lift, cards lift with a larger
  shadow, form field borders darken.
- `:focus-visible` — buttons and form fields get a visible outline/glow so
  the site is usable by keyboard, matching the same colour as `:hover`.
- `:active` — buttons compress slightly (`transform: scale(0.97)`) to give
  tactile click feedback.

### 3.1 Breakpoints
Three explicit breakpoints are used, mobile-first (base styles are mobile,
each `@media` rule adds/overrides for larger screens):
- **Mobile** — base styles, up to 599px: single-column layout throughout,
  stacked navigation, one-column card grids.
- **Tablet** — `@media (min-width: 600px)`: card grids move to 2–3 columns.
- **Small desktop** — `@media (min-width: 900px)`: the hero becomes
  two-column, the contact page splits into a two-column grid, animal/team
  card grids gain another column.
- **Large desktop** — `@media (min-width: 1200px)`: the max content width
  and hero padding increase slightly for very wide screens.

### 3.2 Relative units
Font sizes and spacing use `rem` (scales with the user's root font size) and
`em` (scales with the local font size, e.g. icon sizing relative to their
button's text). Grid columns use `fr` units, and the full-bleed stats band
uses `vw`/`%`-based widths so it always spans the true viewport width
regardless of the page's max-width container.

### 3.3 Responsive images
The homepage hero uses a `<picture>` element with a `<source media="(min-
width: 900px)" srcset="images/hero-desktop.svg">` and a fallback `<img
src="images/hero-mobile.svg">` — an **art-directed** responsive image: a
simpler, tighter illustration is served on narrow screens and a fuller scene
on wide screens, rather than just scaling the same image. Both files are
original SVG illustrations built for this project (see References), so there
are no licensing concerns.

### 3.4 Test and iterate
Tested using browser developer tools' device toolbar at mobile (~375px),
tablet (~768px) and desktop (~1280px+) widths, confirming the nav, card
grids, hero layout and contact page all adapt correctly at each breakpoint.

**TODO before submission:** add screenshots of the site at mobile, tablet and
desktop widths to this README (or to `images/` and reference them here), as
required by the brief.

### Visual design (beyond the core rubric)
On top of the requirements above, the site also uses original SVG
illustrations (`images/hero-mobile.svg`, `images/hero-desktop.svg`,
`images/favicon.svg`) hand-built for this project, small inline SVG icons
throughout, gradient buttons/header, a full-bleed diagonal stats band
(`clip-path`), initials-based team avatars, an "Available!" ribbon on animal
cards, icon-prefixed form fields, a floating "Adopt & Donate" button, and a
`prefers-reduced-motion`-aware fade-in entrance animation. None of this was
explicitly required by the brief, but it builds on the same techniques
(Grid/Flexbox, custom properties, pseudo-classes) rather than replacing them.

## Changelog
Track changes and improvements to the website here as the project progresses.

| Date | Change | Author |
|---|---|---|
| [Date] | Initial project structure, HTML pages for all 5 sitemap pages, base stylesheet, and README created for Part 1. | [Your Full Name] |
| [Date] | Part 2: Rebuilt `css/style.css` with CSS custom properties, a typography scale (Google Fonts: Poppins/Nunito Sans), CSS Grid page layout (`grid-template-areas`) and Flexbox navigation, `:hover`/`:focus-visible`/`:active` states on links, buttons and form fields, and mobile-first responsive breakpoints at 600px/900px/1200px. Added a responsive `<picture>`/`srcset` hero image to `index.html` and a two-column grid layout to `contact.html` on wider screens. | [Your Full Name] |
| [Date] | Part 2 visual design pass: added original SVG artwork (`hero-mobile.svg`, `hero-desktop.svg`, `favicon.svg`) and inline SVG icons across all pages; restructured the homepage hero into a two-column CSS Grid (art-directed responsive image); added a full-bleed stats band, icon badges, gradient buttons/header, card hover/lift effects, and a `prefers-reduced-motion`-aware fade-in entrance animation. | [Your Full Name] |
| [Date] | Part 2 visual polish pass 2: diagonal `clip-path` on the stats band; initials-based avatars on the team list; an "Available!" ribbon badge on animal cards; icon-prefixed form fields (email/phone/name, via inline SVG `background-image`); a fixed floating "Adopt & Donate" call-to-action button; a "Back to top" footer link; trust-badge pills in the hero; a decorative blob behind inner-page headings; and a button hover "shine" sweep. | [Your Full Name] |
| [Date] | Part 2 colour expansion: extended the palette from 2 to 4 brand colours (teal, orange, gold, blue) via new custom properties/gradients; applied them to cycle across icon badges, team avatars, animal-card and location-card accents, and the header background; added a blue collar and gold bow tie to the hero illustration's dog and cat, and gave each scattered paw print a different palette colour. | [Your Full Name] |
| [Date] | Part 1 feedback corrections: *(no specific Part 1 feedback was available at the time of this edit — add entries here once feedback is received and addressed)*. | [Your Full Name] |

## References
References are cited using the Harvard Style Referencing Guide, adapted for the IIE.
References specific to each Website Project Proposal are included in the
*Website Project Proposal* document. General references used to complete Part 1 are
listed below and will be updated with new references as required in Part 2 and Part 3.

- [Author/Organisation. (Year). *Title of source*. Retrieved from URL — add each
  source you actually use for code snippets, text content, or images.]
- Google. (2026). *Google Fonts: Poppins & Nunito Sans*. Retrieved from https://fonts.google.com/
- All illustrations and icons (`images/hero-mobile.svg`, `images/hero-desktop.svg`, `images/favicon.svg`, and inline page icons) are original vector artwork created for this project — no external image sources used.

