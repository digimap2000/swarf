---
name: writing-a-log-entry
description: Turn workshop work into a published story in a project's log on swarf - choosing the topic, bringing the photos in safely, writing it from Andrew's notes and the photos themselves, building, and pushing. Use when Andrew says what he did on a project, drops photos in the inbox, or asks for something to be written up.
---

# Writing a log entry

An entry is a story about one topic on one project, not a diary of one
sitting.

## A story, not a diary

Andrew asked for this on 13 October 2026. The entries until then went
sitting by sitting, and he found them "a bit literal": we did this, then
Andrew did that. He wants the work rolled up into topics that are worth
reading for their own sake, bringing in history, discovery, work and results.
His example was the hunt for the lathe's collet: a paper trail through old
catalogues, checked with 3D prints, is a topic in its own right, though it
ran over two days and a dozen messages.

- **Pick the topic, not the day.** A topic is a question and how it came out:
  what collet does it take, why would the oil not move, is the bed worn. One
  sitting can feed two stories, and one story can take a week.
- **Write it when it has an ending:** a result, a dead end, or a decision.
  Until then the facts go on the reference pages and "Where it stands" is
  kept current, so nothing waits on the story to be recorded.
- **Open with what makes it worth reading,** which is seldom what happened
  first. Arrange it by the puzzle, not the clock. A long story can have a few
  plain crossheads.
- **Bring in the background** that makes sense of it: who made the thing, how
  it is meant to work, what the old paper says. Link every source.
- **Keep the people in.** Who thought of what, in their own words where they
  are good. Wrong turns and dead ends stay, told as part of the story and not
  as a list of corrections.
- **End on what is settled and what is not.**
- **Roll an older entry in** when the new story covers its ground: write the
  story in a new folder, put the old entry's path in `aliases`, and remove
  the old folder, so the old address still arrives somewhere.

Still true of every story: no invented facts, a table for anything measured
more than once, and nothing in it that Andrew did not say or show.

Andrew added on 13 October 2026, about the lathe's journal but true of any:

- **Tell it as it happened.** Do not tidy up the reasoning afterwards, do not
  supply a motive nobody stated, and do not move credit: who found a thing is
  part of the record.
- **Make it useful to someone with the same machine.** Dimensions, part
  numbers, references, the test that settled it, and what is still not
  known.
- **The writing is not another job for Andrew.** He reads for significant
  omissions, inaccuracies and needless explanation. Do not make him an
  editor.

## The order

1. **Get the facts.** Read Andrew's notes and look at every photo. List what
   you still need to know to write it truthfully - a measurement, which part
   that is, what order things happened in - and ask in one go. Do not fill a
   gap with what is usual for machines of the type.
2. **Make the folder.** `content/projects/<project>/log/<YYYY-MM-DD>-<slug>/`.
   The date is the day the story reached its end, not the day it was written
   up. The slug is a few plain words (`stripping-the-headstock`). It becomes
   the URL and cannot change after publication.
3. **Bring the photos in.**
   ```sh
   tools/intake content/projects/<project>/log/<folder> inbox/*.HEIC
   ```
   Then rename each from the camera's number to what it shows
   (`headstock-front-bearing.jpg`). Leave out the ones that add nothing.
4. **Write `index.md`.**
5. **Update the project.** If the work changed where the project stands, rewrite
   the few lines under "Where it stands" in the project's `_index.md`, in plain
   sentences and with no status labels. A fact worth looking up later (a thread, a
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

- `title` is a headline for the story, in a few words.
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
- **A colon in the summary or title.** `summary: Three things: a, b and c`
  is not valid YAML and the build stops with "mapping value is not allowed".
  Put the whole value in double quotes.
- **A photo name in the entry that does not match the file.** The build stops
  with the name of the entry and the photo. That is deliberate.
