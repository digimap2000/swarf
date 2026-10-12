# Working on swarf

Andrew's workshop projects, written up as they happen, and growing into his
portfolio. A Hugo site built from Markdown and published to GitHub Pages on
every push to `main`. `README.md` has the layout and the reasons; this file is
the operating rules.

## Reach for a skill

| Task | Skill |
| --- | --- |
| Write up a session of work | `writing-a-log-entry` |
| Start documenting a new project | `adding-a-project` |
| Anything to do with the Smart & Brown lathe | `restoring-the-lathe` |

## Invariants

**Never invent a fact.** Andrew does the work and Claude writes it up, so every
measurement, serial number, part number, date, price and finding comes from
him or from a photo he supplied. If the notes do not say, ask, or leave it out
and say it is not yet recorded. A plausible sentence about a machine nobody
measured is worse than a gap, because a gap gets filled and a plausible
sentence gets believed.

**The repository is public, and so is its history.** Nothing goes in that
Andrew has not offered for publication: what he paid, who he bought from, his
address, a photo showing a face, a house number or a vehicle plate. Things
Claude needs to remember but must not publish go in `private/`, which git
ignores.

**Say where background came from.** History of a maker, a specification from a
manual, a claim from a forum: link the source in the text. Summarise in your
own words and do not copy passages or photos from other sites.

**Every photo goes through `tools/intake`.** The repository is public and a
phone writes its location into every photo. Never copy a photo into `content/`
any other way, and never commit an original. `tools/check-photos` must pass
before a commit; the pre-commit hook runs it if `core.hooksPath` is set.

**Look at the photos before writing about them.** Alt text says what is in the
picture for someone who cannot see it. The caption says why it is there. Write
both from the photo itself, not from its file name.

**A published URL is permanent.** The folder name is the address. Do not rename
or move a project, entry or reference page once it has been pushed. If it has
to move, add the old path to `aliases` in its front matter.

**Nothing from anywhere else.** No theme, no npm, no script, font or stylesheet
loaded from another site. The templates in `layouts/` and the one stylesheet
are the whole front end, and that is what lets this outlive its host.

**Build before pushing, and read the output.** `hugo` must finish with no
errors and no warnings. A push to `main` is a publication.

**Keep the two Hugo versions in step.** `HUGO_VERSION` in
`.github/workflows/deploy.yml` is what builds the published site. Bump it
deliberately, to the version `hugo version` reports locally, and check the
site still builds clean when you do.

## Commands

```sh
hugo server                                  # preview at localhost:1313/swarf/
hugo --gc --minify                           # full build into public/
tools/intake <page-folder> <photo>...        # bring photos in
tools/check-photos                           # every photo under content/
```

## Prose

British spelling. First person, past tense for work done: "I drew the spindle",
not "the spindle was drawn" and not "we". The "I" is whoever decided the work.
On most projects that is Andrew. On the lathe it is Claude, who directs that
restoration and names Andrew as the one who did and found things; pages there
carry `author: Claude` and the templates show it, so no reader has to guess. Plain and specific, with the reason
as well as the action: why this order, why this fit, what was tried first and
did not work. Mistakes and dead ends are part of the record and stay in.

Give a measurement in the units it was taken in, with the instrument if it
matters, and the conversion in brackets only where a reader would want it. An
imperial machine is described in imperial.

No headings in a short entry. One sentence of `summary` in the front matter,
which is what the log shows; it says what was done, not that something was.
