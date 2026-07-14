# Ember & Salt

A 3-page site (`index.html`, `menu.html`, `contact.html`) sharing one
stylesheet (`style.css`). Built from an existing HTML/CSS starting point,
using two reference screenshots — a bee/honeycomb "Beary's Breakfast Bar"
template and an "Asian Restaurant" hero layout — as structural inspiration
rather than a skin to copy directly.

## File structure

```
index.html      Home page — hero, testimonial, hours, location
menu.html       Menu page — category banners + item cards
contact.html    Contact page — staff cards
style.css       Single shared stylesheet for all three pages
```

All three HTML files load the same `style.css`. Keep all four files in
one folder — if `style.css` goes missing or lives elsewhere, every page
loses its styling, since nothing is inlined.

---

## Why the design departs from the reference screenshots

The references were a **honeycomb/bee bakery** and a **noodle restaurant**
template. Neither theme fits a restaurant called "Ember & Salt," so the
brief was treated as: *borrow the layout patterns and card techniques,
not the honey/bee visual language.* Concretely:

- Beary's thick-bordered **octagon card** → reinterpreted as a
  **faceted, cut-corner panel** (see "Signature shape" below) that reads
  as a charred edge or a cut salt crystal instead of a stop sign.
- Beary's bee mascots flanking headlines → a **flame icon** and a
  **cut-gem icon** flanking headlines, echoing the same "two small
  motifs bracket the title" idea with on-brand icons.
- The Asian Restaurant's **split hero** (text left, image right, CTA
  button, simple text nav) → kept as-is structurally; it's a strong,
  legible pattern independent of cuisine.
- Beary's **empty image placeholder boxes** on menu items → kept the
  same idea (a box you'll drop a real photo into later) but restyled it
  as a dashed-border box with a camera glyph and a "Photo" label, so it
  reads as an intentional placeholder rather than a missing image.

## Color palette

| Token    | Hex       | Used for                                   |
|----------|-----------|---------------------------------------------|
| `--char`  | `#1E1712` | Page background, footer — the "char" half of the brand |
| `--coal`  | `#2A211B` | Raised dark surfaces (e.g. the badge fill) |
| `--ember` | `#FF6A3D` | Primary flame accent — links, prices, CTA gradient |
| `--gold`  | `#E8A33D` | Secondary glow accent, paired with ember in gradients |
| `--salt`  | `#F3EDE2` | Content-section background — the "salt" half of the brand |
| `--paper` | `#FBF6EC` | Card fill on top of `--salt`, for subtle separation |
| `--ash`   | `#A79A8C` | Secondary/muted text on dark backgrounds |
| `--iron`  | `#4A423A` | Body text on light backgrounds, cookware neutral |

The site alternates between `--char` (hero, footer) and `--salt`
(content sections) on every page. This isn't just a stylistic stripe —
it's a direct, literal expression of the two words in the name: dark
sections are "ember," light sections are "salt." It also avoids the
generic "everything is near-black with one accent color" look by giving
the page real light/dark structure.

## Typography

| Role | Font | Why |
|---|---|---|
| Display (headlines) | **Fraunces** | A high-contrast serif with rustic, slightly irregular character — reads as crafted/artisan rather than corporate. |
| Body copy | **Work Sans** | Clean geometric sans, chosen purely for legibility against the display font's personality. |
| Labels, prices, hours, eyebrows | **Space Mono** | A monospace gives numbers and small-caps labels a "measured, precise" feel — ties into cooking times and salt measurements — and visually separates utility text from prose. |

The original CSS used **Sniglet**, a bubbly rounded font that suited
Beary's bakery-for-bears branding. It was dropped here because that
same bubbliness reads as playful/childlike, which works against an
elevated wood-fire restaurant. Fonts load from Google Fonts via a
`<link>` tag rather than the local `@font-face` file in the original
CSS, since the actual `.otf` file wasn't available — swap in a
self-hosted `@font-face` block if you'd rather not depend on Google's
CDN.

## Signature shape: the faceted panel

Every card, banner, and the CTA button on the site uses the same
technique: two nested elements with matching `clip-path: polygon(...)`
cut corners — an outer element with a gold-to-ember gradient fill acts
as a thin glowing border, and an inner element (`--paper` or `--coal`)
sits inset on top of it. This is a direct evolution of Beary's
thick-brown-border-on-octagon technique, but:

- the corners are cut at shallow angles rather than a full stop-sign
  octagon, so it reads as a "trimmed" or "charred" edge instead of a
  badge shape;
- the border is a thin glowing gradient line instead of a thick solid
  fill, matching the light/dark restraint of the rest of the palette;
- it's reused everywhere (nav underline, CTA button, menu item cards,
  category banners, staff cards, the page-title badge) so it functions
  as an actual signature rather than a one-off decoration.

## Hero illustration

The homepage hero uses an original inline SVG (skillet, seared food,
rising embers) instead of a stock photo or AI-generated image. This
sidesteps copyright questions entirely and keeps the art directly
on-palette. It went through one revision: the first pass used a solid
radial-gradient circle behind the pan that read as a glowing sphere/
planet rather than ambient heat — the gradient was softened and
elongated into an ellipse, and the food in the pan was redrawn as a
recognizable seared steak with grill marks plus a couple of vegetables,
so the illustration reads clearly at a glance.

## Page-by-page structure

**Home** (`index.html`) — split hero (copy + SVG art) inspired by the
Asian Restaurant reference, followed by three stacked faceted panels
(testimonial, hours, location) inspired by Beary's stacked card
layout.

**Menu** (`menu.html`) — a centered title badge (flame + gem icons
flanking "Menu," mirroring Beary's bee-flanked title), then repeating
category banners ("From the Fire," "Sides," "To Drink") each followed
by item cards. Every item card has name, description, price (in
Space Mono, ember-colored), and a placeholder photo box.

**Contact** (`contact.html`) — reuses the exact same hero pattern as
the Menu page (title badge + intro line) for visual consistency, then
one staff card per person (name, role, phone, email with small icon
glyphs), mirroring Beary's Mama/Papa/Baby Bear card format.

Reusing the hero markup/CSS between Menu and Contact was a deliberate
choice to keep the codebase small — one pattern, two headlines, instead
of two near-identical patterns.

## Navigation

Nav links and the homepage CTA were originally plain `<button>`
elements with no `href` — visually correct but functionally dead. They
were converted to real `<a href="...">` links across all three pages,
with `.is-active` marking the current page. The "View the Menu" button
on the homepage now links to `menu.html`.

## Accessibility notes

- Focus states: `:focus-visible` gets a visible ember-colored outline
  on interactive elements (nav links, CTA).
- Motion: the drifting-ember animation in the hero SVG is disabled
  under `prefers-reduced-motion: reduce`.
- Decorative SVGs (hero art, flame/gem icons, photo-placeholder icons)
  are marked `aria-hidden="true"` since they carry no information beyond
  what the surrounding text already says.

## Responsive behavior

- Hero (Home) collapses from a two-column split to a single column
  below `880px`, with the illustration moved above the copy.
- Menu item cards and staff cards stack vertically below `620px`,
  moving the photo placeholder underneath the text.
- The nav wraps to a second line below `520px`.

## Placeholder content — replace before launch

Everything below is invented for structure/demonstration and should be
swapped for real information:

- Menu categories, dish names, descriptions, and prices
- Testimonial quote and signature on the homepage
- Address (`212 Kiln Row, Ashport, Maine`) and parking note
- Staff names, roles, phone numbers, and email addresses
- General contact phone/email in the Contact page intro
- All photo-placeholder boxes on the Menu page