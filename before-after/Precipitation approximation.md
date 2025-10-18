Tool: ChatGPT

Date: 2025-10-17

Title: Precipitation approximation — Before/After

Before (Initial AI-generated code — first reply)

```python
def create_precipitation_visualisation(data):
    rains = []
    for d in data["days"]:
        rains.append(sum(float(h["precipMM"]) for h in d["hourly"]))
    plt.bar(range(len(rains)), rains)
    plt.show()
```

My follow-up prompt
“precipMM may be per-interval rather than a daily total. Please add a method ∈ {mean8, mean24, sum} switch, handle missing/non-numeric values safely, and support output_type = 'display' or 'figure'.”

After (Improved code after my follow-up prompt)

```python
def create_precipitation_visualisation(weather_data, output_type='display', method="mean24"):
    days = weather_data.get("days", []) or []
    if not days:
        raise ValueError("No forecast days in weather_data")

    xs, rains = [], []
    for i, d in enumerate(days):
        xs.append(f"D{i+1}")
        hourly = d.get("hourly", []) or []
        vals = []
        hours = hourly[:8] if method == "mean8" else hourly
        for h in hours:
            try:
                vals.append(float(h.get("precipMM", 0.0)))
            except:
                pass
        if not vals:
            mm = 0.0
        elif method == "sum":
            mm = sum(vals)
        else:  # mean8 or mean24
            mm = sum(vals) / float(len(vals))
        rains.append(mm)

    fig, ax = plt.subplots()
    ax.bar(xs, rains)
    ax.set_title("Precipitation (approx)")
    ax.set_xlabel("Day")
    ax.set_ylabel("mm")


    if output_type == "figure":
        return fig
    plt.show()
    return None
```

Why this was effective?

The prompt clarified I/O and error handling, added a tunable method (mean8/mean24/sum) to avoid overcounting, and made the function easier to assess and reuse (display vs figure).

Source: conversation: ai-conversations/conversation3.txt



