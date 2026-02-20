# Collecting Digital Data: Course Redesign Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Produce all teaching materials (4 Beamer slide decks, 8 Colab notebooks, README) for the SGSSS "Collecting Digital Data" course on 24 February 2026.

**Architecture:** A shared Beamer preamble file defines the SGSSS-branded metropolis theme, used by all 4 lecture `.tex` files. Jupyter notebooks are self-contained `.ipynb` files for Google Colab, each with a Python and R version. A `README.md` at the project root links to all materials with Colab badges.

**Tech Stack:** LaTeX/Beamer with metropolis theme, TikZ, minted for code highlighting. Jupyter notebooks (`.ipynb` JSON format) for Google Colab. Python (requests, BeautifulSoup, pandas, matplotlib, json) and R (httr/httr2, rvest, jsonlite, dplyr, ggplot2).

**Design doc:** `docs/plans/2026-02-20-course-redesign-design.md`

**Previous course materials:** `previous-course/` (reference only, do not modify)

**SGSSS brand colours (from logo):**
- Magenta/purple: `#A3217A` (RGB 163, 33, 122) — thistle petals, Gaelic text
- Dark green: `#2D6A3F` (RGB 45, 106, 63) — thistle leaves, triangle
- Black: `#1D1D1B` — English text
- White: `#FFFFFF` — backgrounds

---

## Task 1: Set up directory structure and copy assets

**Files:**
- Create: `collecting-digital-data/presentations/` (directory)
- Create: `collecting-digital-data/code/` (directory)
- Create: `collecting-digital-data/img/` (directory)
- Copy: `admin/SGSSS_Stacked.png` to `img/SGSSS_Stacked.png`

**Step 1: Create directories**

```bash
mkdir -p collecting-digital-data/presentations
mkdir -p collecting-digital-data/code
mkdir -p collecting-digital-data/img
```

**Step 2: Copy logo**

```bash
cp collecting-digital-data/admin/SGSSS_Stacked.png collecting-digital-data/img/SGSSS_Stacked.png
```

**Step 3: Verify**

```bash
ls -R collecting-digital-data/presentations collecting-digital-data/code collecting-digital-data/img
```

Expected: empty `presentations/` and `code/` directories; `img/` contains `SGSSS_Stacked.png`.

---

## Task 2: Create shared Beamer preamble

**Files:**
- Create: `collecting-digital-data/presentations/sgsss-beamer-preamble.tex`

This file is `\input{}` by all 4 lecture `.tex` files to keep theming DRY.

**Step 1: Write the preamble file**

The preamble must:
- Load metropolis theme
- Override colours with SGSSS brand (magenta `#A3217A` as primary/accent, dark green `#2D6A3F` for structure/examples, black for body text, white backgrounds)
- Set Fira Sans (body) and Fira Mono (code) fonts
- Load TikZ with required libraries (arrows.meta, positioning, shapes, trees, calc, decorations.pathmorphing)
- Load minted for syntax-highlighted code blocks with a colour-blind-safe style
- Configure slide footer with small SGSSS logo and page number
- Set minimum font sizes: 20pt body, 14pt code blocks
- Define reusable TikZ styles for diagrams (e.g., `server node`, `client node`, `api node`, `arrow style`)
- Define convenience commands: `\pythoncode{}`, `\rcode{}` for inline code snippets

**Content of `sgsss-beamer-preamble.tex`:**

```latex
% SGSSS Beamer Preamble — shared across all lectures
% Brand colours from SGSSS logo

\usetheme{metropolis}

% --- Colour definitions ---
\definecolor{sgsssMagenta}{HTML}{A3217A}
\definecolor{sgsssGreen}{HTML}{2D6A3F}
\definecolor{sgsssBlack}{HTML}{1D1D1B}
\definecolor{sgsssWhite}{HTML}{FFFFFF}
\definecolor{sgsssLightGrey}{HTML}{F5F5F5}

% --- Metropolis colour overrides ---
\setbeamercolor{palette primary}{bg=sgsssMagenta, fg=sgsssWhite}
\setbeamercolor{title separator}{fg=sgsssGreen}
\setbeamercolor{progress bar}{fg=sgsssGreen, bg=sgsssLightGrey}
\setbeamercolor{frametitle}{bg=sgsssMagenta, fg=sgsssWhite}
\setbeamercolor{alerted text}{fg=sgsssMagenta}
\setbeamercolor{example text}{fg=sgsssGreen}
\setbeamercolor{block title}{bg=sgsssMagenta, fg=sgsssWhite}
\setbeamercolor{block body}{bg=sgsssLightGrey, fg=sgsssBlack}
\setbeamercolor{block title example}{bg=sgsssGreen, fg=sgsssWhite}
\setbeamercolor{block body example}{bg=sgsssLightGrey, fg=sgsssBlack}
\setbeamercolor{normal text}{fg=sgsssBlack}

% --- Fonts ---
\usepackage[sfdefault]{FiraSans}
\usepackage{FiraMono}
\setbeamerfont{frametitle}{size=\large}

% --- Packages ---
\usepackage{graphicx}
\usepackage{hyperref}
\usepackage{booktabs}
\usepackage{minted}
\usepackage{fontawesome5}

% --- TikZ ---
\usepackage{tikz}
\usetikzlibrary{arrows.meta, positioning, shapes.geometric, trees, calc, decorations.pathmorphing, fit, backgrounds}

% Reusable TikZ styles
\tikzset{
    server node/.style={rectangle, draw=sgsssGreen, fill=sgsssGreen!10, thick, minimum width=2.5cm, minimum height=1.2cm, align=center, font=\small},
    client node/.style={rectangle, draw=sgsssMagenta, fill=sgsssMagenta!10, thick, minimum width=2.5cm, minimum height=1.2cm, align=center, font=\small},
    api node/.style={rectangle, draw=sgsssGreen, fill=sgsssGreen!15, thick, rounded corners, minimum width=2.5cm, minimum height=1.2cm, align=center, font=\small},
    data node/.style={rectangle, draw=sgsssBlack, fill=sgsssLightGrey, thick, minimum width=2cm, minimum height=1cm, align=center, font=\small},
    arrow style/.style={-{Stealth[length=3mm]}, thick, sgsssBlack},
    html tag/.style={rectangle, draw=sgsssMagenta, fill=sgsssMagenta!8, rounded corners=2pt, font=\ttfamily\small, inner sep=4pt},
    json key/.style={rectangle, draw=sgsssGreen, fill=sgsssGreen!8, rounded corners=2pt, font=\ttfamily\small, inner sep=4pt},
}

% --- Minted configuration ---
\setminted{
    fontsize=\footnotesize,
    frame=leftline,
    framesep=2mm,
    baselinestretch=1.1,
    bgcolor=sgsssLightGrey,
    breaklines,
    linenos=false,
}
\setminted[python]{style=friendly}
\setminted[r]{style=friendly}

% --- Convenience commands ---
\newcommand{\pythoncode}[1]{\mintinline{python}{#1}}
\newcommand{\rcode}[1]{\mintinline{r}{#1}}
\newcommand{\httpstatus}[2]{\texttt{#1} \textit{#2}}

% --- Footer with SGSSS logo ---
\setbeamertemplate{frame footer}{%
    \includegraphics[height=0.6cm]{../img/SGSSS_Stacked.png}\hfill%
    \insertframenumber/\inserttotalframenumber%
}

% --- Metadata ---
\author{Dr Diarmuid McDonnell}
\institute{Braw Data Ltd \and Gradel Institute of Charity, University of Oxford}
\date{24 February 2026}
```

**Step 2: Verify syntax**

Create a minimal test `.tex` file that inputs the preamble, compile it, and check for errors. Delete test file after.

---

## Task 3: Create Lecture 1 — Welcome & How the Web Works

**Files:**
- Create: `collecting-digital-data/presentations/lecture-1-welcome-and-how-the-web-works.tex`

**Step 1: Write the lecture file**

The file must `\input{sgsss-beamer-preamble}` and contain the following slides:

1. **Title slide** — Course title "Collecting Digital Data: The Role of Web-scraping and APIs", SGSSS logo (large), instructor name, date
2. **About the instructor** — Dr Diarmuid McDonnell, Director of Braw Data Ltd, Visiting Fellow at Gradel Institute of Charity (University of Oxford). Research: geographic distribution of civil society activity. Link to team page.
3. **Course outline** — Table of the day's schedule (times, sessions, formats). Highlight that practicals are on Google Colab, available in Python and R.
4. **Getting set up** — Instructions for accessing Colab notebooks (link to README, Google account requirement). Screenshot or mock-up of Colab interface.
5. **Why collect digital data?** — 3-4 motivating examples: government open data for policy research, social media for opinion analysis, organisational websites for third-sector research, administrative records. Keep to bullet points.
6. **How the web works** — TikZ diagram: client (Your Computer) sends HTTP Request (with URL) to Server, Server returns HTTP Response (with status code + content). Label the arrows with "GET https://..." and "200 OK + HTML/JSON". Below diagram, brief text on common status codes (200, 404, 500).
7. **HTML basics** — TikZ tree diagram: `<html>` at root, branches to `<head>` and `<body>`, `<body>` branches to `<div>`, `<h1>`, `<p>`. Annotate with "tags define structure". Below, show a tiny HTML snippet with colour-coded tags using minted.
8. **Structured vs unstructured data** — Two-column slide. Left: "Unstructured" with a minted HTML snippet. Right: "Structured" with a minted JSON snippet. Brief comparison bullets underneath.
9. **Ethics and legality** — Bullet points: check robots.txt, read Terms of Service, respect rate limits, consider personal data (GDPR), prefer APIs when available, web scraping as last resort. Note: "We will discuss these further throughout the day."
10. **Next up** — "Practical 1: Web Scraping" — brief preview of what students will do.

**Step 2: Compile and verify**

```bash
cd collecting-digital-data/presentations && latexmk -pdf -shell-escape lecture-1-welcome-and-how-the-web-works.tex
```

Expected: PDF with 10 slides, SGSSS branding, all TikZ diagrams render, minted code blocks display.

---

## Task 4: Create Lecture 2 — What Are APIs?

**Files:**
- Create: `collecting-digital-data/presentations/lecture-2-what-are-apis.tex`

**Step 1: Write the lecture file**

Slides:

1. **Section title** — "What Are APIs and Why Use Them?"
2. **What is an API?** — The translator analogy. TikZ diagram: three nodes (Your Application, API, Database/Service) with bidirectional arrows. Label arrows "Request" and "Response". Brief text: "An API simplifies how applications communicate with each other."
3. **APIs vs web scraping** — Two-column comparison table using booktabs:

   | | Web Scraping | APIs |
   |---|---|---|
   | Data format | Unstructured HTML | Structured JSON/XML |
   | Reliability | Breaks when site changes | Versioned, documented |
   | Legality | Grey area | Usually explicit ToS |
   | Rate limits | You must self-impose | Enforced by provider |
   | Authentication | Usually none | Often API key |

4. **Anatomy of an API call** — TikZ diagram showing the components of a URL: `https://data.police.uk/api/stops-force?force=city-of-london&date=2024-01`. Annotate each part: base URL, endpoint, parameters. Plus headers and authentication as separate boxes.
5. **Reading API documentation** — What to look for: checklist with icons (fontawesome5). Endpoints, authentication method, rate limits, response format, example requests/responses. Show screenshot-style mock of UK Police API docs.
6. **JSON deep-dive** — TikZ nested boxes showing a JSON object: outer box `{}` contains key-value pairs, one value is an array `[]`, one array element is a nested object `{}`. Colour-code keys (green) and values (magenta). Below, show same data as minted JSON.
7. **Next up** — "Practical 2: UK Police API" — brief preview.

**Step 2: Compile and verify**

```bash
cd collecting-digital-data/presentations && latexmk -pdf -shell-escape lecture-2-what-are-apis.tex
```

---

## Task 5: Create Lecture 3 — API Landscape Survey

**Files:**
- Create: `collecting-digital-data/presentations/lecture-3-api-landscape.tex`

**Step 1: Write the lecture file**

Slides:

1. **Section title** — "The API Landscape: What's Out There?"
2. **Categories of APIs** — Visual grouping (TikZ or columns): Government & Public Data, International Organisations, Academic & Bibliometric, Geospatial, AI & LLMs. Use icons from fontawesome5 for each category.
3. **UK Parliament API** — What: bills, debates, MPs, divisions. Auth: none. Format: JSON. Example endpoint. URL to docs. Social science use case: political science, legislative studies.
4. **World Bank Indicators API** — What: development indicators (GDP, poverty, education) for 200+ countries. Auth: none. Format: JSON. Example endpoint. Use case: comparative politics, development studies, economics.
5. **OpenAI / Anthropic API** — What: LLM-as-a-service, text generation, classification, embeddings. Auth: API key (paid). Format: JSON. Use case: text annotation, data classification, synthetic data. Note: "We'll discuss LLMs as coding assistants later today."
6. **ONS API** — What: UK official statistics (labour market, population, economy). Auth: none. Format: JSON/CSV. Use case: sociology, demography, policy studies.
7. **OpenStreetMap / Nominatim API** — What: geospatial data, geocoding, reverse geocoding. Auth: none (rate limited). Format: JSON. Use case: spatial analysis, urban studies, geography.
8. **Finding more APIs** — Link to public-apis GitHub repo. Advice: always check documentation quality, rate limits, and ToS before committing to an API for research.
9. **Next up** — "Practical 3: API Challenge" — preview the three options students can choose from.

**Step 2: Compile and verify**

```bash
cd collecting-digital-data/presentations && latexmk -pdf -shell-escape lecture-3-api-landscape.tex
```

---

## Task 6: Create Lecture 4 — LLMs as Coding Assistants

**Files:**
- Create: `collecting-digital-data/presentations/lecture-4-llms-as-coding-assistants.tex`

**Step 1: Write the lecture file**

Slides:

1. **Section title** — "LLMs as Coding Assistants"
2. **What are LLMs?** — Brief, non-technical. TikZ diagram: Training Data (books, code, web) flows into Model, Model takes Prompt and produces Response. No jargon about transformers — just "statistical model trained on vast amounts of text and code."
3. **Paid vs open models** — Two-column comparison:

   | Paid (ChatGPT, Claude) | Open (Llama, Mistral) |
   |---|---|
   | Hosted by provider | Run locally or self-host |
   | Subscription/API fees | Free to use |
   | Often more capable | Improving rapidly |
   | Data sent to provider | Data stays with you |
   | Easy to use (chat UI) | Requires some setup |

4. **How to prompt for code** — Example of a good prompt vs bad prompt. Good: "Write a Python script using the requests library to download stop-and-search data from the UK Police API (https://data.police.uk/api/stops-force) for the City of London force. Save the results as a JSON file." Bad: "Get me some police data." Show both and the quality of output you'd expect.
5. **What LLMs are good at** — Bullet points with green check icons: boilerplate code, syntax and library usage, explaining error messages, converting between languages (Python to R), generating documentation.
6. **What LLMs are bad at** — Bullet points with red cross icons: up-to-date API endpoints/parameters, complex multi-step logic, understanding your specific research context, guaranteeing correctness, hallucinated function names.
7. **Critical evaluation** — Key message: "You must understand the code yourself." Bullet points: always test LLM-generated code, check API docs match what the LLM suggests, be wary of hallucinated libraries/functions, consider reproducibility (LLM outputs vary), security risks (don't paste API keys into chat).
8. **Next up** — "Practical 4: LLM Showdown" — preview the exercise.
9. **Thank you and resources** — Instructor contact details, Braw Data link, links to course materials (GitHub/README), further reading. SGSSS logo (large).

**Step 2: Compile and verify**

```bash
cd collecting-digital-data/presentations && latexmk -pdf -shell-escape lecture-4-llms-as-coding-assistants.tex
```

---

## Task 7: Create Practical 1 Python notebook — Web Scraping

**Files:**
- Create: `collecting-digital-data/code/practical-1-web-scraping-2026-02-24-Python.ipynb`

**Reference:** `previous-course/code/sgsss-web-scraping-practical-1-2025-03-07-Python.ipynb` and `previous-course/code/sgsss-web-scraping-practical-2-2025-03-07-Python.ipynb`

**Step 1: Write the notebook**

Structure (markdown and code cells):

1. **SGSSS logo** (markdown, image link)
2. **Title:** "Collecting Digital Data for Social Scientists"
3. **Introduction** — brief context paragraph (from design doc)
4. **Aims** — (1) Demonstrate Python for web scraping, (2) Cultivate computational thinking
5. **Lesson details** — Level: Introductory, Time: ~45 min, Pre-requisites: None, Learning outcomes
6. **Guide to using this resource** — Jupyter/Colab boilerplate (retain from previous course: explanation of cells, how to execute, `Shift+Enter`, link to Arribas-Bel materials)
7. **Interactive test cell** — `print("Hello...")` with `input()` (retain from previous)

8. **Section: General approach** — what to know (URL, HTML structure) and what to do (request, parse, extract, save). Retain from previous.

9. **Section: Simple text extraction**
   - Identifying the web address (`httpbin.org/html`)
   - Locating information (HTML source, `<p>` tags) — retain explanation
   - Show raw HTML in a raw cell
   - Requesting: `import requests`, `from bs4 import BeautifulSoup as soup`, request URL, check status code
   - Parsing: `soup(response.text, "html.parser")`
   - Extracting: `soup_response.find("p").text`
   - Saving: write to `./downloads/moby-dick-scraped-data.txt`
   - Verify: read file back
   - Retain explanatory markdown cells between code cells (polished/tightened)

10. **Section: Multi-page scraping**
    - Context: Edinburgh Council warm spaces directory
    - Setup: import modules, define file paths, create data folder
    - Build URL list: base URL + A-Z letters
    - Loop: request each page, parse, extract org names and links using `find("ul", class_="list list--record")`
    - Second loop: visit each org page, extract details from `<dl>` tags
    - Save to JSON
    - Verify: read back and display
    - Explanatory cells between code — tightened from previous

11. **Section: Exercise** — Scrape library locations from Edinburgh Council. Skeleton code with `# INSERT CODE HERE`. Solution in appendix.

12. **Closing note** — "In practice, before scraping a website, check whether the data is available through an API. APIs provide structured, reliable access to data and avoid many of the legal and ethical issues associated with web scraping. We'll explore APIs in the next session."

13. **Appendix: Exercise solution** — full working code

14. **END OF FILE marker**

**Step 2: Verify notebook is valid JSON**

```bash
python -c "import json; json.load(open('collecting-digital-data/code/practical-1-web-scraping-2026-02-24-Python.ipynb'))"
```

Expected: no errors.

---

## Task 8: Create Practical 1 R notebook — Web Scraping

**Files:**
- Create: `collecting-digital-data/code/practical-1-web-scraping-2026-02-24-R.ipynb`

**Reference:** `previous-course/code/sgsss-web-scraping-practical-1-2025-03-07-R.ipynb`

**Step 1: Write the notebook**

Same structure and narrative as the Python version (Task 7) but using R equivalents:
- `httr::GET()` instead of `requests.get()`
- `rvest::read_html()` and `rvest::html_elements()` / `rvest::html_text2()` instead of BeautifulSoup
- `jsonlite::write_json()` / `jsonlite::fromJSON()` for JSON
- `readr::write_lines()` for text files
- R Colab setup cell: `install.packages(c("httr", "rvest", "jsonlite"))` at the top (R is not default in Colab, so include the runtime switch note)
- Kernel metadata must specify R (`"kernelspec": {"name": "ir", ...}`)

**Step 2: Verify notebook is valid JSON**

---

## Task 9: Create Practical 2 Python notebook — UK Police API

**Files:**
- Create: `collecting-digital-data/code/practical-2-uk-police-api-2026-02-24-Python.ipynb`

**Reference:** `previous-course/code/sgsss-api-practical-1-2025-03-07-Python.ipynb`

**Step 1: Write the notebook**

Structure:

1. **Logo, title, introduction, aims, lesson details, guide to resource** (as per Practical 1 pattern, adapted for APIs)

2. **Section: What is an API?** — brief recap (1-2 markdown cells) pointing back to Lecture 2. Definition, translator analogy (short).

3. **Section: First API call (~10 min)**
   - Import modules: `requests`, `json`, `pandas`, `datetime`, `time`, `matplotlib.pyplot`
   - Define base URL, forces endpoint, construct URL
   - `requests.get()`, check `status_code`
   - `.json()` to extract data
   - Display response, inspect headers
   - Retain explanatory cells (polished)

4. **Section: Working with JSON (~15 min)**
   - `type()` to confirm list
   - `len()` to count elements
   - Loop and print elements
   - Index access (`forces_data[0]`, `forces_data[9]`)
   - List comprehension to extract `id` field
   - TASK cells for students to try themselves
   - Retain/polish from previous

5. **Section: Parameterised requests and looping (~20 min)**
   - Stop-and-search for one force (City of London): construct URL with parameters, request, store
   - Inspect data, count records
   - **NEW: Loop over all forces** (promoted from appendix): define blank list, loop over `force_ids`, request each, error handling with `if/else` on status code, add `force` field, `time.sleep(1)` for rate limiting
   - Display count of results
   - Explain the `time.sleep()` addition for rate limiting

6. **Section: From JSON to analysis (~15 min)**
   - `pd.read_json()` to convert to DataFrame
   - `.sample(5)` to inspect
   - `pd.crosstab()` for age vs outcome (retained)
   - `pd.crosstab()` for object of search vs age (retained)
   - **NEW: Simple bar chart** using matplotlib: `df['outcome'].value_counts().plot(kind='barh')` with labelled axes and title

7. **Section: Exercise** — "Produce a list of all senior police officers for each force." Skeleton code. Solution in appendix.

8. **Bibliography** — retain from previous, add any new references

9. **Appendix: Exercise solution** — full working code (retained from previous)

10. **END OF FILE**

**Step 2: Verify valid JSON**

---

## Task 10: Create Practical 2 R notebook — UK Police API

**Files:**
- Create: `collecting-digital-data/code/practical-2-uk-police-api-2026-02-24-R.ipynb`

**Step 1: Write the notebook**

Same structure as Task 9 but R equivalents:
- `httr::GET()`, `httr::content(response, "text")`, `jsonlite::fromJSON()`
- `dplyr` for data manipulation (`bind_rows`, `select`, `filter`)
- `table()` or `dplyr::count()` for cross-tabulations
- `ggplot2` for bar chart (`geom_bar()` with `coord_flip()`)
- `Sys.sleep(1)` for rate limiting
- R kernel metadata

**Step 2: Verify valid JSON**

---

## Task 11: Create Practical 3 Python notebook — API Challenge

**Files:**
- Create: `collecting-digital-data/code/practical-3-api-challenge-2026-02-24-Python.ipynb`

**Step 1: Write the notebook**

Structure:

1. **Logo, title, introduction** — "In this practical you'll choose one of three APIs and collect data independently."
2. **Guide to resource** (Colab boilerplate)
3. **Instructions** — Choose one option, work through the scaffolded code, fill in the gaps, save your data. Solutions in appendix.

4. **Option A: UK Parliament API**
   - Brief intro: what data is available (members, bills, divisions)
   - Documentation link: https://members-api.parliament.uk/ and https://developer.parliament.uk/
   - **Scaffolded code:**
     - Import modules (provided)
     - Define base URL and endpoint for current MPs (provided): `https://members-api.parliament.uk/api/Members/Search?IsCurrentMember=true&skip=0&take=20`
     - Make request and inspect response (provided)
     - Extract list of MPs and display (provided)
     - TASK 1: Modify the request to get all MPs (hint: pagination with `skip` and `take` parameters) — `# INSERT CODE HERE`
     - TASK 2: Extract name, party, and constituency for each MP into a list of dictionaries — `# INSERT CODE HERE`
     - TASK 3: Convert to DataFrame and save as CSV — `# INSERT CODE HERE`
     - TASK 4 (stretch): Get voting records for a specific bill — `# INSERT CODE HERE`

5. **Option B: World Bank Indicators API**
   - Brief intro: development indicators for 200+ countries
   - Documentation link: https://datahelpdesk.worldbank.org/knowledgebase/topics/125589
   - **Scaffolded code:**
     - Import modules (provided)
     - Define endpoint for GDP data for one country (provided): `https://api.worldbank.org/v2/country/GB/indicator/NY.GDP.MKTP.CD?format=json`
     - Make request and inspect response (provided)
     - Navigate the nested JSON response (provided — World Bank returns `[metadata, data]` list)
     - TASK 1: Request GDP data for all G7 countries (hint: `country/USA;GBR;FRA;DEU;JPN;ITA;CAN`) — `# INSERT CODE HERE`
     - TASK 2: Extract country, year, and GDP value into a list — `# INSERT CODE HERE`
     - TASK 3: Convert to DataFrame, save as CSV — `# INSERT CODE HERE`
     - TASK 4 (stretch): Request a different indicator (e.g., life expectancy) and plot a time series — `# INSERT CODE HERE`

6. **Option C: ONS API**
   - Brief intro: UK official statistics
   - Documentation link: https://developer.ons.gov.uk/
   - **Scaffolded code:**
     - Import modules (provided)
     - Define endpoint for a dataset listing (provided): `https://api.beta.ons.gov.uk/v1/datasets`
     - Make request and inspect response (provided)
     - TASK 1: List all available datasets and their descriptions — `# INSERT CODE HERE`
     - TASK 2: Choose a dataset and request its latest version — `# INSERT CODE HERE`
     - TASK 3: Extract and save the data — `# INSERT CODE HERE`

7. **Appendix: Solutions** — full working code for each option

8. **END OF FILE**

**Step 2: Verify valid JSON**

**Note:** Before writing this notebook, verify that the Parliament API, World Bank API, and ONS API endpoints are still live and returning expected data. Make test requests and confirm response structures.

---

## Task 12: Create Practical 3 R notebook — API Challenge

**Files:**
- Create: `collecting-digital-data/code/practical-3-api-challenge-2026-02-24-R.ipynb`

**Step 1: Write the notebook**

Same structure as Task 11 but R equivalents:
- `httr::GET()`, `jsonlite::fromJSON()`
- `dplyr::bind_rows()`, `dplyr::select()`, `dplyr::mutate()`
- `readr::write_csv()` for saving
- `ggplot2` for stretch plotting tasks
- R kernel metadata

**Step 2: Verify valid JSON**

---

## Task 13: Create Practical 4 Python notebook — LLM Showdown

**Files:**
- Create: `collecting-digital-data/code/practical-4-llm-showdown-2026-02-24-Python.ipynb`

**Step 1: Write the notebook**

This notebook is a structured worksheet, not a standard coding practical.

Structure:

1. **Logo, title, introduction** — "In this session we evaluate how well LLMs can generate the code we wrote today."
2. **Guide to resource** (Colab boilerplate)

3. **Section: The exercise**
   - Explanation: we define coding prompts based on today's practicals, submit them to different LLMs, and evaluate the outputs
   - Evaluation criteria:
     1. Does the code run without errors?
     2. Does it produce the correct output?
     3. Does it use appropriate libraries?
     4. Is the code well-structured and readable?
     5. Are there any security or ethical issues?

4. **Section: Prompt 1 — Web scraping**
   - Markdown cell with the prompt: "Write a Python script that scrapes all organisation names and URLs from the Edinburgh Council warm and welcoming spaces directory (https://www.edinburgh.gov.uk/directory/10258/other-warm-and-welcoming-locations). The script should loop through the A-Z pages, extract each organisation's name and link, and save the results as a JSON file."
   - Empty code cell: `# Paste ChatGPT output here`
   - Empty code cell: `# Paste Claude output here`
   - Empty code cell: `# Paste open model output here`
   - Markdown cell: Evaluation table (to be filled in):

     | Criterion | ChatGPT | Claude | Open Model |
     |---|---|---|---|
     | Runs without errors? | | | |
     | Correct output? | | | |
     | Appropriate libraries? | | | |
     | Well-structured? | | | |
     | Security/ethical issues? | | | |

5. **Section: Prompt 2 — API**
   - Same structure for: "Write a Python script that downloads stop-and-search data for all police forces using the UK Police API (https://data.police.uk/api/). The script should get a list of forces, loop through each one to request stop-and-search data, handle errors, respect rate limits, and save all results as a single JSON file."

6. **Section: Prompt 3 — Analysis**
   - Same structure for: "Write a Python script that requests GDP data for all G7 countries from the World Bank API, converts the results to a pandas DataFrame, and creates a bar chart comparing the most recent GDP figures."

7. **Section: Discussion questions**
   - Markdown cells with prompts for reflection:
     1. Which LLM produced the best code overall? What made it better?
     2. Did any LLM produce code that looked correct but was actually wrong? How would you know?
     3. What information did you need to include in your prompt to get good results?
     4. How would you use LLMs in your own research workflow? Where would you trust them and where would you not?
     5. What are the implications for reproducibility if researchers use LLM-generated code?

8. **Section: Our solutions** — links back to Practicals 1-3 notebooks as the "ground truth"

9. **END OF FILE**

**Step 2: Verify valid JSON**

---

## Task 14: Create Practical 4 R notebook — LLM Showdown

**Files:**
- Create: `collecting-digital-data/code/practical-4-llm-showdown-2026-02-24-R.ipynb`

**Step 1: Write the notebook**

Same structure as Task 13 but prompts ask for R code instead of Python. E.g.:
- "Write an R script using the httr and rvest packages that scrapes..."
- "Write an R script using httr and jsonlite that downloads stop-and-search data..."
- "Write an R script using httr, jsonlite, and ggplot2 that requests GDP data..."

Evaluation tables and discussion questions identical.

**Step 2: Verify valid JSON**

---

## Task 15: Create README.md

**Files:**
- Create: `collecting-digital-data/README.md` (overwrite existing outline file at project root level — the outline is now superseded by the full materials)

**Step 1: Write the README**

Structure:

```markdown
# Collecting Digital Data: The Role of Web-scraping and APIs

## Event Summary

[Retain from course outline]

## Course Schedule

[Table of day's schedule]

## Interactive Coding Materials

The practicals contain Python and R code for you to execute.

You can complete the lessons online without installing anything.
You need a Google account to run the code notebooks.

### Python

* Practical 1: Web Scraping [Colab badge link]
* Practical 2: UK Police API [Colab badge link]
* Practical 3: API Challenge [Colab badge link]
* Practical 4: LLM Showdown [Colab badge link]

### R

* Practical 1: Web Scraping [Colab badge link]
* Practical 2: UK Police API [Colab badge link]
* Practical 3: API Challenge [Colab badge link]
* Practical 4: LLM Showdown [Colab badge link]

## Presentations

* Lecture 1: Welcome & How the Web Works [PDF link]
* Lecture 2: What Are APIs? [PDF link]
* Lecture 3: API Landscape Survey [PDF link]
* Lecture 4: LLMs as Coding Assistants [PDF link]

## Instructor

Dr Diarmuid McDonnell
Director, Braw Data Ltd
Visiting Fellow, Gradel Institute of Charity, University of Oxford

## Licence

[As appropriate]
```

**Note:** Colab badge URLs will need to be updated once notebooks are pushed to a GitHub repository. Use placeholder format: `https://colab.research.google.com/github/OWNER/REPO/blob/main/code/FILENAME.ipynb`

**Step 2: Verify markdown renders correctly**

---

## Task 16: Compile all Beamer decks and final verification

**Step 1: Compile all 4 lectures**

```bash
cd collecting-digital-data/presentations
latexmk -pdf -shell-escape lecture-1-welcome-and-how-the-web-works.tex
latexmk -pdf -shell-escape lecture-2-what-are-apis.tex
latexmk -pdf -shell-escape lecture-3-api-landscape.tex
latexmk -pdf -shell-escape lecture-4-llms-as-coding-assistants.tex
```

**Step 2: Verify each PDF**
- Correct number of slides
- SGSSS branding (magenta headers, green accents)
- TikZ diagrams render
- Code blocks syntax-highlighted
- Footer with logo and page numbers
- No overflow/layout issues

**Step 3: Validate all notebooks**

```bash
cd collecting-digital-data/code
for f in *.ipynb; do python -c "import json; json.load(open('$f')); print('OK: $f')"; done
```

**Step 4: Test API endpoints**

```bash
curl -s -o /dev/null -w "%{http_code}" https://data.police.uk/api/forces
curl -s -o /dev/null -w "%{http_code}" https://httpbin.org/html
curl -s -o /dev/null -w "%{http_code}" "https://members-api.parliament.uk/api/Members/Search?IsCurrentMember=true&skip=0&take=5"
curl -s -o /dev/null -w "%{http_code}" "https://api.worldbank.org/v2/country/GB/indicator/NY.GDP.MKTP.CD?format=json"
```

Expected: all return `200`.

**Step 5: Final file listing**

```bash
find collecting-digital-data/ -type f | sort
```

Expected: 16 content files (4 `.tex`, 4 `.pdf`, 8 `.ipynb`) plus preamble, logo, README, design doc, plan doc.

---

## Execution Order and Dependencies

```
Task 1 (dirs/assets)
  └─> Task 2 (preamble)
        ├─> Task 3 (Lecture 1)  ─┐
        ├─> Task 4 (Lecture 2)  ─┤
        ├─> Task 5 (Lecture 3)  ─┤  All independent of each other
        └─> Task 6 (Lecture 4)  ─┘
  └─> Task 7 (Practical 1 Py)  ─> Task 8 (Practical 1 R)
  └─> Task 9 (Practical 2 Py)  ─> Task 10 (Practical 2 R)
  └─> Task 11 (Practical 3 Py) ─> Task 12 (Practical 3 R)
  └─> Task 13 (Practical 4 Py) ─> Task 14 (Practical 4 R)
  └─> Task 15 (README) — after all notebooks exist
  └─> Task 16 (Final verification) — after everything
```

Tasks 3-6 can run in parallel. Tasks 7-14 can run in parallel (Python before R within each pair). Task 15 depends on all notebooks. Task 16 is the final gate.
