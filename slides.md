---
theme: hccs
title: NJ Crash Data
info: NJBWC SAFE webinar — Ryan Williams, Hudson County Complete Streets, 5/14/26
selectable: true
colorSchema: dark
mdc: true
drawings:
  persist: false
footer:
  url: safe26.hccs.dev
  urlHref: https://safe26.hccs.dev
  logoHref: https://hudcostreets.org
qr:
  position: br
  size: 72
  uppercase: true
seoMeta:
  ogTitle: "NJ Crash Data"
  ogDescription: "Access, Analysis & Application — NJBWC SAFE webinar, 5/14/26"
  ogImage: https://safe26.hccs.dev/og.jpg
  ogUrl: https://safe26.hccs.dev
publish:
  baseUrl: https://safe26.hccs.dev
  canonicalForm: n
layout: cover
---

# NJ Crash Data

Ryan Williams · Hudson County Complete Streets

[NJBWC SAFE webinar](https://njbwc.org/safe/) · May 14, 2026

[safe26.hccs.dev](https://safe26.hccs.dev) · [crashes.hudcostreets.org](https://crashes.hudcostreets.org)

---
class: hccs-intro
dragPos:
  bp: 580,75,175,125
  blr: 580,210,175,125
  bb: 580,345,175,125
  vz: 770,75,175,125
  vd: 770,210,175,125
---

<style>
.slidev-layout.hccs-intro {
  padding-top: 1.2rem;
  padding-left: 2rem;
  h1 { font-size: 1.9rem; margin-bottom: 0.3rem; }
  blockquote { width: 55%; font-size: 0.9rem; }
  .body {
    width: 56%;
    font-size: 0.9rem;
    li { line-height: 1.5rem; }
  }
  .tile a {
    display: block; width: 100%; height: 100%;
    text-decoration: none !important; border: none !important;
  }
  .tile img {
    width: 100%; height: 100%; object-fit: contain;
    background: white; border-radius: 4px; padding: 4px;
  }
}
</style>

# Hudson County Complete Streets

> Our mission is to improve mobility in Hudson County by advocating for **safe streets**, pedestrian and cycling **infrastructure**, and **access to transit.**

<div class="body">

500+ volunteers · 8K newsletter · 10-member board · 2 part-time staff

Major campaigns:
- [Better PATH][PATH] — 7,000+ signatures, [Nov '25 win][path-win]
- [Better Light Rail][HBLR] · [Better Buses][BB] – launching 2026
- [Turnpike Trap][TT] — 1 bridge compromise [(Mar '26)][tt-win], -$4B
- [Vision Zero][HC VZ] — Hudson County Safety Action Plan
- [14th St Viaduct][Viaduct] — [HC announced major reconstruction May '25!][vd-hc]

Plus [JFK Blvd East][JFK Blvd East], + more → [hudcostreets.org][hudcostreets.org]

**Me:** SWE at [Open Athena][OA], moonlight as transpo advocate

</div>

<div v-drag="'bp'" class="tile"><a href="https://hudcostreets.org/panynj" target="_blank"><img src="/better-path-logo.png"/></a></div>
<div v-drag="'blr'" class="tile"><a href="https://hudcostreets.org/hblr" target="_blank"><img src="/better-light-rail-logo.png"/></a></div>
<div v-drag="'bb'" class="tile"><a href="https://hudcostreets.org/better-buses" target="_blank"><img src="/better-buses-hero.webp"/></a></div>
<div v-drag="'vz'" class="tile"><a href="https://www.hcnj.us/visionzero/" target="_blank"><img src="/vision-zero-logo.webp"/></a></div>
<div v-drag="'vd'" class="tile"><a href="https://www.hcnj.us/blog/2025/05/22/15886/" target="_blank"><img src="/vd-pr.png"/></a></div>

[OA]: https://www.openathena.ai/
[PATH]: https://hudcostreets.org/panynj
[HBLR]: https://hudcostreets.org/hblr
[BB]: https://hudcostreets.org/better-buses
[TT]: https://turnpiketrap.org/
[VZ]: https://hudcostreets.org/vision-zero
[HC VZ]: https://www.hcnj.us/visionzero/
[Viaduct]: https://hudcostreets.org/viaduct
[vd-hc]: https://www.hcnj.us/blog/2025/05/22/15886/
[JFK Blvd East]: https://hudcostreets.org/jfkblvdeastredesign
[path-win]: https://hudcostreets.org/news/press-release-path-win
[tt-win]: https://hudcostreets.org/news/praiseforturnpikeextensionrepairplan
[hudcostreets.org]: https://hudcostreets.org/

---
layout: section
---

# Why crash data matters

Big picture: economic, public-health, transportation disasters

---
class: counters
---

<style>
.slidev-layout.counters {
  padding: 1.2rem 2rem 0.6rem;
  h1 { font-size: 1.5rem; margin-bottom: 0.4rem; }
  .grid {
    display: grid;
    grid-template-columns: 1.7fr 1fr;
    gap: 0.8rem 1.6rem;
    margin-top: 0.6rem;
    align-items: start;
  }
  .col.big {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
  .col.small {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 0.45rem 0.8rem;
    align-items: start;
  }
  .col.small .ksi-head {
    grid-column: 1 / -1;
    font-size: 0.7rem;
    font-weight: 600;
    opacity: 0.85;
    margin-top: 0.15rem;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    border-bottom: 1px dashed rgba(255,255,255,0.25);
    padding-bottom: 0.1rem;
  }
  .footnote {
    margin-top: 0.7rem;
    font-size: 0.6rem;
    opacity: 0.6;
    text-align: center;
    line-height: 1.45;
  }
  .footnote a { color: inherit; }
}
</style>

# New Jersey, 2026 — year to date

<div class="grid">

<div class="col big">
  <TickingCounter
    :per-year="79_000_000_000"
    prefix="$"
    label="Spent on car ownership in NJ"
    rate-label="≈ 6.6M vehicles × $12K/yr (AAA)"
    size="md"
  />
  <TickingCounter
    :per-year="3_440_000_000"
    label="Gallons of gasoline burned in NJ"
    rate-label="≈ 109 gal/sec · 3.44B gal/yr"
    size="md"
  />
  <TickingCounter
    :per-year="1_790_000_000"
    start="2026-01-01"
    :start-value="46_900_000_000"
    prefix="$"
    label="Auto loan debt"
    rate-label="NJ share (2.79%) of US $1.68T total"
    size="md"
  />
</div>

<div class="col small">
  <TickingCounter
    :per-year="280_000"
    label="Crashes reported"
    rate-label="≈ 1 every 2 min"
    size="sm"
  />
  <TickingCounter
    :per-year="85_000"
    label="Vehicles totaled"
    rate-label="≈ 30% of crashes"
    size="sm"
  />

  <div class="ksi-head">People hurt or killed</div>

  <TickingCounter
    :per-year="584"
    start="2026-05-14"
    :start-value="177"
    label="Killed"
    rate-label="proj. 584 EoY · 177 YTD"
    size="sm"
    color="#f3a712"
  />
  <TickingCounter
    :per-year="3_150"
    label="Serious injury"
    rate-label="≈ 3,150 / yr (NJDOT)"
    size="sm"
    color="#f3a712"
  />
  <TickingCounter
    :per-year="12_000"
    label="Moderate"
    rate-label="non-incapacitating"
    size="sm"
  />
  <TickingCounter
    :per-year="25_000"
    label="Minor / other"
    rate-label="possible injury"
    size="sm"
  />
</div>

</div>

<div class="footnote">
Sources: <a href="https://www.aaa.com/autorepair/articles/breaking-down-the-cost-of-car-ownership">AAA</a> · <a href="https://www.nj.com/business/2026/02/the-real-reason-your-nj-gas-costs-keep-changing-its-not-just-the-price-per-gallon.html?gift=b6bf3872-a3b9-4237-b2c9-c24b308fa9c7">NJ.com / API (gas)</a> · <a href="https://fortune.com/2026/05/07/americans-auto-loan-debt-crisis/">Fortune (auto debt)</a> · <a href="https://www.nj.gov/njsp/info/fatalacc/">NJSP</a> · <a href="https://www.nj.gov/transportation/refdata/accident/">NJDOT</a> · <a href="https://crashes.hudcostreets.org">crashes.hudcostreets.org</a>
</div>

<!--
SPEAKER NOTES — running counters
- The $ counter ticks up by ~$2,500/sec.
- Gasoline ticks visibly — ~109 gal/sec.
- KSI counter ticks ~once every 2.3 hours, but the per-year framing is what's visceral.
- Reframe: this is roughly 5x the deaths from homicides in NJ, but gets a fraction of the coverage.
- Spinach/recall analogy: 1 person sick → nationwide recall. 600 traffic deaths per year → "another tragedy."
-->

---
class: efficiency
# Skip OG-shell generation: external iframe (hbt.hccs.dev) keeps the page's
# `load` event waiting longer than the shell-gen timeout. Per-slide social
# preview for this one slide isn't worth the build flake; deck-level OG
# (seoMeta above) covers the canonical share case.
skipOg: true
# Disable adjacent-slide preloading — Slidev preloads current ± 1, so without
# this, slides 4 + 6 would also mount this slide's iframe and never fire
# `load`, hanging OG generation for them too.
preload: false
---

<style>
.slidev-layout.efficiency {
  padding: 1.1rem 1.5rem 0.6rem;
  h1 { font-size: 1.4rem; margin-bottom: 0.2rem; }
  .lede {
    font-size: 0.85rem;
    opacity: 0.92;
    margin-bottom: 0.5rem;
  }
  .panes {
    display: grid;
    /* HBT plot is wide; video is wide-but-shorter — give the plot more
     * horizontal room and let the video letterbox within its narrower pane. */
    grid-template-columns: 1.6fr 1fr;
    gap: 0.8rem;
    height: calc(100% - 4.5rem);
  }
  .pane {
    background: rgba(0,0,0,0.15);
    border: 1px solid rgba(255,255,255,0.18);
    border-radius: 6px;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    position: relative;
    min-height: 0;
  }
  .pane .cap {
    font-size: 0.72rem;
    padding: 0.35rem 0.6rem;
    background: rgba(0,0,0,0.3);
    border-bottom: 1px solid rgba(255,255,255,0.12);
    display: flex;
    justify-content: space-between;
    align-items: center;
    line-height: 1.2;
    flex: 0 0 auto;
  }
  .pane .cap a { color: var(--hccs-accent); }
  .pane iframe {
    flex: 1 1 0;
    width: 100%;
    border: 0;
    background: black;
    min-height: 0;
  }
  .pane video {
    flex: 1 1 0;
    width: 100%;
    min-height: 0;
    border: 0;
    background: black;
    /* Letterbox inside the pane — never crop or overflow. */
    object-fit: contain;
  }
}
</style>

# Bus / Bike lanes and transit are higher capacity

<div class="lede">
Lincoln Tunnel XBL (1 bus lane) carries ≈ 5× the 4 car lanes combined · 2,000 bikes through one intersection in 5 min
</div>

<div class="panes">

<div class="pane">
  <div class="cap">
    <span><strong>Hudson River AM peak flows</strong> — NJ → NY, all modes</span>
    <a href="https://hbt.hccs.dev" target="_blank">hbt.hccs.dev</a>
  </div>
  <iframe v-if="$slidev.nav.currentSlideNo === $slidev.nav.currentRoute?.no" src="https://hbt.hccs.dev/?fs=1" loading="lazy"></iframe>
</div>

<div class="pane">
  <div class="cap">
    <span><strong>2,000 bikes in 5 minutes</strong>, 1-2 lanes</span>
    <a href="https://ht.hccs.dev" target="_blank">ht.hccs.dev</a>
  </div>
  <video src="/wt.mp4" controls preload="metadata" muted playsinline></video>
</div>

</div>

<!--
SPEAKER NOTES — mode efficiency
- Left: HBT (Hub Bound Travel) flow map — passengers per mode (PATH, NJT bus, ferry, Lincoln XBL, GWB, etc.) entering Manhattan's CBD in AM peak.
- Right: drone footage of bike commute — ~2,000 riders through one intersection in 5 min, vastly outperforming any car lane.
- The mode-efficiency story isn't theoretical; the data is already in the public record and the pictures are already on the ground.
-->

---
layout: section
---

# Demo: [crashes.hudcostreets.org](https://crashes.hudcostreets.org)

Public crash data + maps platform.

Daily fatalities · annual all-crashes · cleaned · queryable · open-source.

---
class: data-access
---

<style>
.slidev-layout.data-access {
  padding: 1.3rem 2rem 1rem;
  h1 { font-size: 1.5rem; margin-bottom: 0.4rem; }
  table {
    width: 100%;
    border-collapse: collapse;
    font-size: 0.82rem;
    margin-top: 0.4rem;
    th, td {
      text-align: left;
      padding: 0.4rem 0.6rem;
      border-bottom: 1px dashed rgba(255,255,255,0.2);
    }
    th { font-weight: 600; opacity: 0.85; }
    td.agency { font-weight: 600; }
    td.win { color: var(--hccs-accent); }
  }
  .leap {
    margin-top: 1rem;
    padding: 0.7rem 1rem;
    background: rgba(243, 167, 18, 0.15);
    border-left: 4px solid var(--hccs-accent);
    border-radius: 4px;
    font-size: 0.9rem;
    line-height: 1.5;
  }
}
</style>

# Crash data access — where we stand

<table>
  <thead><tr><th>Agency</th><th>Data</th><th>Frequency</th><th>Delay</th><th>Status</th></tr></thead>
  <tbody>
    <tr><td class="agency">NJSP</td><td>Fatal crashes</td><td>Daily</td><td>1d – 3mos</td><td>✅ Stable</td></tr>
    <tr><td class="agency">NJDOT</td><td>All crashes (NJTR-1)</td><td>Annually</td><td>2–3 yrs</td><td>📋 Manual cleanup</td></tr>
    <tr><td class="agency">AASHTOWare</td><td>All crashes</td><td>~Live</td><td>days–months</td><td class="win">🎉 NEW: '24 + '25</td></tr>
  </tbody>
</table>

<div class="leap">
<strong>The AASHTOWare portal is a major leap forward.</strong>
Years of data that historically took 2–3 yrs to publish are now available days-to-months after the fact.
Thanks Frank, Joe, and team at NJDOT / DHTS.
</div>

<!--
SPEAKER NOTES
- Frame this positively — they're in the audience.
- Mention: still gaps (PDF/photo attachments, geocoding quality), but the trajectory is great.
- Open ask: more historical depth + bulk export.
-->

---
class: open-data
dragPos:
  gh: 540,90,440,260
  pc: 540,360,440,200
---

<style>
.slidev-layout.open-data {
  padding: 1.3rem 2rem 1rem;
  h1 { font-size: 1.5rem; margin-bottom: 0.3rem; }
  .body {
    width: 48%;
    font-size: 0.85rem;
    li { line-height: 1.55; margin: 0.15rem 0; }
    p { margin: 0.5rem 0; }
  }
  img {
    width: 100%; height: 100%; object-fit: contain;
    border-radius: 4px;
    border: 1px solid rgba(255,255,255,0.15);
  }
}
</style>

# Open data + agentic civic SWE

<div class="body">

**Everything is open:**
- Code on GitHub ([hudcostreets/*](https://github.com/hudcostreets))
- Cleaned data in public S3 buckets
- Daily refresh via GitHub Actions
- Multiple mirror sites (crashes, path, hbt, ht, ctbk)

**Agentic coding has changed the equation:**
- 1 dev + Claude Code ≈ team of 5
- HCCS Slack has 10–20 SWEs ready to pitch in
- e.g. [reportjerseycity.com](https://reportjerseycity.com)

**The ask:**
- Publish raw data → enable citizen science
- Agencies + advocates building together >
  agencies building portals alone

</div>

<div v-drag="'gh'"><img src="/agentic-gh-commits.png"/></div>

[//]: # (<div v-drag="'pc'"><img src="/agentic-personal-commits.png"/></div>)

<!--
SPEAKER NOTES
- Top chart: Claude Code GitHub commits over time — 135K/day, ~4% of all public GH.
- Bottom chart: my own commits — orange (Claude-co-authored) explodes since July '25.
- This is why a 1-person volunteer org can ship a data platform that NJDOT spent years building.
-->

---
class: applications
---

<style>
.slidev-layout.applications {
  padding: 1.3rem 2rem 1rem;
  h1 { font-size: 1.5rem; margin-bottom: 0.4rem; }
  .cols {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1.2rem;
    font-size: 0.85rem;
  }
  h3 {
    font-size: 1rem;
    margin: 0 0 0.4rem;
    color: var(--hccs-accent);
  }
  ul { margin: 0; padding-left: 1.2rem; li { line-height: 1.6; } }
  .honest {
    margin-top: 1rem;
    font-size: 0.85rem;
    font-style: italic;
    opacity: 0.85;
    text-align: center;
    line-height: 1.5;
  }
}
</style>

# Applications — early innings, big potential

<div class="cols">
<div>

### To date
- HCCS helped HC launch its Vision Zero campaign + Safety Action Plan
- JC + HOB also running active VZ programs
- **HIN** (High-Injury Network) analyses inform paving / signal priorities
- Crash maps shown at council meetings, with electeds, in newsletters

</div>
<div>

### What's next
- **Real-time data → real-time response.** When AASHTO data lands days after a crash, advocates can show up at the next council meeting.
- **Anecdata → data.** Right now interventions often follow *one* tragic crash. Goal: spot patterns before tragedy.
- **Predictive / preventative.** Routine corridor scoring; safety system planning.
- **Public-facing dashboards** for every NJ muni.

</div>
</div>

---
layout: section
class: thanks
---

# Thanks

[crashes.hudcostreets.org](https://crashes.hudcostreets.org)

[ryanw@hudcostreets.org] · [hudcostreets.org](https://hudcostreets.org) · [@hudcostreets](https://instagram.com/hudcostreets)

Slides + source: [safe26.hccs.dev](https://safe26.hccs.dev)

[ryanw@hudcostreets.org]: mailto:ryanw@hudcostreets.org