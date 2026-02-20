# Course Redesign Design: Collecting Digital Data

**Date:** 2026-02-20
**Course date:** 2026-02-24, 10:00-16:00 (online)
**Instructor:** Dr Diarmuid McDonnell (Braw Data Ltd / Gradel Institute of Charity, Oxford)
**Status:** Approved

## Overview

Redesign of the SGSSS "Collecting Digital Data" one-day training course for social science PhD students. Key changes from the 2025 version: shift emphasis from web scraping to APIs, add LLM-as-coding-assistant content, produce accessible SGSSS-branded Beamer slide decks, and provide all practicals in both Python and R as Google Colab notebooks.

## Schedule

| Time | Session | Format | Deliverable |
|------|---------|--------|-------------|
| 10:00-10:30 | Lecture 1: Welcome, About the Instructor, How the Web Works | Mini-lecture (Beamer) | `lecture-1-welcome-and-how-the-web-works.tex` |
| 10:30-11:15 | Practical 1: Web Scraping (condensed) | Colab notebook | `practical-1-web-scraping-2026-02-24-{Python,R}.ipynb` |
| 11:15-11:30 | Break | | |
| 11:30-11:45 | Lecture 2: What Are APIs? | Mini-lecture (Beamer) | `lecture-2-what-are-apis.tex` |
| 11:45-12:45 | Practical 2: UK Police API Deep-Dive | Colab notebook | `practical-2-uk-police-api-2026-02-24-{Python,R}.ipynb` |
| 12:45-13:30 | Lunch | | |
| 13:30-13:45 | Lecture 3: API Landscape Survey | Mini-lecture (Beamer) | `lecture-3-api-landscape.tex` |
| 13:45-14:45 | Practical 3: API Challenge | Colab notebook | `practical-3-api-challenge-2026-02-24-{Python,R}.ipynb` |
| 14:45-15:00 | Break | | |
| 15:00-15:15 | Lecture 4: LLMs as Coding Assistants | Mini-lecture (Beamer) | `lecture-4-llms-as-coding-assistants.tex` |
| 15:15-15:50 | Practical 4: LLM Showdown | Colab notebook | `practical-4-llm-showdown-2026-02-24-{Python,R}.ipynb` |
| 15:50-16:00 | Wrap-up, resources, Q&A | | |

## Lecture Content

### Lecture 1: Welcome & How the Web Works (10:00-10:30, ~8-10 slides)

- Welcome and housekeeping: course outline, Colab setup instructions, Python vs R (instructor demos Python, R notebooks available)
- About the instructor: Dr Diarmuid McDonnell, affiliations, research interests
- Why collect digital data? Motivating social science examples
- How the web works: HTTP request-response cycle, URLs, status codes. TikZ diagram of client-server interaction.
- HTML basics: tags, elements, nesting. TikZ tree of HTML structure.
- Structured vs unstructured data: JSON key-value pairs vs raw HTML. Visual comparison.
- Ethical and legal considerations: robots.txt, Terms of Service, rate limiting, personal data, when to prefer APIs over scraping

### Lecture 2: What Are APIs? (11:30-11:45, ~6-8 slides)

- What is an API? Translator/intermediary analogy
- APIs vs web scraping: structured data, reliability, rate limits, authentication, legality. Make the case for APIs as preferred approach.
- Anatomy of an API call: base URL, endpoints, parameters, headers, authentication. TikZ diagram.
- Reading API documentation: endpoints, rate limits, auth requirements, response format
- JSON deep-dive: nested structures, arrays of objects, navigation. TikZ nested boxes.

### Lecture 3: API Landscape Survey (13:30-13:45, ~6-8 slides)

- Categories of useful APIs: government open data, social media, academic/bibliometric, geospatial, international organisations
- 1 slide each for 5-6 APIs: UK Parliament, World Bank Indicators, OpenAI/Anthropic, ONS, OpenStreetMap/Nominatim
- Curated list resource (public-apis GitHub repo)
- Preview of Practical 3 API options

### Lecture 4: LLMs as Coding Assistants (15:00-15:15, ~6-8 slides)

- What are LLMs? Brief non-technical overview
- Paid vs open models: ChatGPT/Claude vs Llama/Mistral. Practical differences for researchers.
- How to prompt for code: good prompt structure, iterative refinement
- What LLMs are good/bad at: boilerplate and syntax (good), complex logic and up-to-date API details (bad)
- Critical evaluation: understanding code yourself, reproducibility, hallucinated functions, security risks
- Closing slide: instructor contact details, Braw Data link, resources

## Practical Content

### Practical 1: Web Scraping (10:30-11:15, ~45 min)

Condensed from two previous practicals into one. Three sections:

1. **Simple text extraction (~15 min):** httpbin.org/html example. Request, parse with BeautifulSoup/rvest, extract paragraph, save to file. Teaches request-parse-extract-save workflow.
2. **Multi-page scraping (~20 min):** Edinburgh Council warm spaces directory. Loop over A-Z pages, extract org names and links, visit each org page. Demonstrates loops, conditionals, building datasets.
3. **Exercise (~10 min):** Scrape library locations from same Council site. Skeleton code with gaps.

Changes from 2025: remove file download example, add closing note about preferring APIs. Retain "guide to using this resource" boilerplate for asynchronous learners.

### Practical 2: UK Police API Deep-Dive (11:45-12:45, ~60 min)

Expanded from previous single API practical. Four sections:

1. **First API call (~10 min):** Forces endpoint, inspect JSON, status codes, headers.
2. **Working with JSON (~15 min):** Lists, dictionaries, extracting fields, list comprehensions.
3. **Parameterised requests and looping (~20 min):** Stop-and-search for one force, then all forces. Error handling, rate limiting with time.sleep. Promoted from previous appendix.
4. **From JSON to analysis (~15 min):** Convert to DataFrame/tibble, cross-tabulations, simple bar chart visualisation (new addition).

### Practical 3: API Challenge (13:45-14:45, ~60 min)

New notebook. Students choose from 2-3 APIs:

- **Option A: UK Parliament API** — starter code for list of MPs, tasks to extend (filter by party, voting records)
- **Option B: World Bank Indicators API** — starter code for GDP data, tasks to extend (multiple countries, time series)
- **Option C: ONS API** — starter code for a dataset, tasks to extend

Each option: ~50% scaffolding with gaps. Solutions in appendix.

### Practical 4: LLM Showdown (15:15-15:50, ~35 min)

New session. Structure:

1. **Setup (~5 min):** Explain the exercise.
2. **Define prompts (~5 min):** Class defines 2-3 prompts based on the day's tasks (e.g., "scrape Edinburgh warm spaces", "download stop-and-search for all forces", "request World Bank GDP data in R").
3. **Live demo (~15 min):** Run prompts through ChatGPT, Claude, and an open model. Compare outputs side by side. Does code run? Is it correct?
4. **Discussion (~10 min):** What did LLMs do well/badly? Would you trust this in research? How should you use these tools?

Notebook is a structured worksheet: prompts, space for LLM outputs, evaluation criteria cells.

## Beamer Theme & Accessibility

- **Theme:** metropolis with SGSSS colour overrides
- **Fonts:** Fira Sans (body), Fira Mono (code)
- **SGSSS branding:** logo on title slide, small footer on subsequent slides
- **TikZ diagrams:** HTTP request-response, HTML tree, API architecture, JSON structure, LLM workflow
- **Accessibility:** WCAG AA contrast ratios, no colour-only information, minimum 20pt body / 14pt code, alt-text in TikZ comments, colour-blind-safe code highlighting via minted/listings
- **Slide structure:** title slide, section dividers, content slides (max 5-6 bullets or one diagram), full-width code slides

## File Structure

```
collecting-digital-data/
├── presentations/
│   ├── lecture-1-welcome-and-how-the-web-works.tex
│   ├── lecture-2-what-are-apis.tex
│   ├── lecture-3-api-landscape.tex
│   └── lecture-4-llms-as-coding-assistants.tex
├── code/
│   ├── practical-1-web-scraping-2026-02-24-Python.ipynb
│   ├── practical-1-web-scraping-2026-02-24-R.ipynb
│   ├── practical-2-uk-police-api-2026-02-24-Python.ipynb
│   ├── practical-2-uk-police-api-2026-02-24-R.ipynb
│   ├── practical-3-api-challenge-2026-02-24-Python.ipynb
│   ├── practical-3-api-challenge-2026-02-24-R.ipynb
│   ├── practical-4-llm-showdown-2026-02-24-Python.ipynb
│   └── practical-4-llm-showdown-2026-02-24-R.ipynb
├── img/
│   └── SGSSS_Stacked.png
├── docs/
│   └── plans/
│       └── 2026-02-20-course-redesign-design.md
├── admin/
├── previous-course/
└── README.md
```

## Key Design Decisions

- **APIs over scraping:** 1 scraping practical vs 2 API practicals + 1 API challenge
- **LLMs as coding assistants:** dedicated end-of-day benchmarking session, not woven throughout
- **UK Police API retained:** proven, no-auth, criminology/sociology relevance
- **Beamer with TikZ:** metropolis theme, SGSSS branding, vector diagrams, accessible
- **Google Colab:** free, no install, proven platform, Python + R support
- **Self-contained notebooks:** retain boilerplate guide for asynchronous learners
- **Instructor slide:** Dr Diarmuid McDonnell at start; contact/links at end
