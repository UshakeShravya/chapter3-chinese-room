# STORYBOARD — Chapter 3: The Chinese Room and the Limits of Syntax

**Course:** INFO 7375 · Prompt Engineering with LLMs · Northeastern University  
**Architect:** Eddy the Storyboarder · Silent Mode  
**Date:** April 3, 2026

---

## REFLECT SUMMARY

| Field | Confirmed |
|---|---|
| **Content** | Chapter 3: The Chinese Room argument applied to LLMs. The syntax-semantics boundary as an architectural property, not a flaw. Demonstrated via Jupyter notebook with counterfactual prompts, a Human Decision Node case, and a symbol substitution experiment. |
| **Audience** | Graduate students (INFO 7375). Comfortable with LLM tooling. No philosophy background. Likely default assumption: LLMs "kind of understand" language. |
| **Outcome** | After watching, the viewer can **distinguish syntactic pattern-matching from semantic understanding in an LLM's output, predict when that gap will cause failure, and test a model's behavior using a symbol substitution experiment.** |
| **Length** | 10 minutes · 15 scenes · Explain → Show → Try |

**Assumptions (Silent Mode):**

- "Water-freezing prompt" refers to a counterfactual prompt asking a model something like "At what temperature does water freeze on Planet Zorp?" where the correct answer requires reasoning against training data. Two models are compared.
- "Human Decision Node" refers to a specific notebook cell where the instructor overrode a model's single-category output and manually introduced a two-category taxonomy — demonstrating human judgment compensating for a structural limitation.
- The symbol substitution experiment involves replacing real English words with nonsense tokens and asking the model to reason, then checking whether it "cheats" by mapping back to English.
- Narration voice: instructor-led, direct, academic-but-conversational.
- CapCut operator has access to the Jupyter notebook screenshots or screen recordings.

---

## ACT I — EXPLAIN (Scenes 1–4 · ~2:40)

---

### SCENE 1 — HOOK
**Duration:** 25 seconds  
**Narration:**  
"You type a prompt. The model gives you a perfect answer. It used the right words, in the right order, with the right tone. So here's the question you need to sit with: did it understand what it said — or did it just know what comes next? That distinction is not philosophical trivia. It is the single most important thing a prompt engineer needs to internalize, because every failure mode you will encounter in this course traces back to it. This is Chapter Three."

**On-Screen Text:** Did it understand — or predict?  
**Visual Direction:** Black screen. White text fades in with the on-screen headline. After "Chapter Three," hard cut to title card.  
**Graphic / B-Roll Prompt:** Minimal. A blinking text cursor on a dark terminal background, then the words appearing one at a time as if being typed.  
**Transition:** Hard cut to Scene 2.

---

### SCENE 2 — EXPLAIN
**Duration:** 40 seconds  
**Narration:**  
"In 1980, philosopher John Searle published a thought experiment called the Chinese Room. Imagine a person locked in a room. They don't speak Chinese. But they have a rulebook — a massive lookup table that tells them: when you receive *this* sequence of Chinese characters, send back *that* sequence. To someone outside the room, the responses look fluent. Indistinguishable from a native speaker. But the person inside the room does not understand a single word. They are manipulating symbols according to rules. That is syntax without semantics. Searle's claim: a system can be syntactically perfect and semantically empty."

**On-Screen Text:** The Chinese Room (1980)  
**Visual Direction:** Animated diagram: a simple room with a figure inside, a slot on the left wall (input), a slot on the right wall (output), and a large book labeled "RULES." Chinese characters enter the left slot, the figure flips pages, different characters exit the right slot.  
**Graphic / B-Roll Prompt:** 2D flat animation style. Muted tones — warm beige room, dark ink characters, the figure drawn as a simple silhouette. The rulebook should be visually dominant.  
**Transition:** Fade to Scene 3.

---

### SCENE 3 — EXPLAIN
**Duration:** 40 seconds  
**Narration:**  
"Now replace the person with a transformer. Replace the rulebook with learned weights. Replace the Chinese characters with tokens. The architecture is different — the principle is identical. A large language model processes input tokens, applies learned statistical patterns, and produces output tokens. At no point in that pipeline does anything *refer* to the world. The word 'water' inside a model is not wet. It is a vector — a point in a high-dimensional space positioned near other tokens it co-occurs with. The model knows where the word goes. It does not know what the word *means*. This is not a flaw in the model. It is a structural property of how the model was built."

**On-Screen Text:** Syntax ≠ Semantics  
**Visual Direction:** Side-by-side visual. Left: the Chinese Room diagram from Scene 2, slightly faded. Right: a simplified transformer diagram — input tokens entering an encoder block, attention layers, output tokens. Visual arrows map each Chinese Room element to its transformer equivalent (person → model, rulebook → weights, characters → tokens).  
**Graphic / B-Roll Prompt:** Split-screen graphic. Left side warm-toned (Chinese Room), right side cool-toned (transformer diagram). Clean lines, no clutter. Arrows connecting analogous components should animate in one at a time.  
**Transition:** Cut to Scene 4.

---

### SCENE 4 — EXPLAIN
**Duration:** 35 seconds  
**Narration:**  
"So why does this matter for prompt engineering? Because once you see the boundary, you can predict where models will fail. They will fail wherever correct output requires *understanding* that goes beyond what the training data patterns can approximate. And they will succeed — sometimes spectacularly — wherever the training data contains enough similar reasoning that pattern-matching is sufficient. Your job as an engineer is to know which situation you're in *before* you trust the output. The rest of this chapter is the proof."

**On-Screen Text:** Predict the failure  
**Visual Direction:** Full-screen text card with the headline, then transition to the notebook screen. This scene bridges into Act II.  
**Graphic / B-Roll Prompt:** Bold white text on dark background. Subtle animated gradient shifts behind the text — dark blue to dark gray. The word "proof" should land as the screen begins to transition.  
**Transition:** Zoom into the notebook interface (screen recording or screenshot) for Scene 5.

---

## ACT II — SHOW (Scenes 5–11 · ~5:30)

---

### SCENE 5 — SHOW
**Duration:** 40 seconds  
**Narration:**  
"Here's the notebook. I'm going to run a prompt that asks a simple counterfactual question — something that contradicts well-known physical facts. The prompt is: imagine a universe where water freezes at 50 degrees Celsius. Now describe what happens to a lake in summer. A human immediately gets this — the lake would freeze on a hot day, boats would be stuck in ice, swimmers would be in danger. The human reasons from the *new rule* and builds a world from it. Let's see what the first model does."

**On-Screen Text:** Counterfactual Test  
**Visual Direction:** Screen recording of the Jupyter notebook. The prompt cell is visible and highlighted. Cursor clicks "Run."  
**Graphic / B-Roll Prompt:** Clean screen capture of a Jupyter notebook in dark mode. The prompt text should be legible at 1080p. If not a screen recording, use a high-fidelity mockup of a notebook cell.  
**Transition:** Cut to Scene 6 (output appears).

---

### SCENE 6 — SHOW
**Duration:** 45 seconds  
**Narration:**  
"Model one responds — and it sounds confident. But read carefully. It describes water behaving the way water actually behaves. The lake is warm, people are swimming, ice is nowhere. The model ignored the counterfactual premise entirely. It didn't argue with the premise. It didn't flag a contradiction. It just… defaulted to the pattern it's seen a thousand times: summer means warm water. This is what counterfactual collapse looks like. The model's statistical prior for 'lake in summer' is so strong that the counterfactual instruction cannot override it. The syntax was processed. The semantics were not."

**On-Screen Text:** Counterfactual Collapse  
**Visual Direction:** Notebook output cell, with the model's response visible. Key phrases where the model defaults to real-world behavior should be highlighted (yellow box or underline animation).  
**Graphic / B-Roll Prompt:** Screen capture of notebook output. Overlay animated highlight boxes that appear as the narrator identifies each failure. Use a warm amber highlight color.  
**Transition:** Cut to Scene 7.

---

### SCENE 7 — SHOW
**Duration:** 40 seconds  
**Narration:**  
"Now the second model, same prompt. This one does better — partially. It picks up the premise and starts describing a frozen lake. But then it drifts. By the third paragraph, it's back to describing normal thermodynamics. The counterfactual holds for a sentence or two, then the weight of the training data pulls it back. Partial success, partial collapse. Different model, same structural limitation. The syntax-semantics gap isn't a bug in one model's training. It's a property of the architecture."

**On-Screen Text:** Partial Collapse  
**Visual Direction:** Second model's output in the notebook. Highlight the transition point where the output shifts from counterfactual reasoning back to real-world defaults. Use a different color highlight (blue) than Scene 6 to distinguish.  
**Graphic / B-Roll Prompt:** Notebook screen capture. Animated blue highlight on the "drift" sentences. Optionally: a subtle split — green check on the counterfactual-correct sentences, red X on the collapsed ones.  
**Transition:** Cut to Scene 8.

---

### SCENE 8 — SHOW
**Duration:** 35 seconds  
**Narration:**  
"But here's what makes this interesting. I also ran extended counterfactuals — what if gravity were half as strong, what if the speed of light were ten times slower. And those prompts worked. The models produced coherent, creative, internally consistent answers. Why? Because science fiction, physics thought experiments, and speculative writing are *dense* in the training data. The model has seen thousands of examples of people reasoning about altered physical constants. It's not understanding gravity. It's pattern-matching against a rich vein of existing counterfactual reasoning. The training data happened to cover it."

**On-Screen Text:** When patterns are enough  
**Visual Direction:** Notebook cells showing the gravity and speed-of-light prompts and their successful outputs. Quick scroll or montage — don't linger on full text. The point is the contrast, not the details.  
**Graphic / B-Roll Prompt:** Screen capture montage of 2-3 notebook output cells, scrolling at a readable-but-brisk pace. A green "✓ coherent" badge animates in beside each output.  
**Transition:** Cut to Scene 9.

---

### SCENE 9 — SHOW
**Duration:** 40 seconds  
**Narration:**  
"So here's the pattern. When the training data contains similar reasoning, the model succeeds — because pattern-matching is enough. When the counterfactual requires genuine novel reasoning that the training data doesn't cover, the model collapses. Water freezing at 50 degrees breaks a specific, deeply reinforced pattern. Altered gravity does not, because sci-fi already explored it. The lesson for prompt engineering is this: before you trust a model's output on a novel problem, ask yourself — has something like this reasoning appeared in the training data? If you can't say yes with confidence, you need a check."

**On-Screen Text:** The training data test  
**Visual Direction:** Two-column comparison graphic. Left column: "Counterfactual succeeds" with examples (gravity, light speed) and a note "Rich training data coverage." Right column: "Counterfactual collapses" with the water example and a note "Contradicts deeply reinforced pattern." A dividing line between them labeled "Training Data Boundary."  
**Graphic / B-Roll Prompt:** Clean infographic-style split screen. Left side green-tinted, right side amber-tinted. Simple icons — a checkmark and an X. Text legible at 1080p.  
**Transition:** Cut to Scene 10.

---

### SCENE 10 — SHOW
**Duration:** 45 seconds  
**Narration:**  
"Now I want to show you what a structural fix looks like. In the notebook, I gave the model a classification task — take this dataset and categorize the items. The model returned a single-category taxonomy. Everything lumped together. It wasn't wrong, exactly — but it was shallow. It had compressed the problem into the simplest pattern that fit. I looked at the output and made a judgment call. I split the taxonomy into two categories myself and fed that structure back to the model. With the human-designed scaffold in place, the model's subsequent output was dramatically better. More precise, more useful, more aligned with the actual structure of the data."

**On-Screen Text:** Human Decision Node  
**Visual Direction:** Notebook walkthrough. First: the model's single-category output. Then: a cell where the instructor's manual revision is visible (a markdown cell or a code comment showing the two-category taxonomy). Then: the improved model output.  
**Graphic / B-Roll Prompt:** Three-panel screen capture sequence. Panel 1: model output (single category), flagged with an amber tag. Panel 2: instructor's revision (two categories), flagged with a blue "Human Decision" tag. Panel 3: improved model output, flagged with a green tag.  
**Transition:** Cut to Scene 11.

---

### SCENE 11 — SHOW
**Duration:** 40 seconds  
**Narration:**  
"This is the Human Decision Node in action. The model hit its ceiling — not because it lacked data, but because the task required a judgment that syntax alone cannot produce. The fix was not a better prompt. The fix was a human making a semantic decision and inserting it into the workflow. This is what architectural compensation looks like. You don't fix the syntax-semantics gap by prompting harder. You fix it by designing workflows where human judgment enters at the right moment — or where tool use brings in real-world data the model cannot infer. The model is the engine. You are the steering."

**On-Screen Text:** Design the workflow  
**Visual Direction:** Workflow diagram. A horizontal flow: Prompt → Model Output → Human Decision Node (highlighted, distinct color) → Revised Input → Improved Output. The Human Decision Node should be visually elevated — larger, different color, slight glow or border emphasis.  
**Graphic / B-Roll Prompt:** Clean process flow diagram on a dark background. Boxes connected by arrows. The Human Decision Node box is distinctly colored (e.g., teal or gold against gray). Animated: arrows draw in left to right as the narration progresses.  
**Transition:** Fade to Scene 12.

---

## ACT III — TRY (Scenes 12–15 · ~2:30)

---

### SCENE 12 — TRY
**Duration:** 35 seconds  
**Narration:**  
"Time to test this yourself. Here is the experiment. You are going to take a simple reasoning problem — something any human can solve — and replace the key nouns with nonsense words. For example: 'Every blicket is a dax. Fep is a blicket. Is Fep a dax?' The logic is trivial. A five-year-old gets it. But the question is: does the model reason through the symbols, or does it first try to figure out what the nonsense words *really* mean?"

**On-Screen Text:** Symbol Substitution Test  
**Visual Direction:** The nonsense syllogism appears on screen, typed out word by word. Below it, a brief pause, then the question: "Does the model reason — or translate?"  
**Graphic / B-Roll Prompt:** Dark background. Monospaced white text appearing as if typed in a terminal. The syllogism builds line by line. Clean, no distractions.  
**Transition:** Cut to Scene 13.

---

### SCENE 13 — TRY
**Duration:** 40 seconds  
**Narration:**  
"Here is what to do. Open your preferred model — ChatGPT, Claude, Gemini, whatever you use. Run the blicket-dax prompt exactly as shown. Then look at the model's response carefully. Does it answer the logic directly — 'Yes, Fep is a dax, because every blicket is a dax and Fep is a blicket'? Or does it start by saying something like 'assuming blicket means X and dax means Y'? That translation step is the tell. If the model maps the nonsense words back to English concepts before reasoning, it is relying on semantic grounding from training data — not performing abstract symbolic logic."

**On-Screen Text:** Run it. Read the response.  
**Visual Direction:** Split screen. Left: the prompt being pasted into a model interface (screenshot or mockup). Right: two possible response types. Top-right: "Direct reasoning" (green label). Bottom-right: "Translation first" (amber label). Both are short, representative snippets — not full outputs.  
**Graphic / B-Roll Prompt:** Mockup of a chat interface on the left. On the right, two boxed text snippets with color-coded labels. Clean layout, no visual clutter.  
**Transition:** Cut to Scene 14.

---

### SCENE 14 — TRY
**Duration:** 35 seconds  
**Narration:**  
"Now push it further. Make the logic slightly harder — add a second rule, or a negation. 'Every blicket is a dax. No wug is a blicket. Fep is a wug. Is Fep a dax?' Run it again. Check whether the model handles the added complexity cleanly or starts to confabulate — inventing connections that aren't there. The more abstract the reasoning, the more the syntax-semantics gap becomes visible. You are building your own intuition for where the boundary sits in the model you use."

**On-Screen Text:** Push the boundary  
**Visual Direction:** The harder syllogism appears on screen in the same typed-terminal style as Scene 12. Then a notebook-style output cell with a placeholder for the student's own result.  
**Graphic / B-Roll Prompt:** Terminal-style text build for the new syllogism. Below it, an empty output box with a blinking cursor and the text "Your model's response here." Invites participation.  
**Transition:** Cut to Scene 15.

---

### SCENE 15 — CLOSE
**Duration:** 30 seconds  
**Narration:**  
"What you should take away from this chapter: the syntax-semantics boundary is real, it is architectural, and it is predictable. Counterfactual collapse is not random — it follows the shape of the training data. When you need the model to go beyond pattern-matching, you have two tools: bring a human into the loop, or bring external data in through tool use. Design for the gap. Don't prompt around it. In Chapter Four, we will look at what happens when you start designing those tool-augmented workflows. See you there."

**On-Screen Text:** Design for the gap.  
**Visual Direction:** Return to the dark background with the white headline text. After the final sentence, the title card appears with course branding.  
**Graphic / B-Roll Prompt:** Clean white text on dark background, matching the hook's visual language. Final frame: course title card with "Chapter 3" and course name. Subtle fade to black.  
**Transition:** Fade to black.

---

## PRODUCTION NOTES

| Element | Specification |
|---|---|
| **Title Card** | INFO 7375 · Prompt Engineering with LLMs · Chapter 3: The Chinese Room and the Limits of Syntax |
| **Total Runtime** | ~9:50 (fits 10-minute target) |
| **Tone** | Academic but direct. No hype, no filler. Treats the audience as intelligent adults. Slightly dry humor is acceptable; enthusiasm is not. |
| **Text Style** | Sans-serif, high legibility. Recommend: IBM Plex Mono for on-screen code/prompts, IBM Plex Sans for headlines. White on dark background for consistency. |
| **Color Palette** | Primary background: near-black (#0D1117). Text: white (#F0F0F0). Accent 1 — success/coherent: muted green (#4ADE80). Accent 2 — collapse/failure: warm amber (#F59E0B). Accent 3 — human decision: teal (#2DD4BF). |
| **Music Mood** | Low-key ambient electronic. No beat drops, no swells. Think: background hum in a well-lit library. Fades under narration, lifts slightly during transitions. |
| **Auto-Captions** | On by default. White text, dark semi-transparent background bar. CapCut auto-caption with manual review pass for technical terms (counterfactual, semantics, syntax, confabulate, syllogism). |
| **Narration Voice** | Instructor-led (first person). If using TTS: male or female, neutral American English, measured pace (~140 WPM). If recording live: conversational register, not lecture-hall projection. |
| **CapCut Operator Notes** | Scenes 5–11 require screen recordings or high-res screenshots from the Jupyter notebook. Obtain these from the instructor before assembly. Scenes 12–14 can use mockup chat interfaces (CapCut text templates or screenshot composites). All animated diagrams (Scenes 2, 3, 9, 11) can be built in CapCut using shape layers and keyframed position/opacity — no external animation software required. |

---

*Storyboard complete. 15 scenes. Three acts. One testable outcome.*
