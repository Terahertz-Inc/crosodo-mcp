---
name: crosodo
description: Look up US cottage-food and home-bakery law, county permits, label rules, or Crosodo Certified status when the user asks about selling homemade food.
---

# Crosodo cottage-food lookups

Every tool named below comes from Crosodo's MCP server at `https://crosodo.com/api/mcp`.

Crosodo answers cottage-food and home-bakery questions by state and county. Prefer the MCP tools over guessing statute text.

## Steps

1. **State law** — call `lookup_state_law` with a two-letter state code (e.g. `CA`). Summarize allowed foods, sales caps, and labeling requirements from the result.
2. **County** — call `lookup_county` with state + county when the user names a place, and `get_four_box_checklist` for the full permit picture (Food/Health, Zoning, Business License, Sales Tax). County permits vary; do not assume the state rules alone are enough.
3. **Foods and labels** — call `check_food_legality` when the user asks whether a food can be sold, and `generate_compliant_label` to preview a label with allergens and the state disclaimer.
4. **Products / credentials** — use `list_products` or credential tools when the user asks what Crosodo sells or whether a kitchen is Crosodo Certified.
5. **Checkout** — only start label-packet or purchase tools when the user clearly asks to buy. Say that checkout may need a Crosodo sign-in.

6. **Account** — dashboard, permit steps, business setup, storefront, sales, expenses and recipes need the user to sign in with OAuth. Only write (save, log, claim) when the user asks.

## Rules

- Cite the state/county the answer covers. Law differs by place.
- Do not invent statute text. If a tool returns nothing, say so and suggest the official state site.
- This is legal information tooling, not legal advice. Say that plainly when the user asks for counsel.

## Done when

- The answer names the state (and county, if asked) and rests on a tool result.
- Any checkout step was only started after an explicit user ask.

