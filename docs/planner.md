# VistaraX — Placement Build Planner
 
> **AI-Powered Interactive 3D Visualization Platform**
> A student asks a question. A fine-tuned transformer routes it, RAG grounds it, and an LLM explains it while controlling an interactive 3D scene.
 
| | |
|---|---|
| **Goal** | A deployed, working v1 prototype I can demo and defend in placement interviews |
| **Duration** | 1 setup week + 12 build weeks (29 Sep – 27 Dec 2026) |
| **Effort** | ~15 hours/week |
| **Scope** | 5 3D concepts · LLM tool calling · RAG · fine-tuned DistilBERT router · evaluation · deployment |
| **Companion doc** | `README.md` — product description, API, setup |
 
## Contents
 
1. [How to use this planner](#1-how-to-use-this-planner)
2. [Ground rules](#2-ground-rules)
3. [Weekly routine](#3-weekly-routine)
4. [Milestones at a glance](#4-milestones-at-a-glance)
5. [Week 0 — Setup](#5-week-0--setup)
6. [Month 1 — 3D foundations + first AI](#6-month-1--3d-foundations--first-ai)
7. [Month 2 — RAG + transformers](#7-month-2--rag--transformers)
8. [Month 3 — Heart, evaluation, delivery](#8-month-3--heart-evaluation-delivery)
9. [Build reference](#9-build-reference)
10. [Risks & fallbacks](#10-risks--fallbacks)
11. [Placement kit](#11-placement-kit)
12. [Progress tracker](#12-progress-tracker)
13. [Weekly log template](#13-weekly-log-template)
14. [Resources](#14-resources)
---
 
## 1. How to use this planner
 
- **Every Monday:** read the week's section and turn its tasks into GitHub Issues.
- **Every day:** commit, and write 2 lines in the weekly log.
- **Every Sunday:** fill in the weekly log, update the progress tracker, and do the week's **Explain it** check out loud.
- A week is **done** only when its **Definition of Done** is met — not when the tasks are "mostly" done.
## 2. Ground rules
 
1. **I write the code.** AI tools are my tutor, not my typist: I use them to explain, review and debug, and I understand and re-type anything I take from them.
2. **Explain it or it isn't done.** Every week ends with explaining that week's concepts out loud, without notes.
3. **Working beats perfect.** Ship a plain version first; polish later.
4. **Protect the AI core.** If I fall behind, I cut scene polish — never the router, RAG, validation or evaluation.
5. **Measure, don't claim.** Only real, measured numbers go in the README and on my resume.
6. **Commit daily.** Small commits, clear messages. The GitHub history is part of my proof.
## 3. Weekly routine
 
| Day | Time | What |
|---|---|---|
| Mon – Fri | 1.5–2 h | 30 min learning → 1–1.5 h building → commit + 2-line log |
| Saturday | 4 h | Main build block — the hardest task of the week |
| Sunday | 3 h | Learning track (tiny GPT from Week 5), review, weekly log, plan next week |
 
## 4. Milestones at a glance
 
| Week | Dates | Focus | Milestone |
|---|---|---|---|
| 0 | 29 Sep – 4 Oct | Setup | Tools, accounts and repo ready |
| 1 | 5 – 11 Oct | 3D basics + solar system | |
| 2 | 12 – 18 Oct | Satellites + SVM scene | |
| 3 | 19 – 25 Oct | Backend + LLM tool calling | |
| 4 | 26 Oct – 1 Nov | Double-slit scene | **v0.1** — AI tutor controls 3 scenes |
| 5 | 2 – 8 Nov | RAG | |
| 6 | 9 – 15 Nov | Router dataset | |
| 7 | 16 – 22 Nov | Fine-tune the router | |
| 8 | 23 – 29 Nov | Orbitals & bonding | **v0.2** — full AI pipeline on 4 scenes |
| 9 | 30 Nov – 6 Dec | Heart & blood flow | |
| 10 | 7 – 13 Dec | Evaluation | |
| 11 | 14 – 20 Dec | Deploy + optimise | |
| 12 | 21 – 27 Dec | Presentation + interview prep | **v1.0** — live, documented, defensible |
 
Dates are suggestions. If I start later, shift the whole table.
 
---
 
## 5. Week 0 — Setup
 
**29 Sep – 4 Oct · Goal:** everything installed and the repo skeleton pushed, so Week 1 is pure building.
 
**Build**
- [ ] Install Node.js 18+, Python 3.11+, Git, VS Code (ESLint, Prettier, Python, Pylance)
- [ ] Accounts: GitHub, Google Colab, Hugging Face, Vercel, LLM provider — set a monthly spending limit on the LLM account
- [ ] Create the `vistarax` repo with the README, MIT license and `.gitignore` (Node, Python, `.env`)
- [ ] Skeleton: `frontend/` (Vite + React), `backend/` (FastAPI with `/health`), `ml/`, `tiny-gpt/`, `docs/`
- [ ] GitHub Project board (To do / In progress / Done) with Week 1 issues
- [ ] Create `docs/learning-log.md` from the template in section 13
**Learn (if rusty)**
- React: components, props, state, `useEffect`
- FastAPI: routes, Pydantic models
**Definition of Done:** `npm run dev` shows a React page, `/health` returns `{"status": "ok"}`, and both are committed.
 
---
 
## 6. Month 1 — 3D Foundations + First AI
 
### Week 1 — 3D basics + solar system
 
**5 – 11 Oct · Goal:** a navigable solar system in the browser.
 
**Learn**
- React Three Fiber: `Canvas`, scene graph, meshes, materials, lights, `useFrame`
- drei helpers: `OrbitControls`, `Html` / `Text` labels, `useTexture`, `Stars`
**Build**
- [ ] Scene shell: canvas, lights, starfield, camera controls
- [ ] Sun + 4 planets (Mercury – Mars) with textures, circular orbits (`angle += ω·dt`) and self-rotation
- [ ] `focus(object)` — smooth camera fly-to (interpolate camera position and target)
- [ ] `set_time_speed(x)` and `label(object, text)`
- [ ] Temporary debug buttons that call these functions
- [ ] Scene switcher layout with placeholders for the other 4 scenes
**Technical notes**
- Real distances and sizes can't be to scale and still be visible. Use scaled values and say so in the UI.
- Keep scene functions in one place (a Zustand store). Later the AI calls them exactly the way the buttons do.
**Definition of Done:** planets orbit smoothly; buttons focus any planet and change time speed.
 
**Explain it:** the scene graph · camera vs controls · what `useFrame` does every frame · why scene functions are separate from the UI
 
### Week 2 — Satellites + SVM scene
 
**12 – 18 Oct · Goal:** two concept scenes with real physics and real ML behind them.
 
**Build — satellites**
- [ ] Earth close-up with a geostationary and a polar satellite; `show_orbit(type)`
- [ ] Physics: gravity `a = −GM·r / |r|³`, integrated each frame with semi-implicit Euler (`v += a·dt; x += v·dt`), using scaled units
- [ ] `set_satellite_speed(v)`, compared with `v_circular = √(GM/r)` and `v_escape = √2 · v_circular`: too slow → falls, near `v_circular` → orbits, above `v_escape` → escapes
- [ ] `show_vectors(on)` — velocity and gravity arrows
**Build — SVM**
- [ ] Two classes of 2D points; fit with scikit-learn `SVC` through a backend endpoint `POST /svm/fit` that returns the support vectors and the decision function on a grid
- [ ] Draw the boundary (decision function = 0) and margins (= ±1); `highlight_support_vectors()`, `show_margin(on)`
- [ ] Drag points → debounced refit → live update
- [ ] `apply_kernel("linear" | "rbf")`, `set_param("C", value)`
- [ ] Kernel trick: circular dataset → `lift_to_3d()` maps `z = x² + y²`, shows the separating plane, then animates back down to the curved boundary
- [ ] Add `/svm/fit` to the README's API reference
**Definition of Done:** the satellite visibly falls, orbits or escapes depending on speed; the SVM boundary updates live when points move; the kernel lift animation works.
 
**Explain it:** why satellites don't fall · derive `v_circular` · the SVM objective (maximise the margin) · what support vectors are · what `C` controls · what a kernel does and why the lift works
 
### Week 3 — Backend + LLM tool calling
 
**19 – 25 Oct · Goal:** typed questions control the solar system and SVM scenes.
 
**Learn**
- Tool/function calling in the LLM provider's docs
- JSON Schema basics; Pydantic models and validation
**Build**
- [ ] `backend/app/tools.py` — per-scene action registry; each action is a Pydantic model with typed, bounded arguments (pattern in section 9)
- [ ] Generate the LLM's tool definitions from those Pydantic models — one source of truth
- [ ] `POST /ask` — input: `question`, `scene`, `scene_state`, `session_id`; output as in the README
- [ ] System prompt (section 9): tutor persona, 3–6 sentence answers, always use tools to show, say so when out of scope
- [ ] Validator: drop unknown functions, reject out-of-range arguments, log everything dropped
- [ ] Frontend: chat panel + action runner that executes actions in sequence with short pauses
- [ ] Keep the last 4 turns as conversation history
- [ ] `backend/tests/test_validator.py` — unknown function dropped, bad arguments rejected, valid actions kept
**Definition of Done:** "show me Mars", "make the satellite escape" and "highlight the support vectors" work end to end; validator tests pass.
 
**Explain it:** what actually happens in a tool call (the model outputs a structured request; my code executes it) · why the LLM only sees the active scene's tools · why validation is needed · how scene state reaches the LLM
 
### Week 4 — Double-slit + checkpoint v0.1
 
**26 Oct – 1 Nov · Goal:** the third scene, and a first demo.
 
**Build**
- [ ] Particle source, barrier with two slits, screen
- [ ] Screen intensity: `I(y) ∝ cos²(π·d·y / λL) · sinc²(π·a·y / λL)`, with `sinc(x) = sin(x)/x` (d = slit gap, a = slit width, L = distance to screen)
- [ ] `fire_particles(n)` — sample hit positions from `I(y)` by rejection sampling; draw hits with `InstancedMesh` so thousands of dots stay fast
- [ ] `set_slit_gap(d)`, `set_wavelength(λ)`, one/two-slit toggle, `reset_screen()`
- [ ] `toggle_detector(on)` — drop the interference (cos²) term, leaving only the single-slit envelope: the fringes vanish
- [ ] Register the scene's actions; tool calling works here too
- [ ] Tag **v0.1.0**, record a 60–90 s demo video, add the GIF to the README
**Definition of Done:** the interference pattern builds dot by dot and its fringes vanish with the detector on; the AI tutor controls all 3 scenes.
 
**Explain it:** the intensity formula and what d, a, λ and L each do · rejection sampling · why which-path detection removes the interference term · `InstancedMesh` and draw calls
 
---
 
## 7. Month 2 — RAG + Transformers
 
### Week 5 — RAG
 
**2 – 8 Nov · Goal:** answers grounded in trusted content, with sources.
 
**Learn:** embeddings · cosine similarity · chunking trade-offs · vector databases
 
**Build**
- [ ] Content in Markdown with headings: NCERT excerpts (gravitation; the heart; structure of the atom and chemical bonding) plus my own notes on SVMs and quantum physics
- [ ] `backend/app/ingest.py` — chunk by headings (300–500 tokens, ~50 overlap), metadata `{concept, subtopic, source}`, embed with `all-MiniLM-L6-v2`, store in Chroma
- [ ] Retrieval: filter by concept, top-k = 4; if the best similarity is below a threshold, tell the LLM the topic isn't covered
- [ ] Add retrieved chunks to the prompt; the LLM answers only from them and returns source IDs
- [ ] Show sources under each answer in the chat panel
- [ ] Retrieval check: 30 questions, each labelled with the chunk that answers it → measure recall@4
- [ ] **Sunday — tiny GPT part 1:** data loading, character tokenizer, bigram model
**Definition of Done:** answers show sources; recall@4 is measured and recorded in the log.
 
**Explain it:** what an embedding is · cosine similarity · why chunk size matters · RAG vs fine-tuning for adding knowledge · recall@k
 
### Week 6 — Router dataset
 
**9 – 15 Nov · Goal:** a realistic labelled dataset and a baseline to beat.
 
**Build**
- [ ] Final label set — 16 labels: 3 sub-topics × 5 concepts + `out_of_scope` (section 9)
- [ ] Write 30–40 questions per label (≈ 500–600 total): formal, casual, very short, misspelled, slightly wrong, and some Hinglish (e.g. *"satellite neeche kyun nahi girta?"*)
- [ ] Write questions in paraphrase groups and keep each group inside one split to avoid leakage; split 70 / 15 / 15
- [ ] **External test set:** ask 2–3 friends to write ~60 questions without seeing mine
- [ ] Baseline: TF-IDF + logistic regression; record accuracy and macro-F1
- [ ] **Sunday — tiny GPT part 2:** self-attention, single head → multi-head
**Definition of Done:** dataset committed as CSV in `ml/router_dataset/` with a short data card (how it was written, label counts, split method); baseline numbers recorded.
 
**Explain it:** why the label design matters · data leakage and group splits · why a baseline comes first · accuracy vs macro-F1
 
### Week 7 — Fine-tune the router
 
**16 – 22 Nov · Goal:** a transformer I trained, measured against alternatives, running in the pipeline.
 
**Learn:** BERT architecture · WordPiece tokenization · the [CLS] token · fine-tuning vs training from scratch
 
**Build**
- [ ] `ml/train_router.ipynb` on Colab: `distilbert-base-uncased` (try `distilbert-base-multilingual-cased` if Hinglish scores badly), max length 64, batch 16, learning rate 2e-5 – 5e-5, 4–6 epochs, weight decay 0.01; keep the best epoch by validation macro-F1
- [ ] Evaluate on the internal and the friends' test sets: accuracy, macro-F1, confusion matrix, and 10 misclassified examples with notes
- [ ] Compare with the TF-IDF baseline and zero-shot LLM classification on accuracy, latency and cost
- [ ] Export with `save_pretrained`; load in `backend/app/router.py`
- [ ] Confidence threshold: below it, treat the question as out of scope or fall back to the LLM
- [ ] Use the router's output to filter retrieval and the tool list
- [ ] **Sunday — tiny GPT part 3:** full transformer block, training, text generation
**Definition of Done:** the router runs inside `/ask`; the comparison table is filled in `ml/eval/results.md`.
 
**Explain it:** BERT vs GPT (encoder vs decoder, bidirectional vs causal attention) · what fine-tuning changes · why [CLS] is used for classification · the confidence threshold · what the confusion matrix showed
 
### Week 8 — Orbitals & bonding + checkpoint v0.2
 
**23 – 29 Nov · Goal:** the fourth scene and the complete AI pipeline.
 
**Build**
- [ ] Orbitals as point clouds: sample points from `|ψ|²` of the hydrogen wavefunctions (1s, 2p x/y/z, 3d) by rejection sampling; `show_orbital(type)`
- [ ] `bring_atoms_together(a, b)` — two 1s clouds approach and overlap, with higher density between the nuclei (illustrative)
- [ ] Molecules from PubChem 3D conformers (H₂, H₂O, CH₄, CO₂) drawn as spheres and cylinders; `show_molecule(name)`
- [ ] `show_bond_angle(on)` (H₂O ≈ 104.5°, CH₄ ≈ 109.5°), `show_lone_pairs(on)`
- [ ] Tool calling + RAG for chemistry
- [ ] Tag **v0.2.0**; record the full-pipeline demo
**Definition of Done:** router → RAG → LLM → validated actions → 3D works on 4 scenes.
 
**Explain it:** an orbital as a probability density · sampling a 3D distribution · VSEPR and why water is bent · how this scene connects to the double-slit scene
 
---
 
## 8. Month 3 — Heart, Evaluation, Delivery
 
### Week 9 — Heart & blood flow
 
**30 Nov – 6 Dec · Goal:** all 5 scenes working with the tutor.
 
**Build**
- [ ] Get a heart model (Z-Anatomy or NIH 3D), check its license, decimate it, and export as glTF with Draco compression (target under 5 MB)
- [ ] Name meshes for chambers and valves; `highlight(part)` and `focus(part)`, with click-to-select
- [ ] `play_animation("heartbeat")` — scale pulse or morph targets
- [ ] `trace_blood_path()` — particles along `CatmullRomCurve3` paths, red (oxygenated) and blue (deoxygenated), through the lungs and body
- [ ] `cutaway(on)` — clipping plane
- [ ] Tool calling + RAG for the heart
- [ ] **Fallback:** if there's no usable model by Wednesday, build a stylised heart from basic shapes with the same part names and actions
**Definition of Done:** all 5 scenes work with the AI tutor.
 
**Explain it:** glTF and Draco · raycasting for clicks · animating particles along a curve · clipping planes
 
### Week 10 — Evaluation
 
**7 – 13 Dec · Goal:** real numbers and an honest failure analysis.
 
**Build**
- [ ] `ml/eval/cases.json` — 50 cases (10 per concept): question, scene, expected sub-topic, acceptable actions, key facts
- [ ] `ml/eval/run_eval.py` — calls `/ask`; scores routing, actions (any acceptable match), key facts present and latency; writes `results.md`
- [ ] Rate answer correctness by hand (1–5); optionally add LLM-as-judge and spot-check it
- [ ] Grounding check: is each answer supported by the sources it returned?
- [ ] Fix the 5 worst failures (prompt, tool descriptions, data, thresholds); re-run and record before/after
- [ ] **Bonus:** Whisper voice input
**Definition of Done:** the README's evaluation tables contain real numbers, plus a short failure analysis in `results.md`.
 
**Explain it:** why LLM output is hard to evaluate · automatic vs manual vs LLM-as-judge · the before/after of my fixes
 
### Week 11 — Deploy + optimise
 
**14 – 20 Dec · Goal:** a public link that works on a cheap phone.
 
**Build**
- [ ] Export the router to ONNX and quantize to int8; compare size, latency and accuracy with the PyTorch version
- [ ] Deploy the backend to Hugging Face Spaces (Docker) or Render, and the frontend to Vercel; set env vars and CORS
- [ ] Protect the public demo: per-IP rate limit, a fast low-cost LLM model, cached answers for the demo questions, a spending cap
- [ ] Test on a low-end Android phone: lazy-load scenes, compress textures, cap the pixel ratio, check the frame rate
- [ ] Loading states, clear error messages, and a friendly fallback when the LLM is unavailable
- [ ] GitHub Actions: ruff + pytest on every push
- [ ] **Bonus:** LoRA fine-tune of a small open LLM for simpler explanations, compared on the eval set
**Definition of Done:** the public link works on a phone; CI is green.
 
**Explain it:** ONNX and quantization trade-offs · CORS · cold starts on free hosting · how I keep API cost under control
 
### Week 12 — Presentation + interview prep
 
**21 – 27 Dec · Goal:** a project I can present and defend.
 
**Build**
- [ ] README: live link, demo GIF, architecture diagram, real results, verified credits
- [ ] 2–3 minute demo video (script in section 11)
- [ ] Resume bullets with real numbers (section 11)
- [ ] 2 mock interviews using the question bank — with a friend, or recorded
- [ ] Tag **v1.0.0** and write release notes
- [ ] Optional: LinkedIn post with the demo video
**Definition of Done:** live link, GitHub repo, video and resume bullets are ready, and I can answer every question in section 11 without notes.
 
---
 
## 9. Build Reference
 
### Router labels (16)
 
| Concept | Sub-topics |
|---|---|
| `solar_system` | `planets` · `satellite_orbits` · `orbital_speed` |
| `svm` | `margin` · `support_vectors` · `kernel_trick` |
| `quantum` | `interference` · `wave_particle` · `observation` |
| `chemistry` | `orbitals` · `bonding` · `molecular_shape` |
| `heart` | `chambers` · `valves` · `circulation` |
| — | `out_of_scope` |
 
### Scene actions
 
| Scene | Actions |
|---|---|
| Solar system | `focus` · `set_time_speed` · `set_satellite_speed` · `show_orbit` · `show_vectors` · `label` |
| SVM | `highlight_support_vectors` · `show_margin` · `apply_kernel` · `lift_to_3d` · `set_param` |
| Double-slit | `fire_particles` · `set_slit_gap` · `set_wavelength` · `toggle_detector` · `reset_screen` |
| Chemistry | `show_orbital` · `bring_atoms_together` · `show_molecule` · `show_bond_angle` · `show_lone_pairs` |
| Heart | `highlight` · `focus` · `play_animation` · `trace_blood_path` · `cutaway` |
 
### Action definition pattern
 
```python
from pydantic import BaseModel, Field
 
class FireParticles(BaseModel):
    """Fire particles through the slits one at a time."""
    n: int = Field(ge=1, le=5000, description="Number of particles to fire")
 
SCENE_ACTIONS = {
    "double_slit": {
        "fire_particles": FireParticles,
        # "set_slit_gap": SetSlitGap, ...
    },
}
 
# The same models generate the LLM's tool definitions
# and validate every call the LLM makes.
```
 
### Prompt structure
 
```
SYSTEM:  You are VistaraX, a patient tutor for school and college students.
         - Answer in 3–6 short sentences at the student's level.
         - Use ONLY the provided context and cite its source IDs.
         - Use the scene tools to show what you explain.
         - If the context doesn't cover the question, say so.
CONTEXT: <retrieved chunks with source IDs>
SCENE:   <current state, e.g. detector off, wavelength 500 nm>
HISTORY: <last 4 turns>
USER:    <question>
```
 
### Repo structure
 
Same as the README's *Project Structure*, plus `backend/tests/` and `.github/workflows/ci.yml`.
 
### Git workflow
 
- `main` always works; one branch per feature (`feat/double-slit`, `fix/validator-args`)
- Commit prefixes: `feat:` · `fix:` · `docs:` · `test:` · `refactor:`
- Merge through pull requests, even working solo — note what changed and why
- Tags: `v0.1.0` (Week 4) · `v0.2.0` (Week 8) · `v1.0.0` (Week 12)
---
 
## 10. Risks & Fallbacks
 
| Risk | Early warning | Fallback |
|---|---|---|
| 3D learning curve eats Month 1 | Week 1 not done by Sunday | Lean on drei helpers and examples; cut decorative polish |
| LLM calls wrong or invalid actions | Many validator drops | Fewer tools per scene, clearer tool descriptions, 2–3 examples in the prompt; verify with the eval |
| Router data too clean | High internal score, low friends' test score | Add messier questions; collect more friend-written data |
| No usable heart model | Nothing found by Wednesday of Week 9 | Stylised heart from basic shapes |
| Free hosting runs out of memory | Deploy crashes on start | ONNX int8 router; host the backend on Hugging Face Spaces |
| API bill grows | Usage spikes | Low-cost model, caching, rate limiting, spending cap |
| Falling behind | Two weeks' Definition of Done missed | Cut in this order: heart detail → extra molecules → extra interactions. Never cut the router, RAG, validation or evaluation |
| Placements start early | — | Keep `main` demo-ready from v0.1; v0.2 is already a complete story (full AI pipeline, 4 scenes) |
 
---
 
## 11. Placement Kit
 
### Resume bullets
 
Replace X, Y and Z with measured numbers only.
 
- Built **VistaraX**, an AI-powered 3D learning platform (React Three Fiber, FastAPI) with 5 interactive scenes spanning physics, machine learning, quantum physics, chemistry and biology.
- Fine-tuned **DistilBERT** to route student questions across 16 sub-topics, reaching **X% macro-F1** vs **Y%** for a TF-IDF baseline; quantized it to ONNX int8 for a **Z× smaller** model.
- Designed an **LLM tool-calling pipeline** with **RAG** (sentence-transformers + Chroma) and schema-validated scene actions, achieving **X% correct actions** on a 50-question end-to-end benchmark.
### 30-second pitch
 
"VistaraX is an AI tutor that explains hard concepts in interactive 3D. A student asks a question; a DistilBERT model I fine-tuned routes it to the right concept, RAG grounds the answer in NCERT content, and an LLM uses tool calling to control the 3D scene while it explains. Every action is validated, and I evaluated the whole pipeline on a 50-question benchmark."
 
### 2-minute walkthrough
 
1. **Problem** (15 s) — students memorise things they've never seen
2. **Live demo** (45 s) — satellite speed, kernel trick, double-slit detector
3. **Architecture** (30 s) — router → RAG → LLM tools → validation → 3D
4. **Hardest problem** (20 s) — one real bug or decision and how I solved it
5. **Results and next steps** (10 s) — measured numbers, v2 plans
### 3-minute demo script
 
1. Solar system — ask *"Why doesn't the satellite fall?"*; vectors appear; push the speed until it escapes
2. SVM — ask *"What does the kernel trick do?"*; the points lift into 3D
3. Double-slit — fire 2,000 particles; ask *"What happens if we watch which slit it goes through?"*; the fringes vanish
4. Point to the sources under an answer
5. Close on the evaluation table
### Hardest-problem story (fill in during the build)
 
Situation → what went wrong → how I debugged it → what I measured before and after → what I'd do differently
 
### Question bank
 
**LLMs & agents** — How does tool calling work? · How do you prevent invalid tool calls? · How do you handle conversation history and context length? · How would you cut latency and cost?
 
**RAG** — Why RAG instead of fine-tuning for knowledge? · How did you choose chunk size and top-k? · What is an embedding? What is cosine similarity? · How did you measure retrieval quality?
 
**Transformers** — Explain self-attention. · BERT vs GPT? · What does fine-tuning change? · Why the [CLS] token? · How does WordPiece tokenization work?
 
**ML fundamentals** — How does an SVM find the maximum margin? · What does the kernel trick do? · Precision, recall and macro-F1? · How did you avoid data leakage?
 
**System & deployment** — Walk me through one request end to end. · Why quantize to ONNX? · How would you scale to 10,000 students? · How do you control API costs?
 
**Project** — What was the hardest part? · What failed in evaluation, and how did you fix it? · What would you do differently?
 
### Skills this project lets me claim honestly
 
Generative AI · LLMs · tool/function calling · agents · RAG · embeddings · vector databases · transformers · fine-tuning (Hugging Face) · PyTorch · model evaluation · ONNX quantization · FastAPI · REST APIs · React · Three.js · CI · deployment
 
---
 
## 12. Progress Tracker
 
⬜ not started · 🟨 in progress · ✅ done
 
| Week | Focus | Status | Hours | Notes |
|---|---|---|---|---|
| 0 | Setup | ⬜ | | |
| 1 | 3D basics + solar system | ⬜ | | |
| 2 | Satellites + SVM | ⬜ | | |
| 3 | Backend + tool calling | ⬜ | | |
| 4 | Double-slit · **v0.1** | ⬜ | | |
| 5 | RAG | ⬜ | | |
| 6 | Router dataset | ⬜ | | |
| 7 | Fine-tune router | ⬜ | | |
| 8 | Orbitals & bonding · **v0.2** | ⬜ | | |
| 9 | Heart | ⬜ | | |
| 10 | Evaluation | ⬜ | | |
| 11 | Deploy + optimise | ⬜ | | |
| 12 | Presentation · **v1.0** | ⬜ | | |
 
---
 
## 13. Weekly Log Template
 
```
### Week N — <dates>
Done:
Learned (explain in 2–3 lines):
Stuck on / how I solved it:
Numbers measured:
Next week:
Hours:
```
 
---
 
## 14. Resources
 
| Topic | Resource |
|---|---|
| React Three Fiber | Official docs and pmndrs examples |
| drei | drei docs |
| Three.js | *Three.js Journey* by Bruno Simon (paid); free YouTube tutorials |
| FastAPI | Official tutorial |
| Tool calling | Anthropic and OpenAI tool-use docs |
| RAG | sentence-transformers docs · Chroma docs |
| Transformers | Hugging Face NLP course · *The Illustrated Transformer* (Jay Alammar) |
| From scratch | Andrej Karpathy — *Let's build GPT* and *Neural Networks: Zero to Hero* |
| SVM | scikit-learn SVM user guide · StatQuest SVM videos |
| Double-slit & orbitals | HyperPhysics · NCERT Class 11–12 physics and chemistry |
| ONNX | Hugging Face Optimum · ONNX Runtime docs |
| 3D assets & data | NASA 3D Resources · Solar System Scope · PubChem · Z-Anatomy · NIH 3D |
 