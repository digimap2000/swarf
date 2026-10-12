---
name: writing-a-log-entry
description: Turn a session of workshop work into a published log entry on swarf - bringing the photos in safely, writing the entry from Andrew's notes and the photos themselves, building, and pushing. Use when Andrew says what he did on a project, drops photos in the inbox, or asks for something to be written up.
---

# Writing a log entry

An entry is one sitting of work on one project: what was done, what was found,
what it means for what comes next.

## The order

1. **Get the facts.** Read Andrew's notes and look at every photo. List what
   you still need to know to write it truthfully - a measurement, which part
   that is, what order things happened in - and ask in one go. Do not fill a
   gap with what is usual for machines of the type.
2. **Make the folder.** `content/projects/<project>/log/<YYYY-MM-DD>-<slug>/`.
   The date is the day the work was done, not the day it was written up. The
   slug is a few plain words (`stripping-the-headstock`). It becomes the URL
   and cannot change after publication.
3. **Bring the photos in.**
   ```sh
   tools/intake content/projects/<project>/log/<folder> inbox/*.HEIC
   ```
   Then rename each from the camera's number to what it shows
   (`headstock-front-bearing.jpg`). Leave out the ones that add nothing.
4. **Write `index.md`.**
5. **Update the project.** If the work changed where the project stands, change
   `status` in the project's `_index.md`, and take anything now established out
   of its "Still to record" list. A fact worth looking up later (a thread, a
   bearing number, a clearance) also goes on a reference page.
6. **Build.** `hugo --gc --minify`, and read the output: no errors, no
   warnings. Look at the page in `hugo server`.
7. **Show Andrew** the entry before it is pushed, unless he has said to
   publish without asking.
8. **Commit and push.** `tools/check-photos` first. The push publishes.
9. **Confirm it is live.** `gh run watch`, then load the page.

## The entry

```markdown
---
title: Stripping the headstock
date: 2026-10-20
summary: The spindle is out. The front bearing is scored and the rear is fine.
---

Prose.

![The front bearing journal, with a score line running round it a third of the
way along](front-journal-scoring.jpg "The score is deep enough to catch a
fingernail, so the journal will need grinding rather than polishing.")
```

- `title` says what was done, in a few words.
- `summary` is one sentence and gives the outcome, because the log shows it and
  most readers will read only that.
- A photo on a line of its own becomes a full-width figure. The text in square
  brackets describes the picture; the quoted text is the caption.
- A run of photos that belong together goes in a gallery:
  ```markdown
  {{< gallery >}}
  ![description](one.jpg "caption")
  ![description](two.jpg "caption")
  {{< /gallery >}}
  ```
- Link to another page by its file path, `../../reference/specification.md`,
  so the link works on GitHub as well as on the site.
- A table for anything measured more than once.

## What goes wrong

- **A photo copied in by hand.** It carries a location. The pre-commit hook
  catches it only if `git config core.hooksPath .githooks` was run in this
  clone - check with `git config core.hooksPath`.
- **A date in the future.** Hugo leaves the page out of the build without
  saying so. If an entry is missing from the log, check its date first.
- **A photo name in the entry that does not match the file.** The build stops
  with the name of the entry and the photo. That is deliberate.
