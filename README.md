[MAXIMUM-landing-spec.md](https://github.com/user-attachments/files/35246967/MAXIMUM-landing-spec.md)
# maximum
maximum
[Uploading MAXIMUM-landing-spec.md…]()
# MAXIMUM — Landing Page Spec

A single-screen landing page for MAXIMUM, a company that manages turnkey sedation and anesthesia for dental clinics. On desktop the page fits in one viewport (100vh) and does not scroll.

Reference mockups: `MAXIMUM Landing.dc.html`. 3a and 3b are the base desktop and mobile designs. 4a is 3a with a gradient background, and 4b is 3a with a gradient on the navigation bar only.

---

## Content

**Navigation:** Trust · Services · Patient Benefit · Company

**Headline**
> We manage turnkey <u>sedation</u> and <u>anesthesia</u> for leading dental clinics across Canada.

Only "sedation" and "anesthesia" are underlined. "and" is not.

**Buttons**
- For Doctors
- For Dental Clinics

**Logo strip label:** Partner clinics

**Footer:** © 2026 Maximum Dental Corporation

---

## Design tokens

| Token | Value |
|---|---|
| Background | `#111111` |
| Primary text | `#FFFFFF` |
| Secondary text | `#8E8E88` (≈ 6:1 on #111) |
| Hairline | `rgba(237,237,232,0.12)` |
| Button border | `0.5px solid rgba(237,237,232,0.45)` |
| Font | DM Sans (Google Fonts), weights 400 / 500 / 700 |
| Corner radius (buttons) | `2px` |

DM Sans stands in for Styrene B, the font Anthropic uses, which requires a paid licence. If MAXIMUM buys a Styrene licence, swap the font family and keep every other value the same.

### Background variant (4a)
```css
background:
  repeating-linear-gradient(180deg, rgba(237,237,232,.022) 0 1px, transparent 1px 4px),
  linear-gradient(180deg, #2B2B2A 0%, #1C1C1C 28%, #111 60%, #0A0A0A 100%);
```
The background is grey at the top and fades to black, with faint scanlines. Buttons use a `transparent` background in this variant.

### Navigation-only variant (4b)
```css
background: linear-gradient(180deg, #3B3B3A 0%, #222221 45%, #111 100%);
box-shadow: inset 0 1px 0 rgba(237,237,232,.12);
```

---

## Layout — desktop (designed at 1440 × 900)

Column, full viewport height. Horizontal padding `64px`.

1. **Top bar**: 76px tall, with a 1px hairline below.
   - Left: logo image (`assets/maximum-logo-white.png`), 26px tall.
   - Right: nav links, 14px, white, 28px gap.
2. **Hero**: fills the remaining space, with content vertically centred and left-aligned to the logo.
   - Headline: 52px, weight 500, line-height 1.08, letter-spacing −0.03em, max-width 820px, `text-wrap: balance`.
   - Underline: 1px thick, offset 0.14em, colour `rgba(237,237,232,.6)`.
   - Buttons: 40px below the headline, 10px apart. Each is 40px tall with 0 22px padding, 14px text, 0.01em letter-spacing, the button border above, and a 2px radius.
3. **Partner clinics strip**: padding 28px 64px.
   - Label: 13px, secondary grey, 18px below.
   - Infinite horizontal marquee of logo tiles 150 × 44px with a 64px gap. One loop takes 40s and runs linearly. The edges fade with `mask-image: linear-gradient(90deg, transparent, #000 12%, #000 88%, transparent)`.
4. **Footer**: 60px tall, with a 1px hairline above. 12px text in secondary grey.

## Layout — mobile (designed at 390 × 844)

Horizontal padding is `20px`. The page may scroll if the content doesn't fit.

- Top bar: 64px tall, with the logo 20px tall. The nav collapses into a menu icon (two 20px × 1px white lines, 44px tap target).
- Headline: 32px, weight 500, line-height 1.1.
- Buttons: side by side, each `flex: 1`, 44px tall.
- Logo strip: tiles 110 × 36px with a 32px gap, one loop every 30s. The label is 12px.
- Footer: 11px.

---

## Marquee implementation

```css
@keyframes mxMarquee { from { transform: translateX(0) } to { transform: translateX(-50%) } }
```
The track is `display:flex; width:max-content; animation: mxMarquee 40s linear infinite`. It contains two identical sets of logos, and the second set has `aria-hidden="true"` so screen readers skip it. Honour `prefers-reduced-motion` by pausing the animation.

---

## Assets

- `assets/maximum-logo-white.png`: white wordmark on a transparent background.
- Partner clinic logos: **to be supplied**. Use white or single-colour versions. Don't use placeholder or invented logos in production.

## To do

- Supply the real partner clinic logos.
- Set the link targets for Trust, Services, Patient Benefit and Company, and build those pages.
- Set the link targets for the For Doctors and For Dental Clinics buttons.
- Design the open state of the mobile menu.
- Optional: a subtle fade-in of the headline on page load.
