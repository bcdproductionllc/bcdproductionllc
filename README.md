# GitHub setup — what to do with this package

Ordered by impact. Step 1 alone changes more than everything else combined.

> **Correction from the first version of this file.** I originally wrote a step
> telling you to fix fleetgpu.com by uploading files to the `fleetgpu.github.io`
> repo. That was wrong — **fleetgpu.com is served by a Cloudflare Worker, not
> GitHub Pages.** Files pushed to that repo do not reach the live site. See
> step 3 for what's actually true.

---

## 1. Profile README (30 minutes, biggest single win)

Right now `github.com/bcdproductionllc` shows an account with no description and no README. Anyone who looks you up sees nothing.

1. Create a **new public repository** named exactly **`bcdproductionllc`** — same as your username. GitHub will show a note confirming it's a special repo.
2. Check **"Add a README file"**.
3. Replace its contents with **`PROFILE-README.md`** from this package.
4. **Read the comment block at the top first** — it lists five things I inferred rather than verified. Fix or delete each one, then delete the comment block.
5. Commit.

It now renders at the top of your profile.

---

## 2. Fleet GPU case-study repo (the one you pin)

This is what a hiring manager actually opens. It's documentation, not source — clearly labeled as such.

1. Create a **new public repository** named **`fleet-gpu`**.
2. Upload the contents of **`fleet-gpu-repo/`**:
   - `README.md`
   - `docs/img/dashboard.png`
   - `docs/img/widget.png`
   - `docs/img/statistics.png`
   - `docs/img/icon.png`

   Keep the `docs/img/` folder structure — the README references those paths. In the GitHub web uploader you can drag the whole `docs` folder in at once.
3. **Work through the `[CONFIRM]` and `[FILL]` markers in the README.** The "Engineering notes" section is the part that gets you interviews, and two subsections there need details only you have: your backend stack and your persistence/concurrency choices. Everything else I wrote from your published material.
4. Set the repo **description** and **topics** (see the table in step 4).
5. Pin it to your profile: profile → **Customize your pins** → select `fleet-gpu`.

---

## 3. fleetgpu.com — optional, and it does not go through GitHub

**How the site is actually served:** a Cloudflare Worker named `fleetgpu`, serving static assets, bound to the custom domain `fleetgpu.com`. Last deployed manually from the Cloudflare dashboard.

**The `fleetgpu.github.io` repo is not connected to it.** That repo holds an older copy of the site and currently serves nothing — its `CNAME` claims `fleetgpu.com`, but DNS points at Cloudflare, so GitHub Pages never answers. You've chosen to leave it as-is; nothing in this package touches it.

**If you want to update the live site**, the `site-fixes/` folder holds a rewritten landing page — restyled to match bcdproduction.com, with the earnings features added and the contact address masked in JavaScript so it isn't scrapeable.

Treat it as an **optional redesign, not a repair.** The live page is in better shape than I first reported: it already has the correct App Store link and renders emoji correctly. I have not verified whether its images load — check that yourself before deciding this is worth doing.

To deploy it, either:

- **Cloudflare dashboard** → Workers & Pages → `fleetgpu` → **New deployment** → upload the contents of `site-fixes/` (this matches how it was deployed before), or
- **Wrangler CLI** → `wrangler deploy` from a local folder containing those files.

Either way you'll also want `privacy.html` and `terms.html` in the upload, since they're part of the current site and are linked from your App Store listing. Grab the live copies first so you don't lose them.

---

## 4. Repo READMEs and metadata

Add **`bcdproduction.github.io-README.md`** as `README.md` in the `bcdproduction.github.io` repo. (That one *is* GitHub Pages — it genuinely serves bcdproduction.com.)

Then set a description and topics on each repo — click the **⚙ gear** next to "About" on the repo homepage. Empty "About" boxes are what make an account look abandoned.

| Repo | Description | Website | Topics |
|---|---|---|---|
| `fleet-gpu` | `Engineering case study — iOS app for real-time Vast.ai GPU fleet monitoring and earnings tracking. Built with Swift and SwiftUI.` | `https://fleetgpu.com` | `ios` `swift` `swiftui` `widgetkit` `case-study` `gpu-monitoring` `vast-ai` |
| `bcdproduction.github.io` | `Studio site for BCDPRODUCTION — independent iOS app development.` | `https://www.bcdproduction.com` | `github-pages` `static-site` `portfolio` `ios` |
| `fleetgpu.github.io` | *Leaving as-is for now. If you later want it tidy, archiving it is one click in Settings and costs nothing.* | — | — |

---

## 5. Profile settings

Profile → **Edit profile**:

- **Name** — your actual name, not the LLC. Recruiters search for people.
- **Bio** — `iOS engineer · Swift & SwiftUI · 4 apps on the App Store · 15+ yrs controls engineering`
- **Website** — `https://www.bcdproduction.com`
- **Location** — fill it in; a lot of recruiter filtering is geographic.

---

## Honest expectations

A few things worth knowing before you spend a weekend on this:

**GitHub Pages sites don't help you get hired.** Nobody finds a candidate through a marketing site's repo. What gets read is your profile README and any pinned repo with a substantial write-up. That's why the ordering above puts the profile first and the site work last and optional.

**A docs-only repo is a real pattern, but it has a ceiling.** "Closed source, here's the architecture" is completely legitimate for commercial apps and many senior engineers present exactly this way. It demonstrates that you can reason and communicate. It cannot demonstrate that you write clean code. If you want that too, the highest-value addition later is one small genuinely open-source repo — a Swift package you factored out of one of your apps, for example. That's a bigger project than this package and worth doing separately.

**The `[FILL]` sections are not optional.** A case study that only describes features reads like marketing. The parts that make an engineer want to talk to you are the constraint-and-tradeoff paragraphs, and two of those need your backend and persistence details. If you skip them, you get a nice-looking page that says less than your App Store listing.

**Your account is an LLC, not a person.** `bcdproductionllc` is right for the apps and fine for a studio. For a job search, a personal account under your own name usually lands better — you can keep both and cross-link. Your call; I left the package usable either way.

**One deployment path worth considering later.** Connecting a repo to Cloudflare Workers Builds so pushes deploy fleetgpu.com automatically would give you a real source-of-truth repo *and* visible CI/CD — both of which read well for iOS/software roles. You've deferred it, which is reasonable; it's a change to a live site and not urgent. Worth revisiting once the profile and case study are up.
