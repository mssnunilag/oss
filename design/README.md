# Design tokens

One token file covering all four MSSN UNILAG open-source projects, in the
[W3C Design Tokens](https://tr.designtokens.org/format/) format (`$value` / `$type`)
that Tokens Studio and the Figma variables importers read.

**[`mssn-oss.tokens.json`](./mssn-oss.tokens.json)**

**Design canvas** — [the system drawn out](https://claude.ai/artifact/LE1NYGAzMg2Ndz6Cod75V9): the seven roles across all four
themes, the status colours with what each one means, the type and spacing scales, the
shared component vocabulary, and each app's screen at phone width. Rebuild from it in
Figma, or hand it to a designer as the spec. *(Private until shared from the page's
Share menu.)*

## The idea

The four apps are not four palettes. They are **one skeleton re-themed four times**.

Every app defines the same seven roles, in the same order, for the same purposes:

| Role | Used for |
| --- | --- |
| `ink` | primary text |
| `inkSoft` | secondary text, hints, metadata |
| `parchment` | page background |
| `card` | raised surface — cards, panels |
| `rule` | borders and dividers |
| `brand` | primary action, progress fill, active tab |
| `brandSoft` | brand-tinted background — callouts, selected states |

On top of that, each app adds its own **status** colours, which are the only place the
four genuinely diverge — because each is expressing something different:

- `salat-campus` — `clear` / `tight` / `blocked`, how much room a prayer window has.
- `hifz-trail` — `solid` / `shaky` / `lost`, the three revision grades.
- `halal-bites-unilag` — `certified` / `owned` / `reported` / `unverified`, the four
  levels of halal assurance. These four are deliberately distinct hues so they can
  never be mistaken for the price band sitting next to them.
- `zakat-kit` — `due` / `short` / `over`.

Each status token carries a `$description` saying what it means, because a designer
picking `tight` should know it means "under ten free minutes", not "amber-ish".

## Importing into Figma

### With Tokens Studio (recommended)

1. Install the **Tokens Studio for Figma** plugin.
2. Plugin → **Tools → Load from file/folder** → choose `mssn-oss.tokens.json`.
3. The file ships `$metadata` and `$themes`, so the four themes appear ready to
   switch between. `core` is marked **source** in each theme — it is shared, and
   editing it changes all four apps.
4. **Export to Figma variables** from the plugin to turn them into native variables.

### With native Figma variables import

Most variables-import plugins accept this file directly. `core` becomes one
collection; each `theme/*` set becomes a mode or a collection of its own, depending on
the plugin.

### Dark mode

Each theme carries a `color.pageDark` token — the body background under
`prefers-color-scheme: dark`. The apps currently re-theme only the page background and
let text invert, so there is no full dark palette to import yet. **Producing one is a
genuinely useful design contribution**, and the obvious next piece of work here.

## Keeping it honest

These values were extracted from the four apps as built, not invented for the file —
each one is live in an `@theme` block in that project's `app/globals.css`. If you
change a token here, change it there too, or the file starts lying.

The type scale and spacing mirror the Tailwind steps the apps actually use, not the
full Tailwind scale. If a size is not in this file, no app uses it.

## What is not in here yet

- A dark palette beyond the page background (see above).
- Type *styles* — the apps compose size and weight inline rather than naming
  combinations like "card title".
- Component specs. Those live in the design-system page rather than in tokens.
