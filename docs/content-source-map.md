# Content Source Map — where the real content for this scaffold already lives

Written 2026-09-26, per direct instruction, after reading every page in both portfolio
directories and surveying the real project folders across this workspace. This is the analysis
requested: what these two directories are, how they relate to each other and to the *existing*
portfolio site, and — page by page — which real project folder actually contains the material
each placeholder is asking for.

## 1. The two directories, and how they relate

`github-pages-portfolio/` and `github-pages-portfolio2/` are **the same content, two iterations
of presentation**, not two different portfolios:

- Every content page (`about/`, `research/*.md`, `systems/*.md`, `education/`, `services/`,
  `books/`, `data-engineering/`, `architecture/`, `recruiting/`, `job-seeking/`, `intelligence/`,
  `work/`, `case-studies/`, `templates/*.md`) is **byte-identical** between the two directories —
  confirmed directly with `diff -rq`, not assumed.
- **v1** (`github-pages-portfolio/`) is the first pass: Jekyll's default `minima` theme, a plain
  Markdown homepage, and three now-unused scaffold folders (`_data/`, `_includes/`, `_posts/` —
  all empty).
- **v2** (`github-pages-portfolio2/`) is a real design iteration on top of the *same* content: a
  custom `_layouts/{default,home,page,system}.html`, real `assets/css/site.css` +
  `assets/js/site.js`, a fully custom homepage (hero, capability stack, system grid, architecture
  diagram, research grid, book band, CTA — not Markdown prose), a new `docs/interface-model.md`
  defining the real visual/content grammar ("Large editorial typography · thin rules · dense
  system diagrams · neutral paper/black palette · one controlled accent · no generic SaaS
  gradients"), and a `systems/index.md` nav page v1 doesn't have.
- **v2 supersedes v1 for anything user-facing.** v1 is worth keeping only as the simpler
  reference/fallback theme, or archived once v2 is confirmed working. Any content fix should be
  made in both (or a build step should generate one from the other) to avoid drift — right now
  they'd have to be edited twice by hand.

`docs/interface-model.md`'s own **"Evidence rule"** governs everything below: *"Do not claim a
result until evidence exists. Use explicit status labels: Research / Prototype / Active /
Deployed."* Every system page already carries a real status line (e.g., "Prototype / research
system"); filling these pages means adding real evidence under that same label, not upgrading the
label without the evidence.

## 2. The relationship to the *existing* portfolio site

There is a third, already-built and content-populated surface this scaffold doesn't reference
directly: **`frontend/caphe_portfolio_site/`** — a real, deployed React/Vite site with its own
`About.jsx`, `Research.jsx`, `Consulting.jsx`, `Home.jsx`, `Contact.jsx`, real design tokens, and a
`site/taxonomy.yaml`/`conversion.yaml` content model (the one this whole engagement has been
directly editing all session — the "Diagnose" language rename, the contact-email fixes, etc.).

Concretely: `frontend/caphe_portfolio_site/src/pages/About.jsx` already contains full, polished,
real prose for almost every checkbox on this scaffold's `about/index.md` — "Who I Am," "What I
Study," "How I Think," "How I Build," "Professional Experience" (the real Maxim
Healthcare/Harbor-UCLA/Long Beach VA arc, the DBS Bank/Singapore engagement), "Education," and
"Teaching." This is not a case of writing new copy — it's a case of **porting real, already-written
copy** from one real surface to another. The two sites are not currently kept in sync; treat
`caphe_portfolio_site` as upstream truth for identity/positioning prose and this Jekyll scaffold as
a second, GitHub-Pages-native surface, unless the intent is for one to eventually replace the
other — that's a real open decision, not something to guess at silently.

## 3. Page-by-page: what's real and where it already lives

| Scaffold page | What it's asking for | Real source(s) that already exist |
|---|---|---|
| `about/index.md` | Resume, portfolio, diagrams, demos, research, teaching, client outcomes, certifications, talks | `frontend/caphe_portfolio_site/src/pages/About.jsx` (portable prose, see §2) · `resume/engine/profile/*.yaml` (the real evidence source of truth — experience, education, achievements, technologies) · `resume/engine/data/resumes/` + `resume/data-engineer/resumes/` (generated resumes/PDFs) · `claremont/` (real CGU CISAT D.Tech/PhD program PDFs — the actual certification evidence) |
| `systems/recruiting-intelligence-platform.md` | Architecture diagram, data model, ATS adapter, Gmail/Calendar integration, Job/Candidate Intelligence Brief, metrics, case study | `canvas/03_INDUSTRY/RECRUITING/ENTERPRISE_ARCHITECTURE/recruiting-information-architecture.yaml` (+ the live React Flow viewer, localhost:3003) for the diagram · `consulting/recruiting/w2/systems/job_search_engine/` for the real schema/ATS adapter · `integrations/gmail_client.py`, `cal_com_client.py`/`calendly_client.py` (live-verified) · `job_search_engine/run_job_intelligence_brief.py` and `intelligence/caphe_recruiting_intelligence_reporting/` (Candidate Intelligence Brief) · `docs/dissonance-report.md` addenda for real metrics/case-study material |
| `systems/job-seeking-intelligence-system.md` | Signal registry, opportunity schema, matching model, application tracker, outreach workflow, demo | `resume/engine/` (job_matcher.py, resume_generator.py, `data/normalized/jobs/`) · `resume/data-engineer/` (the live, run example of this exact system — 10 real postings → matched → generated resumes) · `job_search_engine/config/feed_registry.yaml` (signal registry) |
| `systems/threat-intelligence-system.md` | Signal schema, source registry, entity graph, pattern model, investigation brief, case workflow | `resume/engine/profile/technologies.yaml`'s "Wolf OS" entry — real but currently undocumented beyond a one-line mention; **this is the least-evidenced system** and the most honest thing to do is mark it clearly "Research" until real artifacts exist, not backfill placeholder evidence |
| `systems/caphe-learning-management-system.md` | Course catalog, lesson/exercise schema, assessment model, LMS architecture, learning analytics, sample module | `lms/` (the real, live Moodle install — index.php, caphe_loader.py) · `drvalentine/courses/` (real course folders: `cap-hr-303`, `cap-rec-202`, `caphe-algebra2`, `cap-car-102`, `cap-python-for-business`, `caphe-fin-001` — several with a real `course.json`/`syllabus.md`/`ebook-framework.md`, and `caphe-algebra2` is a fully runnable app with `engine.py`/`main.py`/`preview.html`) · `curriculum/catalog.py` (real CGU/CISAT program data, sourced from `claremont/`'s real PDFs) · `syllabus/`, `training/` (repo root) |
| `systems/operational-data-workflow-system.md` | The reusable cross-domain architecture | `consulting/recruiting/_shared/scoring_kernel.py` (the real, equivalence-tested shared band-resolution rule already reused across 3 systems) — this page can cite that directly as real, existing evidence, not a future build |
| `research/human-in-the-loop-systems.md` | Literature review, case studies, failure examples, human decision boundaries | `resume/engine/profile/research.yaml` (the real D.Tech research program) · every canvas graph's `escalates_to`/`human_authority` nodes (recruiting, job-intelligence, healthcare graphs) are real, working examples of an enforced human-decision boundary, not theory |
| `research/recruiting-architecture.md` | Job/Candidate/Recruiter Intelligence models, ATS event model, workflow maps, metrics | `canvas/03_INDUSTRY/RECRUITING/` graphs (both levels) · `intelligence/caphe_recruiting_intelligence_reporting/docs/` (the real dissonance reports, integration plans, master-report-alignment analysis) |
| `research/job-seeking-intelligence.md` | Already fairly complete prose; needs real evidence, not more thesis | `resume/data-engineer/` is the real, running instance of exactly this thesis — cite it directly |
| `data-engineering/index.md` | Pipeline, schema, API, warehouse, data-quality system, entity-resolution example, case study | `resume/healthcare/healthcare-data-systems-portfolio/` (the real Postgres schema, FastAPI, analytics layer, data-quality report — this is the single strongest, most complete real match in the entire workspace for this page) · `job_search_engine/` (the bronze/gold pipeline) |
| `architecture/index.md` | Current/future-state architecture, data model, workflow model, integration map, operating model | `canvas/` in its entirety — this is literally what the canvas engine is for; link to it rather than re-deriving diagrams by hand |
| `recruiting/index.md`, `job-seeking/index.md`, `intelligence/index.md` | Service modules, product concepts, intelligence types | Mostly already real via the pages above; `intelligence/index.md`'s "Property Intelligence" section has **no matching real project anywhere in this workspace** — the one placeholder here that's genuinely aspirational, not just unwritten |
| `education/index.md`, `services/index.md` | Curriculum, audiences; service families and entry path | `lms/`, `drvalentine/courses/`, `curriculum/` · `frontend/caphe_portfolio_site/src/pages/Consulting.jsx` and `site/taxonomy.yaml`/`conversion.yaml` (the real, already-written service-tier positioning, including the "Diagnose" language already in production) |
| `books/index.md` | Thesis, TOC, chapter summaries, manuscript | `books/27seconds-manifesto.md`, `books/27seconds-framework.md`, `books/book-framework.md` (real, existing drafts) · `books/caphe-books-os/` (a real, separate publishing-engine app — mkdocs-based) |
| `work/index.md`, `case-studies/index.md` | Real project write-ups using `templates/case-study.md` | Every real system built this session is a real candidate: the healthcare data portfolio, the recruiting-intelligence reporting engine's Addenda, the Data Engineer resume-generation run, the pose simulator MVP — each already has a real, dated build record (dissonance reports, implementation plans) that a case study would summarize, not invent |

## 4. What's genuinely not backed by anything real yet

Named honestly, per the scaffold's own evidence rule:

- **Threat Intelligence System** — one real mention in `technologies.yaml`, no schema/code/demo
  anywhere. Keep its status label conservative until that changes.
- **Property Intelligence** — appears in `intelligence/index.md` and `research/index.md`'s theme
  list with no corresponding real project folder anywhere in this workspace.
- **Demo videos** (named on multiple system pages) — none exist for any system.
- **Talks/interviews, client outcomes** (`about/index.md`) — no real project folder found for
  either.

## 5. Recommended fill order

Highest real-evidence-to-effort ratio first:

1. **`data-engineering/index.md`** — the healthcare data portfolio alone answers 6 of its 8
   "Evidence to add" boxes today.
2. **`about/index.md`** — port `caphe_portfolio_site/About.jsx`'s existing prose directly; this is
   editing, not writing.
3. **`systems/recruiting-intelligence-platform.md`** — the most evidence of any system page; link
   the real canvas diagram and the real Job Intelligence Brief output.
4. **`systems/caphe-learning-management-system.md`** — the real `courses/` catalog fills the
   "Course catalog" checkbox immediately; `caphe-algebra2` is a real, runnable "sample module."
5. **`work/` + `case-studies/`** — populate from this session's own real dissonance-report addenda
   and implementation-plan docs, using `templates/case-study.md`.
6. Everything else in §3, in the order the real source material is most complete.

Leave **Threat Intelligence** and **Property Intelligence** genuinely marked "Research" until real
work exists — per the scaffold's own rule, not this document's opinion.
