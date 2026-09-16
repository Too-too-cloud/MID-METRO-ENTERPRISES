# Midmetro Enterprises — website and email setup

Three-page static site (Home, About, Contact) ready for GitHub Pages on **midmetroenterprises.online**.

Files:

| File | What it is |
|---|---|
| `index.html` | Home |
| `about.html` | About |
| `contact.html` | Contact, with quote-request form |
| `styles.css` | Shared styling for all three pages |
| `favicon.svg` | Browser tab icon |
| `CNAME` | Tells GitHub Pages your domain. Leave it exactly as is. |

---

## Part 1 — Put the site on GitHub Pages (about 10 minutes)

**1. Create the repository**

On GitHub, click **New repository**. Name it anything (e.g. `midmetro-site`). Set it to **Public** — GitHub Pages needs public on free accounts. Don't add a README, since you already have one.

**2. Upload the files**

On the new empty repo page, click **uploading an existing file**. Drag in all six files (not the folder — the files themselves, so they sit at the top level of the repo). Commit.

**3. Turn on Pages**

Repo → **Settings** → **Pages** → under *Build and deployment*, set Source to **Deploy from a branch**, branch **main**, folder **/ (root)**. Save.

Wait a minute, then check `https://YOUR-USERNAME.github.io/midmetro-site/` — the site should be live.

**4. Add your domain in GitHub**

Still in Settings → Pages → *Custom domain*, type:

```
midmetroenterprises.online
```

Save. It will say the DNS check is in progress. That's expected until you do Part 2.

---

## Part 2 — Point the domain at GitHub (in your registrar's DNS panel)

Log into wherever you bought `midmetroenterprises.online` and open its DNS / Advanced DNS page. Add these:

| Type | Host / Name | Value | Priority |
|---|---|---|---|
| A | `@` | `185.199.108.153` | — |
| A | `@` | `185.199.109.153` | — |
| A | `@` | `185.199.110.153` | — |
| A | `@` | `185.199.111.153` | — |
| CNAME | `www` | `YOUR-USERNAME.github.io` | — |

Replace `YOUR-USERNAME` with your actual GitHub username. Delete any existing A record on `@` that points somewhere else (registrars often add a parking page record).

DNS usually settles within 30 minutes but can take a few hours. Once it does, go back to GitHub → Settings → Pages and tick **Enforce HTTPS**. If the tickbox is greyed out, the certificate hasn't issued yet — check again in an hour.

---

## Part 3 — Private email on your domain (about 15 minutes)

This gives you `info@midmetroenterprises.online` and up to five other mailboxes, free, with no ads.

**Recommended: Zoho Mail, Forever Free plan.** Five users, 5 GB each, one custom domain. The catch is that the free tier is webmail and mobile app only — no Outlook or Apple Mail. If you want desktop mail clients, Zoho Mail Lite is around $1/user/month.

**Steps**

1. Go to `zoho.com/mail` → Sign up → choose the **business / existing domain** option, and pick the **Forever Free** plan (it's further down the pricing page, below the paid tiers).
2. Enter your domain as `midmetroenterprises.online` — no `www`.
3. Zoho gives you a **TXT record** to prove ownership. Add it in the same DNS panel you used in Part 2: Type `TXT`, Host `@`, Value = the string Zoho shows. Then click Verify in Zoho.
4. Create your first mailbox: `info`. That becomes `info@midmetroenterprises.online`, which is the address already used throughout the site.
5. **Add the MX records** Zoho gives you, Host `@`. They look like `mx.zoho.com` (priority 10), `mx2.zoho.com` (20), `mx3.zoho.com` (50) — **use the exact values from your Zoho panel**, because Zoho assigns a different data centre (`.com`, `.eu`, `.in`) depending on where you signed up. Getting this wrong is the single most common reason mail doesn't arrive.
6. **Add SPF and DKIM**, again copy-pasted from Zoho's setup wizard. These aren't optional any more — Gmail and Yahoo reject unauthenticated mail from domains without them, so skipping this step means your quotes land in spam.
7. Send yourself a test message both ways before you print the address on anything.

**Note on the A records:** MX records and A records don't conflict. Your website can live on GitHub while your mail lives at Zoho, on the same domain, at the same time.

---

## Things to change before you go live

- **Phone number** — `contact.html` has a placeholder `+254 700 000 000` in two places (the link and the visible text).
- **Business description** — the copy assumes general supplies and contracting. Rewrite the Home and About text to match what you actually do.
- **Hours and location** — currently Naivasha, Mon–Sat. Adjust in `contact.html`.
- **Contact form** — it currently opens the visitor's own email app with the message pre-filled. To get submissions delivered straight to your inbox instead, sign up free at formspree.io and follow the commented instructions inside `contact.html`.
