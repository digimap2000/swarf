# Swarf

Workshop projects, written up as they happen. Published at
<https://digimap2000.github.io/swarf/>.

This repository is the record. The website is a rendering of it that can be
thrown away and rebuilt from here at any time, on any host. Every page is a
Markdown file and every photo is a JPEG beside it, so the whole thing can be
read on GitHub, or in a text editor, with no tooling at all.

## Layout

```
content/
  projects/
    smart-and-brown-lathe/
      _index.md                       the project: what it is, where it stands
      cover.jpg                       optional, the photo that represents it
      log/
        2026-10-20-what-was-done/     one folder per entry, dated
          index.md
          a-photo.jpg                 the entry's photos live with it
      reference/
        specification.md              undated pages: facts worth keeping
layouts/      the templates, all written for this site, no theme
assets/css/   one stylesheet
tools/        intake and check-photos, for photographs
```

A page's place in that tree is what decides how it is shown. A folder under
`projects/` is a project, anything under its `log/` is a dated entry, and
anything under its `reference/` is a reference page.

## Adding to it

Photos first, always through `tools/intake`, never copied in by hand:

```sh
mkdir -p content/projects/smart-and-brown-lathe/log/2026-10-20-what-was-done
tools/intake content/projects/smart-and-brown-lathe/log/2026-10-20-what-was-done ~/Desktop/IMG_*.HEIC
```

Then the entry, as `index.md` in the same folder:

```markdown
---
title: What was done
date: 2026-10-20
summary: One sentence, shown in the log.
---

Prose.

![What the photo shows](img-4471.jpg "Why it matters")
```

## Why photos go through intake

This repository is public, and a phone records where it was in every photo it
takes. `tools/intake` converts to sRGB JPEG, cuts the long edge to 2400 px,
and removes all metadata, then reads the file back to prove it. The originals
stay in the photo library; only the web-sized copy is committed.

The pre-commit hook refuses a photo that still carries metadata. Git does not
run hooks from a fresh clone until told to, once per clone:

```sh
git config core.hooksPath .githooks
```

## Previewing and publishing

```sh
hugo server          # http://localhost:1313/swarf/, rebuilds as files change
```

Publishing is a push to `main`. The workflow in `.github/workflows/deploy.yml`
builds the site with a pinned Hugo and replaces what is on GitHub Pages,
usually within a couple of minutes.

A build fails, rather than publishing a broken page, if an entry refers to a
photo that is not in its folder.

## Moving house

Nothing here depends on GitHub beyond the workflow file. `hugo` writes the
whole site to `public/` as plain files, and any static host will serve that
folder. To leave:

1. Build with the new address: `hugo --baseURL https://new.example/`
2. Upload `public/`, or point the new host at this repository with `hugo` as
   the build command and `public` as the output folder.

A domain of its own is the one thing that would make that move invisible to
readers. There is none yet, so links to `digimap2000.github.io/swarf` would
break if the site moved.

## Limits to watch

GitHub asks that a repository stay under about 1 GB, and a Pages site may not
exceed 1 GB. At roughly half a megabyte a photo that is on the order of two
thousand photos. `du -sh content` is the number to keep an eye on. If it is
ever reached, the photos move to object storage and the Markdown stays here.
