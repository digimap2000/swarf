---
title: Projects
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
---
