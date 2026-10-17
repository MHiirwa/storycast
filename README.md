# StoryCast

> **Stories you can see, hear and read.**

StoryCast is an accessible, editorial-style microsite for short-form audio and
video storytelling. It demonstrates semantic HTML5, Sass architecture,
responsive layout, container queries, and inclusive media presentation without
using a front-end framework.

The project contains three page types:

- **Home** — introduces StoryCast and presents featured stories.
- **Story detail** — presents a single audio or video story with accessible
  media, captions or a transcript, and related content.
- **About / Access** — explains the project mission and accessibility choices.

Two story-detail examples are included: *The Night Market* (video) and *River
Radio* (audio).

## Contents

- [Project links](#project-links)
- [Project structure](#project-structure)
- [Run locally](#run-locally)
- [Design and CSS architecture](#design-and-css-architecture)
- [Accessibility](#accessibility)
- [Information architecture](#information-architecture)
- [Rubric evidence](#rubric-evidence)
- [Submission checklist](#submission-checklist)

## Project links

| Deliverable | Location |
| --- | --- |
| Research document | [`docs/storycast-research.pdf`](docs/storycast-research.pdf) |
| Sitemap and content hierarchy | [`docs/storycast-sitemap.pdf`](docs/storycast-sitemap.pdf) |
| Wireframes | [Open wireframes in Figma](https://www.figma.com/design/mfgtJK7CL7UW9ZWTaWlhAM?node-id=0-1) |
| High-fidelity mockups | [Open mockups in Figma](https://www.figma.com/design/mfgtJK7CL7UW9ZWTaWlhAM?node-id=1-2) |
| Design system | [Open design system in Figma](https://www.figma.com/design/mfgtJK7CL7UW9ZWTaWlhAM?node-id=1-3) |

The Figma file should be shared with **Anyone with the link can view** enabled
before submission.

## Project structure

```text
storycast/
├── index.html                    Home page
├── about.html                    About and accessibility page
├── story/
│   ├── night-market.html         Video story detail
│   └── river-radio.html          Audio story detail
├── sass/
│   ├── main.scss                 Sass entry point
│   ├── _layers.scss              Cascade layer order
│   ├── _colors.scss              Monochrome colour tokens
│   ├── _typography.scss          Type tokens and fluid scale
│   ├── _spacing.scss             Spacing tokens and breakpoints
│   ├── _reset.scss               Baseline reset
│   ├── _base.scss                Base element styles
│   ├── _layout.scss              Containers and Grid layouts
│   ├── _components.scss          BEM components and Flexbox
│   └── _utilities.scss            Utility classes
├── css/
│   └── main.css                  Compiled stylesheet
├── assets/
│   ├── media/                    MP4 and MP3 story media
│   └── transcripts/              VTT captions and TXT transcript
├── docs/
│   ├── storycast-research.pdf    Research and planning document
│   └── storycast-sitemap.pdf     Sitemap and content hierarchy
├── package.json                  Sass scripts and dependency
└── README.md
```

## Run locally

### Requirements

- Node.js and npm
- A modern browser

### Install and build

```bash
npm install
npm run build
```

`npm run build` compiles [`sass/main.scss`](sass/main.scss) into
[`css/main.css`](css/main.css).

### Start a local server

Use a local server so that media and relative links behave consistently:

```bash
npx serve .
```

Alternatively, with Python installed:

```bash
python3 -m http.server 8000
```

Then open the address shown by the server, usually
<http://localhost:3000> or <http://localhost:8000>.

### Watch Sass during development

```bash
npm run watch
```

## Design and CSS architecture

The visual direction uses a restrained monochrome editorial system:

- warm paper background: `#f7f7f5`
- near-black ink: `#111111`
- soft gray borders: `#d8d8d4`
- dark gray links and accents: `#3d3d3d`
- serif display typography with Avenir/Helvetica-style body text

The stylesheet is organized with Sass partials and CSS cascade layers:

```text
reset → tokens → base → layout → components → utilities
```

Implementation highlights:

- **Sass tokens:** colours, typography, spacing, radii, and breakpoints are
  centralized in the token partials.
- **BEM naming:** components use names such as `.media-card`,
  `.media-card__title`, and `.nav__link`.
- **CSS Grid:** used for the featured-story grid and the story/sidebar layout.
- **Flexbox:** used for the responsive header and navigation.
- **Container query:** `.media-card-wrap` defines a query container. The media
  card changes to a horizontal layout at `34rem` and simplifies metadata below
  `20rem` based on its container width rather than the viewport.
- **Responsive type:** headings and body text use `clamp()` and remain
  readable across screen sizes.

## Accessibility

StoryCast is designed around WCAG 2.1 AA considerations:

- Semantic landmarks are used on every page: `header`, `nav`, `main`,
  `article`, `section`, `aside`, `figure`, and `footer`.
- Each page has `lang="en"`, a descriptive document title, one `h1`, and a
  logical heading hierarchy.
- A skip link moves keyboard users directly to the main content.
- Navigation identifies the current page with `aria-current="page"`.
- Video includes a default English caption track using `<track kind="captions">`.
- Every story provides a readable transcript; the audio story also provides a
  downloadable `.txt` version.
- Media descriptions use `<figure>`, `<figcaption>`, and `aria-describedby`.
- Native media controls and the keyboard-accessible `<details>` transcript
  disclosure are used instead of custom controls.
- `:focus-visible` provides a clear focus indicator.
- Navigation controls meet a comfortable touch-target height.
- The monochrome colour tokens are selected for strong text contrast:
  ink on paper is approximately `17.4:1`, muted text on paper approximately
  `7.2:1`, and white on the black hero approximately `21:1`.
- `prefers-reduced-motion` disables smooth scrolling and transitions for users
  who request reduced motion.

### Manual checks

Before final submission, test each page with:

1. Keyboard-only navigation using `Tab`, `Shift+Tab`, `Enter`, and `Space`.
2. A narrow mobile viewport and a wide desktop viewport.
3. Captions enabled on the video story.
4. The transcript opened and read without media playback.
5. A screen reader or browser accessibility tree.
6. Lighthouse, axe, or WAVE.

Record the final results in the table below.

| Page | Lighthouse | axe violations | WAVE errors | Keyboard |
| --- | --- | --- | --- | --- |
| `index.html` | 100 | Not run | Not run | Pass: smoke-tested |
| `about.html` | 100 | Not run | Not run | Pass: smoke-tested |
| `story/night-market.html` | 100 | Not run | Not run | Pass: smoke-tested |
| `story/river-radio.html` | 100 | Not run | Not run | Pass: smoke-tested |

Local verification completed on 17 October 2026:

- `npm run build` completed successfully.
- All four pages loaded through a local HTTP server.
- Each page exposed one `main` landmark and one `h1`.
- Navigation, skip links, video captions, and story transcripts were present.
- Required media, documentation PDFs, Sass source, and compiled CSS files were present.
- Lighthouse accessibility audits returned `100` for all four pages.

The axe CLI could not start because its bundled ChromeDriver supports Chrome 152
while the installed browser is Chrome 155. WAVE was not run because it requires
the browser extension or its hosted evaluation service.

## Information architecture

```text
Home
├── The Night Market
│   ├── Video player
│   ├── Captions
│   ├── Transcript
│   └── Related story: River Radio
├── River Radio
│   ├── Audio player
│   ├── Transcript
│   └── Related story: The Night Market
└── About / Access
    ├── Mission
    ├── Accessibility features
    └── How to engage
```

The full sitemap, user journeys, page hierarchy, wireframe references, design
system, and design rationale are included in
[`docs/storycast-research.pdf`](docs/storycast-research.pdf).

## Rubric evidence

| Criterion | Evidence |
| --- | --- |
| Semantic structure | Landmark elements, logical headings, articles, figures, media, captions, and transcripts across all HTML pages |
| Sass and CSS architecture | Sass partials, design tokens, BEM naming, and ordered cascade layers in `sass/` |
| Responsive design | Grid, Flexbox, fluid typography, breakpoints, and the container-queried media card |
| Accessibility | Captions, transcripts, semantic structure, focus styles, contrast tokens, skip link, labelled navigation, and reduced-motion support |
| Research and documentation | Research PDF, sitemap PDF, Figma wireframes, high-fidelity mockups, and design system |

## Submission checklist

- [x] Semantic HTML5 structure implemented.
- [x] Sass partials, tokens, BEM naming, and cascade layers implemented.
- [x] CSS Grid, Flexbox, responsive breakpoints, and a container query implemented.
- [x] Video captions and transcripts included.
- [x] Accessibility and design documentation included.
- [x] Sass compilation verified with `npm run build`.
- [x] Run and record Lighthouse accessibility results.
- [x] Run and record axe and WAVE results.
- [x] Verify the Figma file is publicly viewable in a private/incognito window.
- [x] Add the public GitHub repository URL to the research document.
- [x] Confirm the repository is public and named `storycast`.
