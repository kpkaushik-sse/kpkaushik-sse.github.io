# LearnHub - Autonomous AI Engineering

LearnHub is a GitHub Pages powered learning platform focused on practical, project-driven AI education.
It includes structured tracks for Agentic AI, web fundamentals, Git, and API concepts, with a flagship 12-week Autonomous AI Systems course.

Live site:
https://kpkaushik-sse.github.io

## What this repository contains

- A modern Jekyll site with custom layouts and LMS-style lesson pages
- Long-form tutorial posts under posts
- A course collection under courses
- A complete multi-unit Agentic AI track from foundations to cloud deployment

## Main learning track

Autonomous AI Systems - Practical Engineering Track

Progression:

1. U1: Agentic AI Essentials
2. U2: Agentic AI Architecture and Design Patterns
3. U3: Chain Composition with LangChain
4. U4: Stateful Agent Workflows with LangGraph
5. U5: Retrieval-Augmented Agent Pipelines
6. U6: Rapid Agent Prototyping with Phidata
7. U7: Coordinated Agent Teams with CrewAI
8. U8: Conversational Agent Networks with Autogen
9. U9: Tracing, Evaluation, and Agent Telemetry
10. U10: Visual and Low-Code Agent Builders
11. U11: Capstone - Deploying Autonomous AI on Major Clouds

## Tech stack

- Jekyll (GitHub Pages)
- pages-themes/architect remote theme with custom overrides
- Plugins: jekyll-remote-theme, jekyll-feed, jekyll-seo-tag
- Markdown: kramdown
- Highlighting: rouge

## Project structure

- \_config.yml: Site config, theme, plugins, collections
- \_layouts: Shared page and post layouts
- \_posts: Blog lessons and module content
- \_courses: Course collection pages
- assets/images: Brand and media assets
- \_site: Generated site output (build artifact)

## Run locally

Option A - Docker (recommended)

    docker compose up

Site URL:
http://localhost:4000

Option B - Ruby/Jekyll

1. Install Ruby and Bundler
2. Install dependencies:

   bundle install

3. Serve the site:

   bundle exec jekyll serve

4. Open:

   http://localhost:4000

## Writing workflow

### Add a new tutorial post

1. Create a file in \_posts using this pattern:
   YYYY-MM-DD-topic-title.md
2. Add front matter (layout, title, categories, description)
3. Write content using the existing LMS-style structure used by the Agentic AI units
4. Verify it appears in the Blog and relevant course pages

### Add or update a course unit

1. Create or edit the unit post in \_posts
2. Add or update its entry in courses/agentic-ai-engineering
3. Verify links from Home, Courses, and module pages

## Publishing

This repository is configured for GitHub Pages deployment from the main branch.

Typical publish flow:

1. Commit changes
2. Push to main
3. Wait for Pages build to finish
4. Verify production site

## Content and quality guidelines

- Keep lessons practical and implementation-oriented
- Prefer original wording and examples
- Keep module progression consistent (concepts, patterns, architecture, hands-on)
- Include hands-on tasks and review checkpoints in each module

## Contact

Author: Khush Kaushik
Email: kpkaushik@virtualemployee.com

## License

Site content and code are maintained in this repository by the project owner.
