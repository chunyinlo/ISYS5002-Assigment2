# 🌦️ WeatherWise Template

## Project Overview
This is a lean Hybrid solution: two visualisations (temperature line, precipitation bar) + simple NLP Q&A + a small ipywidgets form.  
**Data source:** wttr.in JSON (`https://wttr.in/<location>?format=j1`) – no API key, typically ~3-day forecast.

## How to Run (Google Colab)
1. Open the [Notebook](Notebook.ipynb) in Colab.
2. Run **Setup and Configuration** cells (installs: `requests`, `matplotlib`, `ipywidgets` if needed).
3. Run sections in order: Weather Data → Visualisations → NLP → Main Logic → UI.
4. In the form, set *Location/Days* and click **Fetch & Plot**; try a question like  
   *“Will it rain in Perth tomorrow?”*

## AI Conversations & Before/After
**Conversations (text files):**
- [ai-conversations/conversation1.txt](ai-conversations/conversation1.txt) – Implementation options
- [ai-conversations/conversation2.txt](ai-conversations/conversation2.txt) – Function I/O and data model
- [ai-conversations/conversation3.txt](ai-conversations/conversation3.txt) – Pseudocode → precipitation chart
- [ai-conversations/conversation4.txt](ai-conversations/conversation4.txt) – Edge cases & debugging (NameError, 404 fix)
- [ai-conversations/conversation5.txt](ai-conversations/conversation5.txt) – Modular helper & trade-offs

**Before/After examples:**
- [before-after/Precipitation approximation.md](before-after/Precipitation%20approximation.md) – Precipitation approximation
- [before-after/NLP location parsing (404 fix).md](before-after/NLP%20location%20parsing%20(404%20fix).md) – NLP location parsing (404 fix)
- [before-after/Temperature chart polishing.md](before-after/Temperature%20chart%20polishing.md) – Temperature chart polish

## Notes & Limitations
- wttr.in usually provides ~3 days; the app caps plots to available days.
- If a strict 5-day visual is required, you can switch the data source to Open-Meteo (no key) as a future extension.

