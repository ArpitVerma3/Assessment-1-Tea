# AI Prompt Log — Mistvale Tea Co.

## Prompt 1
- **Tool:** Antigravity / Gemini 3.6 Flash
- **Type:** code & research
- **Prompt:**
  > Analyze index.html and BRAND.md and produce a structured audit covering functional bugs, business rule violations, accessibility, mobile, performance, SEO, design/UX issues, and a prioritized implementation plan.
- **Outcome:** accepted
- **Why:** Identified critical issues including null cart crash, parseInt("1,299") price corruption, closure bugs in Quick View, inverted search logic, boolean sort comparators, WELCOME10 coupon bugs, missing focus outlines, and brand color/font violations.

## Prompt 2
- **Tool:** Antigravity / Gemini 3.6 Flash
- **Type:** code
- **Prompt:**
  > Refactor index.html according to the audit plan: remove third-party libraries (jQuery, Font-Awesome, Animate.css), implement Vanilla JS store state engine (Category + Search + Sort), enforce business rules (max 5 units/stock limit, WELCOME10 logic, shipping threshold, Indian digit formatting, pincode error handling), apply BRAND.md design system (colors, typography, section order), add SEO/JSON-LD, and ensure mobile responsiveness.
- **Outcome:** accepted
- **Why:** Successfully implemented all business rules, UX design rules, accessibility, and SEO while retaining zero framework dependencies and leaving PRODUCTS, API, and footer legal text untouched.

## Prompt 3
- **Tool:** Gemini 3.1 Flash Image (generate_image)
- **Type:** image
- **Prompt:**
  > Create a premium realistic product photograph for Mistvale Tea Co., a tea brand from the Darjeeling hills.
  > Product: [PRODUCT NAME]
  > Description: [PRODUCT DESCRIPTION]
  > Show a single elegant tea package/pouch with the tea leaves or relevant ingredients subtly visible beside it. Natural warm lighting, earthy premium aesthetic, clean cream/parchment background, soft shadows, minimal composition, realistic commercial product photography.
  > Use a consistent visual style across all Mistvale Tea Co. products. No people, no hands, no extra text, no fake awards, no badges, no promotional claims. Square composition, centered product, high detail, web-optimized appearance.
- **Outcome:** accepted & modified
- **Why:** Generated high quality commercial photography for product catalog items (p101–p106). Standardized all 8 product images to square 1:1 aspect ratio on cream/parchment background.
