---
version: "1.0"
name: ""
description: ""

colors:
  background: ""
  foreground: ""
  primary: ""
  secondary: ""
  accent: ""
  muted: ""
  border: ""

typography:
  display:
    fontFamily: ""
    fontSize: ""
    fontWeight: ""
    lineHeight: ""
    letterSpacing: ""
  heading:
    fontFamily: ""
    fontSize: ""
    fontWeight: ""
    lineHeight: ""
  body:
    fontFamily: ""
    fontSize: "1rem"
    fontWeight: "400"
    lineHeight: "1.6"
  label:
    fontFamily: ""
    fontSize: ""
    fontWeight: ""
    letterSpacing: ""

rounded:
  sm: "4px"
  md: "8px"
  lg: "12px"
  xl: "16px"

spacing:
  xs: "8px"
  sm: "16px"
  md: "24px"
  lg: "32px"
  xl: "48px"
  2xl: "80px"

logo:
  location: "brand-assets/"
  primary: ""
  light: ""
  icon: ""

delivery:
  format: ""
  briefTime: ""
  deliverTo: ""
  sendFrom: ""
---

# [Client Name] — Design DNA

Single source of truth for all brand decisions. Follows the `@google/design.md` specification.

**Validate:** `npx @google/design.md lint references/DESIGN.md`
**Filled by:** /onboard — active brand extraction (website scrape, logo analysis, Q10 answers)
**Used by:** every skill that generates client-facing output

---

## Visual Style

**Aesthetic:** *(e.g. modern and clinical, warm and approachable, bold and energetic, minimal and editorial)*

**Photography:** *(e.g. real team/job photos, lifestyle, illustration, none yet)*

**Icons:** *(flat / outlined / filled / custom)*

**Spacing feel:** *(airy and minimal / balanced / tight and dense)*

---

## Brand Assets

- [ ] Logo — primary (SVG or PNG with transparent background) → `brand-assets/`
- [ ] Logo — light variant (for dark backgrounds) → `brand-assets/`
- [ ] Icon / standalone mark → `brand-assets/`
- [ ] Brand colors confirmed with hex codes
- [ ] Fonts confirmed and source identified
- [ ] Brand guidelines document (if exists)
- [ ] Business or service photos
- [ ] Owner or team headshot

---

## Named Rules

*(Brand-specific rules — things to always do, things to never do.)*
*(Examples: "always lead in Spanish for student-facing content" / "orange is accent only, never dominant")*

---

## Email Template

**Header background:** *(hex or "use primary")*
**CTA button color:** *(hex or "use accent")*
**Body font (email-safe):** *(e.g. Arial, sans-serif)*
**Signature format:** *(e.g. Name, Title, Phone, Website)*

---

## Sources

**Website scraped:** *(URL — date scraped)*
**Logo files analyzed:** *(filenames)*
**Reference sites:** *(URLs used for aesthetic direction)*
**Manual input:** *(any fields filled by interview rather than extraction)*

---

## Usage rule

Before generating any artifact that leaves this system — read the YAML frontmatter above. Apply colors, typography, logo paths, and delivery settings. Never ask the client for brand information mid-session. It is here.

`references/voice.md` handles tone and register. This file handles how it looks. Both required before any external-facing output.
