# The Academic Corner: Newsletter Archive

Public archive of The Academic Corner, the monthly newsletter of the Office of
Academic Affairs at Berea College. Published with GitHub Pages.

**Live site:** https://bereacollege-ie.github.io/academic-corner-archive/

## Folder layout

```
index.html                  Archive landing page (lists every issue)
assets/fonts/               Brand fonts, used by the landing page only
assets/img/                 Academic Affairs logo
issues/
  2026-08/index.html        One folder per issue, named YYYY-MM
.nojekyll                   Tells GitHub Pages to serve files as-is
```

## Adding an issue

1. Create `issues/YYYY-MM/` and save the finished newsletter inside it as `index.html`.
2. Open `index.html` at the repo root and follow the comment marked
   `ADD A NEW ISSUE HERE`. Move the previous current issue into Past issues.
3. Commit and push in GitHub Desktop. The site updates in about a minute.

## Rules that keep links working

- Issue files are always named `index.html` inside a `YYYY-MM` folder. This gives
  clean URLs like `/issues/2026-09/` with no file extension.
- Published paths use lowercase, digits, and hyphens only. No spaces, no
  parentheses, no dates in the filename. Spaces become `%20` in a URL and break
  when pasted into some email clients.
- Once an issue path is published it is never renamed, moved, or deleted.
  Links live in email inboxes indefinitely.

## What belongs in this repo

Finished, already-distributed issues only. The repository is public, which means
its full commit history is public. Anything committed here stays readable in
history even after the file is deleted. Drafts, held items, and contributor
submissions belong in the private submissions repo, not here.

---
*This archive was built by the Office of Academic Affairs in collaboration with Claude AI.*
