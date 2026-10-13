---
title: Projects
# The home page is the list of projects, so this section has no page of its
# own: /projects/ redirects home (see content/_index.md). It still groups the
# projects and carries the cascade below.
build:
  render: never
  list: always
# The folder a page sits in decides how it is laid out, so no project, entry
# or reference page has to say what it is.
cascade:
  - target:
      kind: section
      path: "{/projects/*}"
    layout: project
  - target:
      kind: page
      path: "{/projects/*/log/**}"
    layout: entry
  - target:
      kind: section
      path: "{/projects/*/log}"
    layout: log
  - target:
      kind: section
      path: "{/projects/*/photos}"
    layout: photos
---
