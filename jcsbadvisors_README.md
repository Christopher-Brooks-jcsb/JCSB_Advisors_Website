# JCSB Wealth Management — Advisors Site (jcsbadvisors.com)

This repository contains all source files for **jcsbadvisors.com** — the business owner and 401(k) advisory landing page for JCSB Wealth Management, led by **Brent Turner, CFP®**.

This is one of three repositories under the `Christopher-Brooks-jcsb` GitHub account:

| Repository | What It Is | Published Via |
|------------|-----------|---------------|
| **This repo** — `jcsb-landing` | jcsbadvisors.com — business owner / 401(k) site | GitHub Pages |
| `jcsb-financial-landing` | jcsbwealth.com — personal wealth advisory site | GitHub Pages |
| `jcsb-form-backend` | Shared form backend server | Railway |

---

## What This Site Is

A single-page landing site targeting **business owners** — specifically those who sponsor or are considering a company 401(k) retirement plan. The site runs two parallel campaigns:

- **Plan Takeover** — Business owners with an existing plan that lacks active advisory support or documented fiduciary oversight
- **New Plan Setup** — Business owners considering their first retirement plan, using SECURE Act 2.0 tax credits and talent retention as the primary hooks

The site is designed to create recognition in the right reader, route them to the appropriate campaign, and convert them into a scheduled consultation — all while meeting FINRA and SEC marketing compliance standards. See `/brand-guides/05_JCSB_Compliant_Copy_Framework.md` for the full compliance copy approach.

---

## File Structure

```
/
├── index.html              # The entire website — content, layout, CSS, and JS in one file
├── JCSBWM_Logo.svg         # Horizontal logo (nav and footer)
├── favicon.png             # Browser tab icon
├── README.md               # This file
└── /brand-guides/          # Brand, design, copy, and compliance reference docs
    ├── 01_JCSB_Brand_Foundation.md
    ├── 02_JCSB_Print_Design_Guide.md
    ├── 03_JCSB_Web_Design_Guide.md
    ├── 04_JCSB_Campaign_Playbook.md
    └── 05_JCSB_Compliant_Copy_Framework.md
```

> **Note:** Brent's photo (`brent_turner.png`) is hosted externally at `https://jcsbwealth.com/brent_turner.png` and referenced directly — it does not need to be in this repo.

---

## How the Site Is Hosted

**Hosting:** GitHub Pages. This repo's `main` branch is published automatically. Any push to `main` updates jcsbadvisors.com within 2–4 minutes. No deployment step required.

**Domain:** Managed through Brent's domain registrar account. DNS points to GitHub Pages servers.

**Compliance status:** The `<meta name="robots" content="noindex, nofollow">` tag is present in `index.html` while the site awaits compliance approval. Remove it once approval is received — that is the only change needed to allow search engine indexing.

**Recommended future host (if transferring):** Netlify — free tier, faster CDN, easier rollback, same GitHub-connected auto-deploy workflow. The Railway backend does not need to change for a Netlify transfer.

---

## How the Contact Form Works

```
Visitor submits form on jcsbadvisors.com
              ↓
index.html sends HTTPS POST to Railway backend
(payload includes source: 'advisors')
              ↓
jcsb-form-backend (Railway)
              ↓                      ↓
Wealthbox contact created      SendGrid notification
with advisors-specific tags    email sent to Brent
+ follow-up task due tomorrow
```

**Backend repo:** `Christopher-Brooks-jcsb/jcsb-form-backend`
**Backend live URL:** `https://jcsb-form-backend-production.up.railway.app`
**Health check:** `GET /health` → `{"status":"ok","service":"jcsb-form-backend",...}`

### Source field

Every form submission from this site includes `source: 'advisors'` in the JSON payload. The backend uses this to apply advisors-specific tags, notes, task names, and email subjects — distinguishing these leads from those submitted via jcsbwealth.com.

| Field | Value sent from this site |
|-------|--------------------------|
| `source` | `advisors` |
| Wealthbox page tag | `JCSB Advisors 2026` |
| Wealthbox source tag | `Site - JCSB Advisors` |
| Notification email subject | `New Lead — JCSB Advisors — 401(k) Campaign Lead` |
| Wealthbox note source line | `JCSB Advisors (jcsbadvisors.com) — 401(k) Campaign` |

### Form situation values

The contact form dropdown sends one of three values, each mapping to a Wealthbox campaign tag:

| Dropdown option | `situation` value sent | Wealthbox tag applied |
|----------------|----------------------|-----------------------|
| We have an existing plan — interested in a review | `takeover` | `Campaign - Plan Takeover` |
| We are considering a new retirement plan | `new` | `Campaign - New Plan Setup` |
| Not sure yet — just exploring my options | `unsure` | `Campaign - Exploring` |

### Viewing leads in Wealthbox

- **All advisors site leads:** Filter contacts by tag `Site - JCSB Advisors`
- **Takeover leads only:** Filter by `Campaign - Plan Takeover`
- **New plan leads only:** Filter by `Campaign - New Plan Setup`

---

## Page Structure

The page is organized as a single scrolling layout with these sections in order:

1. **Hero** — Fiduciary responsibility framing + self-identification card (which situation are you in?)
2. **Campaigns** — Tabbed panel: Plan Takeover / New Plan Setup with illustrative situations for each
3. **Illustrative Situations** — Three scenario cards (existing plan, new plan, bundled/inherited plan) following the compliant Hook → Story → Offer structure
4. **Who This Serves** — Fit / not-fit block to help owners self-qualify
5. **Philosophy** — The 3(21) co-fiduciary approach: retained control, shared burden
6. **3(21) vs. 3(38) Comparison** — Structured table explaining the difference in plain business terms
7. **Annual Review Calendar** — Six cards showing what ongoing advisory actually includes each year
8. **Owner Bridge** — How the company plan connects to the owner's personal wealth picture
9. **Meet Brent** — Advisor bio, credentials, CFP® designation
10. **Process** — Four-step journey from first conversation to ongoing partnership
11. **Final CTA** — Three-option contact block (book / call / message) + contact form
12. **Footer** — Full regulatory disclosure, legal links, TOS/Privacy modals

---

## Making Changes

### Recommended: Claude + Claude Code

Connect Claude Code to this GitHub account. Claude reads the files in `/brand-guides/` automatically, so every change stays on-brand, on-voice, and compliance-aware.

1. Open a conversation at claude.ai (Claude Pro — $20/month or $100/month)
2. Describe the change: *"Update the phone number in the footer"* or *"Revise the new plan section copy"*
3. Claude reads the relevant files, makes the change, and pushes to `main`
4. GitHub Pages updates jcsbadvisors.com within 2–4 minutes

### Simple edits: GitHub web editor

1. Open `index.html` in this repository on github.com
2. Click the pencil icon to edit
3. Make your change and click **Commit changes → Commit directly to `main`**
4. Site updates in 2–4 minutes

### Local preview

```bash
git clone https://github.com/Christopher-Brooks-jcsb/jcsb-landing.git
cd jcsb-landing
# Open index.html directly in a browser — no build step needed
# Or use a local server:
npx serve .
```

No framework, no build process. The file works as plain HTML.

---

## The Brand Guide Folder

Read these before making any significant content or design changes. Claude reads them automatically when connected via Claude Code.

| File | What It Covers |
|------|---------------|
| `01_JCSB_Brand_Foundation.md` | Master reference — colors (hex values), typography, voice, vocabulary rules, service pillars. Load this first for every task. |
| `02_JCSB_Print_Design_Guide.md` | Layout and design rules for print and static documents. |
| `03_JCSB_Web_Design_Guide.md` | Layout rules for web — gradients, cards, animations, orange usage, CTA placement, section architecture. |
| `04_JCSB_Campaign_Playbook.md` | Messaging, copy direction, and CTAs for the business-owner (Plan Takeover and New Plan Setup) and personal wealth campaigns. This is the primary reference for advisors site content. |
| `05_JCSB_Compliant_Copy_Framework.md` | The compliance copy framework — recognition hooks, illustrative situations, friction-removal offers, second opinion framing, and the four-question compliance test. Required reading before writing any new copy. |

---

## Key Rules — Do Not Change Without Review

**Colors**
- Green: `#3E8E63` — growth, fiduciary partnership
- Blue-dark: `#2F3E46` — trust, authority, dark section backgrounds
- Orange: `#F38D0C` — signal color only; primary CTA button and urgency elements; never for general emphasis
- Full token table in `01_JCSB_Brand_Foundation.md` Part 5

**Orange usage on this site**
Orange is used for the nav CTA button, the form submit button, and the pain-point block left borders (takeover campaign). It is not used for general emphasis, decorative purposes, or body text. Its power comes from its rarity — overusing it breaks the signal.

**Typography**
- Headlines: Playfair Display always — never substituted
- Body copy: DM Sans at weight 300 always
- Eyebrow labels: DM Sans 700, all-caps, letter-spacing 2px

**Credential**
Always reference **Brent Turner, CFP®** on first mention in any section. The CFP® mark must not be omitted or abbreviated differently.

**Compliance copy**
- Never guarantee investment returns or outcomes
- Never use "fee-only" — use "primarily fee-based"
- Never assert a factual claim about the reader's plan or advisor without a factual basis
- Never imply the reader's existing advisor has failed or is inadequate
- All SECURE Act 2.0 credit figures must be labeled illustrative with a "consult a tax professional" note
- Run all new copy through the four-question compliance test in `05_JCSB_Compliant_Copy_Framework.md` before submitting for review

**noindex tag**
`<meta name="robots" content="noindex, nofollow">` is present on line 6 of `index.html`. Remove this line once compliance approves the site for publishing.

---

## Compliance Submission Checklist

Before sending to the compliance officer:

- [ ] All copy passes the four-question test in `05_JCSB_Compliant_Copy_Framework.md`
- [ ] No return guarantees or outcome promises anywhere on the page
- [ ] No "fee-only" — only "primarily fee-based"
- [ ] All SECURE Act 2.0 figures labeled illustrative with tax professional disclaimer
- [ ] Illustrative situation cards all have their disclaimer line
- [ ] 3(21) vs 3(38) table has its "not legal advice" note
- [ ] Full Kovack Securities / Kovack Advisors disclosure in footer
- [ ] FINRA BrokerCheck link present in footer
- [ ] Form CRS link present in footer
- [ ] CFP Board certification mark disclosure present in footer
- [ ] TOS and Privacy Policy modals complete and accurate for jcsbadvisors.com domain
- [ ] `noindex` tag still present (remove only after approval)
- [ ] Site tested as a standalone HTML file — all assets load from external URLs, no local file dependencies

---

## Scheduling Links

The "Book a Time" buttons link to Motion. If these URLs ever change, update them in `index.html`:

| Button | URL |
|--------|-----|
| In Person | `https://app.usemotion.com/meet/jcsbwm_brentcfp/inofficemeeting` |
| By Zoom | `https://app.usemotion.com/meet/jcsbwm_brentcfp/zoommeeting` |

---

## Environment Variables (Backend — managed in Railway)

These live in the `jcsb-form-backend` Railway service, not in this repo. Never commit API keys to GitHub.

| Variable | Purpose |
|----------|---------|
| `WEALTHBOX_API_TOKEN` | Authenticates to Wealthbox CRM |
| `SENDGRID_API_KEY` | Sends lead notification emails |
| `NOTIFICATION_EMAIL` | Address that receives new lead notifications |
| `ALLOWED_ORIGIN` | CORS — set to `*` for compliance review; lock to domain in production |
| `NODE_ENV` | `production` |

---

## Costs

| Service | Cost |
|---------|------|
| GitHub Pages (hosting) | Free |
| Domain — jcsbadvisors.com | ~$15–20/year (Brent's domain account) |
| Railway (shared form backend) | ~$5/month (shared with jcsbwealth.com) |
| SendGrid (email notifications) | Free tier |
| Claude Pro (for site editing) | $20–100/month if used |

---

## Related Repositories

| Repo | Purpose |
|------|---------|
| `Christopher-Brooks-jcsb/jcsb-financial-landing` | jcsbwealth.com — personal wealth advisory site |
| `Christopher-Brooks-jcsb/jcsb-form-backend` | Shared backend — form processing, Wealthbox, SendGrid |

---

## Contact

**Brent Turner, CFP®** — JCSB Wealth Management
(806) 677-9416 · brent@jcsbadvisors.com

Built by Christopher Brooks using Claude (Anthropic) and Claude Code.
