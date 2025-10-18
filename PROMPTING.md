# PROMPTING.md

## 1) What I asked the AI to help me with 
I used ChatGPT to plan options, stabilise function input/output, draft pseudocode, challenge edge cases, and iteratively improve code and documentation. The goal was a small hybrid app in Colab: fetch (no-key), two charts, simple NLP, and a widgets UI.

## 2) Intentional Prompting Techniques Used
- **Problem restatement & option choice**: I restated the brief and compared dashboard/chatbot/hybrid and chose **Hybrid** for balanced scope.
- **Input/output contracts first**: asked the AI to define Args/Returns for the 5 core functions to prevent downstream breakage.
- **Pseudocode-first**: precipitation visual—requested steps before asking for code.
- **Edge-case challenges**: explicitly prompted for 404 fix when location contains “in/today/tomorrow” and handle missing & non-numeric values.
- **Modular improvements**: establish `output_type = 'display'|'figure'` so plots are testable without auto-show.
- **Trade-offs**: discuss wttr.in (no key, ~3 days) vs 5-day sources; keep toggle as future option.

## 3) Before/After Evidence 
### 3.1 Precipitation approximation
- **My prompt (excerpt)**: “Add a method switch (mean8/mean24/sum) and safe parsing of `precipMM`. Includd labels and input validation.”
- **Improvement**: Flexible method + robust parsing; clearer chart.
- **Links**: `before-after/Precipitation approximation.md` · `ai-conversations/conversation3.txt`
- **Trace**: Implemented in `Notebook.ipynb` (visualisation function)

### 3.2 NLP location parsing (404 fix)
- **My prompt (excerpt)**: “Strip stop-words (in/today/tomorrow) from location; fallback to typed Location if parsing fails.”
- **Improvement**: 404 eliminated; natural questions work.
- **Links**: `before-after/NLP location parsing (404 fix).md` · `ai-conversations/conversation4.txt`
- **Trace**: `parse_weather_question()` and UI cell

### 3.3 Temperature chart polish
- **My prompt (excerpt)**: “Add axis labels, legend, and return a Figure when `output_type='figure'`.”
- **Improvement**: Readable plot + figure-return contract verified in tests.
- **Links**: `before-after/Temperature chart polishing.md` · `ai-conversations/conversation2.txt`
- **Trace**: `create_temperature_visualisation()`

## 4) Handling a wrong/unsafe suggestion
- **Issue**: Initial parser treated “Perth tomorrow” as a raw location → wttr.in 404.
- **Prompted fix**: stop-word truncation + UI fallback; added input checks.
- **Outcome**: Questions like “Will it rain in Perth tomorrow?” now succeed.

## 5) Why this improved the implementation
Defining input/output first to reduce rework. Then, pseudocode-first made the precipitation logic correct on the first try. And, edge-case prompts produced real fixes; the output-type contract enabled testable figures. Overall, prompting moved quick drafts to a clearer and more reliable notebook.

*(All full conversations are in `ai-conversations/`. Each improvement also appears in `before-after/` with code diffs.)*
