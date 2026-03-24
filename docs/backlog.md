# Backlog

Items that are planned, need owner input, or warrant future exploration.

---

## Needs Owner Input Before Implementation

**HOA dues payment link**
The "Pay HOA Dues" button on the home page links to `#`. Swap the `href` in `content/_index.md` once the payment processor URL is known.

**TikTok social link**
The footer social link is ready to add. Needs the HOA's TikTok account URL. When available, add to `hugo.toml` under `params.ananke.social`.

---

## Future Features

### Resident Directory — Magic Link Access

**Problem:** The resident directory currently lives in a Google Sheet managed by the board. There's no way to share it with residents that's both private and low-friction (no passwords).

**Proposed solution:** A Cloudflare Worker-based magic link system.

**User flow:**
1. Resident visits `/directory/` on the site
2. No valid session → form asks for their email (and optionally street address for verification)
3. Worker generates a one-time token, stores it in Cloudflare KV (15-min TTL), sends a magic link via email
4. Resident clicks the link → token is validated and deleted, a signed session cookie is set (7-day expiry)
5. Directory page renders — Worker fetches the Google Sheet (published as CSV) and returns formatted data

**Architecture:**

| Piece | Tool | Notes |
|---|---|---|
| Token storage | Cloudflare KV | TTL-based, free tier |
| Email delivery | MailChannels (native to CF Workers) | No third-party API keys needed |
| Session auth | HMAC-signed HttpOnly cookie | Secret stored as Worker env var |
| Directory data | Google Sheet → published CSV | Sheet stays private; only the Worker touches it |
| Backend | Cloudflare Worker (~150–200 lines) | Three endpoints: request, verify, directory |

**Worker endpoints:**
- `POST /api/request-link` — accepts email, generates token, writes to KV, sends magic link
- `GET /api/verify?token=…` — validates token, deletes it, sets session cookie, redirects
- `GET /api/directory` — validates cookie, fetches + returns Sheet data

**Access control options (pick one):**
- No restriction — anyone with an email can request (relies on URL obscurity)
- Address verification — form requires email + street address, Worker checks against a known list
- Board-managed allowlist — board maintains resident emails in KV; outsiders get rejected

Address verification is the recommended sweet spot — low friction for residents, meaningful barrier for outsiders, no access list to maintain.

**Dependencies before starting:**
- Decide on access control approach
- Ensure Google Sheet is structured consistently (column headers matter for parsing)
- Cloudflare Workers enabled on the Pages project

---

### Volunteer Coordination

**Problem:** Interest in volunteering doesn't convert to action. People "like" posts or say yes informally but there's no clear intake path.

**Proposed solution:** A `/volunteer/` page listing open roles, each linking to a Google Form (one form with a role selector, or one per role). Low friction, no backend needed.

**Consideration:** Someone on the board must own keeping the roles list current. A stale volunteer page is worse than none.

---

### Events Upgrade — Google Calendar + Luma

**Problem:** Events are currently static markdown pages. Adding or updating an event requires a code change.

**Proposed solution:**
- Embed a **Google Calendar** (managed via `pvhoaroswell@gmail.com`) for a live calendar view residents can subscribe to
- Use **[Luma](https://lu.ma)** for individual event RSVPs instead of SignUpGenius — cleaner UX, board gets a dashboard, still free

Both are managed entirely outside the codebase. Re-evaluate when event volume grows or the board wants a more polished experience.

---

### Contractor / Service Provider Directory

A curated list of trusted local contractors and service providers recommended by neighbors. Could be a simple markdown page maintained by the board, or a Google Sheet embedded as a public view. Worth building once there's enough content to populate it meaningfully.
