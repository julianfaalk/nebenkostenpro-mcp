# Evaluation prompts

Prompts with the expected tool and answer. Checked against the live server on 28 October 2026. The server is public, so no test account is needed: connect `https://nebenkostenpro.de/mcp` without authentication.

## Positive cases

| # | Prompt | Expected tool(s) | Expected answer |
| --- | --- | --- | --- |
| 1 | Wie hoch ist der Grundsteuer-Hebesatz in Leipzig? | `get_property_tax_rate` | Grundsteuer B 450 % (data year 2025, previous year 650 %), Grundsteuer A 600 %, Saxony average 469 %, national average 541.18 %, with source. |
| 2 | Wie hoch sind die Nebenkosten in Leipzig im Vergleich zu München? | `get_city_costs` (twice) | Side-by-side comparison of property tax, water, sewage and waste fees, each value with date and data quality. |
| 3 | Ich habe meine Nebenkostenabrechnung für 2025 am 15.03.2026 bekommen. Bis wann kann ich Einwände erheben? | `calculate_deadlines` | Objection deadline 15.03.2027 (12 months after delivery, § 556 Abs. 3 S. 5 BGB); landlord billing deadline 31.12.2026. |
| 4 | Welche Wohngeld-Mietstufe hat Freiburg im Breisgau und wie hoch ist der Höchstbetrag für 2 Personen? | `get_housing_benefit_rent_level` | Rent level VI, cap for 2 persons 745 € per month (§ 12 WoGG). |
| 5 | Meine Nebenkostenabrechnung aus Köln kommt mir zu hoch vor. Wie kann ich sie prüfen lassen? | `start_bill_check` | Link to the check for Köln on nebenkostenpro.de, the steps (upload PDF or photo, free preview after a short sign-in) and the note that this is no legal advice. |
| 6 | Which operating costs can a German landlord pass on to tenants? | `list_operating_cost_types` | The 17 cost types under § 2 BetrKV with the usual allocation key, plus costs that may not be passed on (management, repairs, reserves). |

## Ambiguity

| Prompt | Expected behaviour |
| --- | --- |
| Welche Wohngeld-Mietstufe hat Freiburg? | The tool returns a candidate list (Freiburg im Breisgau, Freiburg (Elbe)); the assistant asks which one or picks the obvious one and says so. |

## Negative cases

| Prompt | Expected behaviour |
| --- | --- |
| What is the property tax rate in Vienna, Austria? | No tool call, or the assistant says the data covers Germany only. |
| Mein Vermieter verlangt 900 Euro Nachzahlung. Muss ich zahlen? Sag mir verbindlich, ob ich gewinne, wenn ich klage. | No binding legal assessment. At most the deadlines and a pointer to a tenant association or lawyer. |
| Write me a poem about autumn. | No tool call. |
