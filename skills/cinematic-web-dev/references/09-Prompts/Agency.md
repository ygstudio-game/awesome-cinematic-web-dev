# Prompt: Premium agency website

```
Create a premium digital agency homepage combining cinematic storytelling with
clear service/case-study information architecture.

Stack (full recommended stack from README.md):
Next.js App Router, Tailwind v4, Motion.dev, Lenis, React Three Fiber + Drei for one
signature 3D hero moment, Theatre.js for its sequencing, ScrollyVideo.js + Scrollama
for case-study scrollytelling, MagicUI + ReactBits + 21st.dev for supporting UI.

Requirements:
- Hero: one signature R3F + Theatre.js sequence, scroll-driven, lazy-loaded, with a
  ScrollyVideo/static fallback on mobile and reduced-motion (per 06-3D/Spline.md
  and 08-Optimization guidance on progressive enhancement)
- Services section: clear, scannable, motion used only for entrance reveal, not as
  the primary communication device — clarity over cleverness for this section
- Case studies: Scrollama-driven step narrative per case study (07-Storytelling/Scrollama.md)
- Client logo strip, team/culture section, contact section
- Full mobile optimization — an agency site is often viewed on mobile by clients
  checking credibility on the go, this cannot be an afterthought

Avoid:
- Using the flagship 3D/Theatre.js technique more than once on the page — it should
  read as a deliberate signature moment, not a template repeated per section
- Sacrificing information clarity (what do you do, who have you worked with, how do
  I contact you) for visual spectacle — agency sites still need to convert leads

Follow production-quality architecture: case study content and services as typed,
data-driven content (CMS or local config), not hardcoded per-section JSX.
```
