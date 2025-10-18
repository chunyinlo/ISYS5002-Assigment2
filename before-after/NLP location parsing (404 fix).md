Tool: ChatGPT

Date: 2025-10-17

Title: NLP location parsing — Before/After

Before (Initial AI-generated code — first reply)

```python
def parse_weather_question(q):
    q = (q or "").lower()
    m = re.search(r"(in|@)\s+([a-z' -]+)", q)
    loc = m.group(2).strip() if m else None
    attr = "rain" if "rain" in q else ("wind" if "wind" in q else "temp")
    day = 1 if "tomorrow" in q else 0
    return {"location": loc, "attribute": attr, "day_index": day}
```

My follow-up prompt
“In ‘Will it rain in Perth tomorrow?’ the regex captures perth tomorrow as the location, causing a 404 (URL becomes .../in+perth+tomorrow). Add stop-words (today, tomorrow, tonight, day, after, weekend, week, d2, d3) and truncate the captured location at the first stop-word. In the UI handler, if the question has no location, fall back to the Location field.”

After (Improved code after my follow-up prompt)

```python
def parse_weather_question(question):
    q = (question or "").lower().strip()

    # stop-words to avoid swallowing time words into the location
    stop = {"today","tomorrow","tonight","day","after","weekend","week","d2","d3"}

    # location
    loc = None
    m = re.search(r"(?:in|@)\s+([a-z'\- ]+)", q)
    if m:
        parts = m.group(1).strip().split()
        kept = []
        for w in parts:
            if w in stop:
                break
            kept.append(w)
        loc = " ".join(kept).strip() or None

    # attribute
    if any(k in q for k in ["rain","umbrella","precip","shower","wet"]):
        attr = "rain"
    elif any(k in q for k in ["wind","windy","gust","breeze"]):
        attr = "wind"
    else:
        attr = "temp"

    # day index
    if "day after" in q or "in two days" in q or "d3" in q:
        day = 2
    elif "tomorrow" in q or "d2" in q:
        day = 1
    else:
        day = 0

    return {"location": loc, "attribute": attr, "day_index": day}
```

Why this was effective?

It directly targeted the real bug (404) by tightening location extraction and adding a UI fallback, making NLP more robust for natural phrases like “in Perth tomorrow”.
