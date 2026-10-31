# MSSN UNILAG — Open Source

Open-source software built by and for the Muslim Students' Society of Nigeria,
University of Lagos branch.

This repository is an index, not code. Each project below lives in its own repository,
stands on its own, and can be cloned and run in about two minutes with no credentials,
no database and no onboarding from anyone.

---

## Why these projects exist

MSSN UNILAG already runs software for the society itself — membership, events,
attendance, camps, programmes, welfare. That software needs our data and our access,
which makes it a poor place for an outside contributor to start.

The projects here are the opposite. Each one solves a problem a Muslim student at
UNILAG actually has, each one works entirely on the student's own device, and none of
them touches a single byte of society data. That is what makes them safe to open up —
and it is also what makes them genuinely useful, because a prayer-time app that needs
a network is an app that fails in the lecture hall.

---

## The projects

### 🕌 [salat-campus](https://github.com/mssnunilag/salah) — prayer times and timetable conflicts

**The problem.** You register for courses in week one. Around week six you notice your
Tuesday lab runs 3pm–6pm, which is the whole of the 'Asr window. Nothing told you,
because nothing puts a timetable and a prayer schedule on the same screen.

Computes prayer times for UNILAG Akoka from solar astronomy — offline, no API key —
then reports which lectures leave no room for which prayer, and lists prayer spaces on
campus.

`Next.js` · `TypeScript` · `Tailwind` · 33 tests · **[10 drafted first issues](https://github.com/mssnunilag/salah/blob/main/ISSUES.md)**

> Good first contribution with no code: verify one campus prayer space and correct its
> entry. Every one is currently marked unverified.

---

### 📖 [hifz-trail](https://github.com/bytheitc/hifz) — Qur'an memorisation and revision

**The problem.** Memorising is the part people plan; revision is the part that decides
whether any of it lasts. Portions are lost quietly, because nothing ever said they
were due.

A revision scheduler built for hifz rather than flashcards: three grades, a lapse
returns a portion to a one-day interval, and the day's queue comes back in Qur'anic
order rather than most-overdue-first. Progress is counted in distinct ayahs, so it can
never exceed 100%.

`Next.js` · `TypeScript` · `Tailwind` · 47 tests · **[10 drafted first issues](https://github.com/bytheitc/hifz/blob/main/ISSUES.md)**

> Good first contribution: add the 30 juz boundaries. Everyone thinks in juz and the
> app cannot express them.

---

### 🍲 [halal-bites-unilag](https://github.com/mssnunilag/halal) — halal food directory

**The problem.** Ask a new student where to eat and the answer is "ask around". The
information exists, scattered across WhatsApp groups and hostel corridors, and every
intake rediscovers it from nothing.

A directory for Akoka, Yaba, Bariga and on campus that never simply asserts food is
halal. Every entry records *how we know* — certified, Muslim-owned, community-reported
or unverified — and a claim above `unverified` without a note saying who checked
**fails the build**.

`Next.js` · `TypeScript` · `Tailwind` · 25 tests · **[10 drafted first issues](https://github.com/mssnunilag/halal/blob/main/ISSUES.md)**

> The most accessible project here. Most pull requests are data, and `pnpm validate`
> checks them for you before CI does.

---

### 💰 [zakat-kit](https://github.com/bytheitc/zakat) — zakat calculator and allowance planner

**The problem.** Students assume zakat is not their concern, right up until someone is
holding a term's saved fees for eight months. Finding out otherwise means four lookups
and some arithmetic — just enough friction that the question goes unasked.

Works out zakat on wealth with the full working shown, Zakat al-Fitr by measure and by
price, and splits a monthly allowance with sadaqah and savings taken out *first*.

`Next.js` · `TypeScript` · `Tailwind` · 27 tests · **[10 drafted first issues](https://github.com/bytheitc/zakat/blob/main/ISSUES.md)**

> Where scholars differ, this app offers an option and names it. It never decides.

---

## Design

All four apps share one design system — seven colour roles, one type scale, one
spacing scale — re-themed four times. Only the brand hue and the status colours
differ, because each app is saying something different with them.

- **[Design canvas](https://claude.ai/artifact/LE1NYGAzMg2Ndz6Cod75V9)** — the roles, the status colours and what each means, the
  scales, the component vocabulary, and every screen at phone width. *(Private until
  shared.)*
- **[`design/mssn-oss.tokens.json`](./design/mssn-oss.tokens.json)** — the same values
  in W3C Design Tokens format, importable into Figma via Tokens Studio. See
  [`design/README.md`](./design/README.md).

Every token was extracted from the apps as built, not invented for the file. Change
one and you change it in that project's `app/globals.css` too — or the file starts
lying.

A **dark palette** beyond the page background does not exist yet, and is a genuinely
useful design contribution.

## Starting out

Pick one and clone it:

```bash
git clone https://github.com/mssnunilag/salah.git
```

```bash
git clone https://github.com/bytheitc/hifz.git
```

```bash
git clone https://github.com/mssnunilag/halal.git
```

```bash
git clone https://github.com/bytheitc/zakat.git
```

Every project then works the same way:

```bash
pnpm install
```

```bash
pnpm dev
```

If a project ever asks you for an API key, a `.env` file or a database connection,
that is a bug — please open an issue.

Then read that project's `ISSUES.md`. Each has ten drafted tasks marked 🟢 gentle,
🟡 straightforward or 🔴 needs thought, saying what to do and which files to touch.
Comment on the matching GitHub issue to claim one so two people do not do the same
work.

## What we care about in a contribution

**Comments explain why, not what.** This is the convention we care about most. A
comment saying `// increment the counter` is noise. A comment explaining that the
hour-angle sign is the easiest thing in the file to get backwards, and that an
inverted one puts Fajr after sunrise, is worth more than the code it sits above.

**Logic is pure and tested.** Everything in each project's `lib/` is a pure function
over plain data, which is why it can be tested without a browser. React state stays in
`app/` and `components/`.

**TypeScript, strict. No `any`.**

**Test names are sentences about behaviour.** `"counts overdue portions on the first
day rather than losing them"`, not `"test upcomingLoad"`. Three real bugs in these
projects were caught by running them rather than reading them; each has a test behind
it that explains the failure.

**Small and finished beats large and nearly-there.** A pull request correcting one
unverified entry is a real contribution and is treated as one.

## On religious content

Three of these projects touch matters people are obliged to get right. The rule across
all of them is the same: **where scholars differ, add an option and name the position
— never a default buried in a constant.** Calculation methods, the 'Asr shadow ratio,
the gold-versus-silver nisab, the lunar-versus-solar rate: each is a labelled choice.

A pull request that resolves one of these in code, however well-sourced, will be asked
to make it configurable instead. If you are unsure, open an issue rather than a pull
request — nobody will think less of you for asking.

## Hacktoberfest

These projects are offered for Hacktoberfest. They were chosen to be contributable:
self-contained, no production data, no secrets, and a spread of tasks from "correct a
line of JSON" to "design how we represent a mixed kitchen without misleading anyone".

Maintainers aim to review within a few days. If a pull request goes quiet, a polite
nudge on the issue is welcome.

## Licence

Every project here is [MIT](https://github.com/mssnunilag/salah/blob/main/LICENSE) licensed.

These are community projects, not official MSSN UNILAG products, and they use none of
the society's data or branding.
