# Pine Valley HOA - Site Analysis & Planning Notes

Generated: 2026-03-24

---

## Existing Site (pinevalleyroswell.fyi)

The current site redirects to a single-page link hub hosted on a third-party service (me-page.org).
It is essentially a landing page with buttons linking out to external services — no native content
management, no multi-page structure.

---

## Functionality to Replicate

| Feature | Current Implementation | Recommendation |
|---|---|---|
| HOA Dues Payment | Button → external payment processor, $50/year | Prominent CTA button on home page |
| Directory Entry Form | Google Form: `https://docs.google.com/forms/d/1WJyLceXpmpj3I3vMLdW3jvh3DDVfZGrJUhsEYZaeNJ8/edit` | Keep Google Form, link from Community or Resources page |
| Event Signup | SignUpGenius per-event links | Link to SignUpGenius from a new Events section |
| News/Announcements | Single button, unclear destination | Already handled by `content/news/` |
| Facebook Group | `https://www.facebook.com/groups/1263262673794257` | Add to footer social links (Ananke supports natively) |
| Email Contact | pvhoaroswell@gmail.com | Add to Contact page (replace placeholder) |
| TikTok | Footer icon | Add to footer social links |

A new **Events** section (`content/events/`) would also be valuable — it's an obvious gap in
the current site.

---

## Media Assets

The existing site has **no reusable media assets** — it is third-party hosted with no original
images. All photos in `static/images/` on the new site are original assets:

- `neighborhood-sign.jpg` — primary featured image
- `neighborhood-sign-summer.jpg` — seasonal variant
- `neighborhood-sign-close.jpg` — close-up view
- `neighborhood-entrance.jpg` — entrance photo

The existing site establishes a **color palette** worth carrying forward in `custom.css`:

- Dark charcoal: `#101B1B`
- Forest green: `#1F4A42`
- Cream/light backgrounds
- White text on dark backgrounds

---

## Hugo / Ananke Theme Assessment

### What Ananke Does Well
- Clean multi-page layout with nav, featured images, and footer
- Native news/blog content type — already working
- Social links in footer via `hugo.toml` params
- Built-in `form-contact` shortcode (`layouts/shortcodes/form-contact.html`)
- Responsive, mobile-friendly out of the box
- Low maintenance overhead — good fit for a volunteer-run HOA

### Ananke Gaps / Limitations
- No events or calendar support — needs a custom page layout or external links (SignUpGenius)
- No payment widget — needs a raw HTML button/link in markdown or a custom shortcode
- Contact form requires a backend handler — Cloudflare Pages does not process forms natively.
  Options: Formspree, Netlify Forms (with adapter), or a Cloudflare Worker.
- Design is generic — the forest green/charcoal palette needs to be applied via `custom.css`

### Alternative Themes Considered

| Theme | Strengths | Trade-offs |
|---|---|---|
| **Ananke** (current) | Well-documented, simple, blog-ready | Generic look, limited layout flexibility |
| **PaperMod** | Very clean, fast, good for resource-heavy sites | More complex configuration |
| **Congo** | Modern card layout, strong community-site fit | Requires Go modules setup |
| **Hinode** | Bootstrap-based, rich component library | Heavier, more initial setup |

**Verdict**: Ananke is adequate for the core goal. The main additions needed are a payment button
shortcode and a working contact form backend. If a more polished community-hub look is desired,
**Congo** is worth evaluating — its card-based layouts suit an HOA site better than Ananke's
blog-centric design.

---

## Recommended Next Steps (Priority Order)

1. **Complete Contact page** — add real email address; integrate Formspree (or similar) for the contact form
2. **Add payment CTA** — home page button/shortcode linking to dues payment processor
3. **Add Events section** — simple markdown pages with SignUpGenius links per event
4. **Wire up social links** — Facebook group + email in `hugo.toml` footer params
5. **Apply color branding** — update `custom.css` with forest green palette from existing site
6. **Add Directory link** — on Resources or a new Community page

---

## Key External Links (from existing site)

- Facebook Group: https://www.facebook.com/groups/1263262673794257
- HOA Email: pvhoaroswell@gmail.com
- Directory Form: https://docs.google.com/forms/d/1WJyLceXpmpj3I3vMLdW3jvh3DDVfZGrJUhsEYZaeNJ8/edit
- Spring Fling 2026 Signup: https://www.signupgenius.com/go/904044EA4AD22A31-62785442-2026
  (April 25, 4:00 PM - 7:00 PM)
