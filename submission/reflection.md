# ✍️ Project Reflection

## AI Tools Used
I primarily used ChatGPT to plan the solution, reason about design trade-offs, and iteratively refine code. I also used it to draft and polish documentation. In code, ChatGPT helped me transform rough ideas into workable Python for requests + JSON parsing, matplotlib visualisations, and a small ipywidgets UI. I deliberately did not use Copilot or external wrappers so that the notebook demonstrated manual control of inputs/outputs and error handling.

## Prompting Techniques
I applied multiple intentional prompting strategies. First, to restate the problem and compared implementation options (dashboard, chatbot, hybrid).Second, defined I/O contracts for each core function to stabilise signatures.
And, request pseudocode first for the precipitation chart, then asked for code. Then, tried to challenge edge cases like empty/missing keys nad non-numeric values. And, requested modular improvements and queried design trade-offs

## What Worked Well?
I’m most proud of turning the precipitation visualisation from a naïve hourly sum into a flexible approach with a method switch (mean8, mean24, sum) and safe parsing. This made the chart defensible and assessor-friendly (labels, title, robust defaults) while still staying within basic matplotlib. It also showed clear evidence of intentional prompting from pseudocode → implementation → refinement.

## What Would You Do Differently?
If I had more time, I would add a data-source toggle to support 5-day forecasts via Open-Meteo (no key) while keeping wttr.in as the default. I would also extend the NLP beyond rules to cover more attributes (humidity/UV) and add lightweight tests to lock the I/O contract. Finally, I’d extract the core functions into a small helper module so the notebook cells stay even cleaner.

## Final Thoughts
The biggest learning was how targeted prompts accelerate high-quality outcomes. Like asking for I/O definitions prevented downstream breakage, pseudocode first avoided rework and edge-case prompts led to real fixes. For example like preventing a 404 from the phrase “in Perth tomorrow” by adding stop-word truncation and a UI fallback to the typed location. Overall, the notebook now demonstrates API interaction (no key), two clear visualisations, a simple but robust NLP layer, and tidy documentation of the AI process, evidenced by the Before/After examples and conversation logs.
