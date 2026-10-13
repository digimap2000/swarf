---
name: adding-a-project
description: Start documenting a new project on swarf - choosing its permanent folder name, writing the overview page and its front matter, and setting up its cover photo and reference pages. Use when Andrew wants a new project on the site, including one that is already finished or lives in another repository.
---

# Adding a project

A project is a folder under `content/projects/`. Its place in the tree is all
that makes it a project; there is nothing to register.

## The order

1. **Agree the folder name with Andrew.** Lower case, hyphens, the thing's own
   name (`smart-and-brown-lathe`). It is the URL for the project and for every
   entry under it, and it cannot change once pushed.
2. **Write `_index.md`** in that folder, and copy `log/_index.md` and
   `photos/_index.md` from an existing project. They give the project its
   full log page and its photos page, which the project page links to.
3. **Add a cover** if there is a photo that stands for the project: bring it in
   with `tools/intake` and name it `cover.jpg`. A project with no cover is
   listed without a thumbnail, which is fine.
4. **Build, show Andrew, commit, push**, as for an entry.

## The overview

```markdown
---
title: Can an AI restore a lathe?
summary: "The question on nobody's lips: can an AI bring an old lathe back to precision work?"
kind: Restoration
date: 2026-10-12
coverAlt: The lathe as collected, on its cabinet stand
facts:
  - { label: Maker, value: Smart & Brown }
  - { label: Model, value: Model A }
---

What it is and why it is here, in a paragraph or two.
```

- `title` and `summary` are the hook. Andrew asked on 13 October 2026 for them
  to read like a journalist's headline and standfirst, a question or a tease
  that makes someone want to click: "Can an AI restore a lathe?", not "Smart
  & Brown Model L lathe". The plain name of the thing goes in `facts` and the
  first paragraph. The summary is what the list of projects shows, so it can
  run to two short sentences, and every claim in it still has to be true.
- `kind` is what sort of project it is, in a word: Restoration, Build,
  Software, Electronics. Reuse a word already in use before adding one.
- There is no `status` field. Andrew asked on 13 October 2026 for no status
  labels anywhere a reader sees them: where a project stands is said in
  plain sentences on its page, not as a tag like "Survey at rest".
- `date` is when the project started, and shows as "Started October 2026".
- `facts` is the short table at the top of the page: only what is established,
  in the order given. Leave a fact out rather than writing "unknown".
- `coverAlt` describes the cover photo.
- `coverPlaceholder: true` marks a cover that is a stand-in card rather than
  a photo of the thing, which keeps it out of the project's photo gallery.
  Delete the line when a real cover goes in.

The projects list ranks projects by their newest log entry: the latest is the
hero, the next three are cards, the rest a short list. A project with no
entries sits at the bottom in order of title, so a new project rises only
when work on it is written up. There is nothing to set by hand.

## Reference pages

Undated pages under `reference/`, one subject each: a specification, a parts
list, the sources consulted. They are listed at the foot of the project page in
alphabetical order by title.

```markdown
---
title: Specification
summary: Capacities, speeds and threads, from the maker's manual.
---
```

Say on the page where each figure came from - measured, or from which document.

## A project that lives somewhere else

For software or a design with its own repository, the overview links to the
repository and to anything running, and says what the project is in terms a
visitor can follow. Do not copy the other repository's README in; it will go
stale. The log is optional for a project that is not being worked on here.
