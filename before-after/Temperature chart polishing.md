Tool: ChatGPT

Date: 2025-10-17

Title: Temperature chart — Before/After

Before (Initial AI-generated code — first reply)

```python
def create_temperature_visualisation(data):
    xs = [f"D{i+1}" for i in range(len(data["days"]))]
    tmax = [float(d["maxtempC"]) for d in data["days"]]
    tmin = [float(d["mintempC"]) for d in data["days"]]
    plt.plot(xs, tmax)
    plt.plot(xs, tmin)
    plt.show()
```

My follow-up prompt

“Please add input validation (raise ValueError if no days), axis labels/title/legend, and support output_type='figure' (return the Figure) versus 'display' (show). Keep it basic matplotlib.”

After (Improved code after my follow-up prompt)

```python
def create_temperature_visualisation(weather_data, output_type='display'):
    days = weather_data.get("days", []) or []
    if not days:
        raise ValueError("No forecast days in weather_data")

    xs, tmax, tmin = [], [], []
    for i, d in enumerate(days):
        xs.append(f"D{i+1}")
        tmax.append(float(d.get("maxtempC", 0.0)))
        tmin.append(float(d.get("mintempC", 0.0)))

    fig, ax = plt.subplots()
    ax.plot(xs, tmax, label="Max °C")
    ax.plot(xs, tmin, label="Min °C")
    ax.set_title("Temperature Trend")
    ax.set_xlabel("Day")
    ax.set_ylabel("°C")
    ax.legend()

    if output_type == "figure":
        return fig
    plt.show()
    return None
```

Why this was effective?

The prompt added assessor-friendly elements (validation, labels, legend) and a clear return/display contract, making the function easier to test and reuse.

Source conversation: ai-conversations/conversation2.txt, ai-conversations/conversation5.txt
