# Newsletter Archive - GitHub Pages Setup and Monthly Workflow (08-13-2026)

This guide takes the archive from the folder now sitting in your newsletter
directory to a live, linkable web page. The files are already built. What
remains is a repository, a checkbox, and a link on the Academic Affairs page.
Budget about 20 minutes.

The August teaser preview is installed as a placeholder issue so you can test
the whole chain before the September issue exists.

## What you end up with

| Page | Address |
|---|---|
| Archive landing page | `https://bereacollege-ie.github.io/academic-corner-archive/` |
| August 2026 teaser | `https://bereacollege-ie.github.io/academic-corner-archive/issues/2026-08/` |
| September 2026 issue | `https://bereacollege-ie.github.io/academic-corner-archive/issues/2026-09/` |

The pattern holds forever: one folder per issue, named `YYYY-MM`, and the URL is
the folder path. Nothing else has to be decided later.

## How this differs from the submission form

The submission form needed a serverless function, a GitHub token, and Vercel,
because it writes data. The archive only reads. GitHub Pages takes the files in
a repository and serves them as an ordinary website, which is the entire
mechanism. There is no token, no build step, no second service, and no monthly
cost.

The one thing GitHub Pages does not do on the free plan is serve from a private
repository, so this repository is public. That was the tradeoff you accepted.
See "What must never go in this repository" below, because the consequence is
sharper than it first appears.

## Step 1: Create the repository

1. Go to `github.com/BereaCollege-IE` and click **New repository**.
2. Name: `academic-corner-archive`. The name becomes part of every published
   URL, so it should be lowercase and hyphenated, and it should not be renamed
   afterward.
3. Visibility: **Public**. On the free plan this is required for Pages.
4. Do not initialize with a README, a .gitignore, or a license. The folder
   already has what it needs, and an initialization commit creates a conflict
   you would then have to resolve.
5. Click **Create repository**.

If the New repository button is missing or the organization refuses the
creation, the organization owner may have restricted repository creation or
Pages publication under Organization settings. That is a permissions
conversation, not a technical problem.

## Step 2: Publish the folder with GitHub Desktop

1. Open GitHub Desktop. Choose **File > Add Local Repository**.
2. Select `Newsletter Archive Web App` inside your newsletter folder.
3. GitHub Desktop will say it is not a repository and offer to create one here.
   Accept.
4. Enter a commit message such as "Initial archive with August teaser" and click
   **Commit to main**.
5. Click **Publish repository**. Confirm the name is `academic-corner-archive`,
   confirm the organization is `BereaCollege-IE`, and **uncheck** "Keep this
   code private." Publish.

If GitHub Desktop shows a stale `index.lock` warning, the submission form
repository has a few of those already, and they are harmless leftovers from
interrupted operations. They do not affect this repository.

## Step 3: Turn on GitHub Pages

1. On the repository page, go to **Settings > Pages**.
2. Under Build and deployment, set Source to **Deploy from a branch**.
3. Set the branch to **main** and the folder to **/ (root)**. Click **Save**.
4. Wait. The first publish usually finishes in about a minute, though it can
   take closer to ten. The Pages settings page shows the live URL with a green
   check when it is ready.

The `.nojekyll` file already in the folder tells GitHub to serve the files
exactly as they are rather than running them through its blog engine first.
Without it, any folder or file beginning with an underscore would be silently
dropped. It costs nothing to keep and prevents a confusing class of failure.

## Step 4: Verify before telling anyone

1. Open the landing page URL. The masthead should be dark blue with the
   Academic Affairs logo, and the fonts should be Barlow and Newsreader Display
   rather than a system default. If the fonts look generic, the `assets` folder
   did not publish.
2. Click the August 2026 entry. It should open in a new tab and render the
   newsletter, not the code.
3. Open the same URL on a phone. The landing page has been checked for
   horizontal overflow at 390 pixels wide.
4. Press Tab once on the landing page. A "Skip to the issue list" link should
   appear in the top left corner. That link is the fastest confirmation that
   keyboard navigation is intact.

## Step 5: Link it from the Academic Affairs page

The new-window behavior lives on the linking page, not on GitHub. The markup is:

```html
<a href="https://bereacollege-ie.github.io/academic-corner-archive/"
   target="_blank" rel="noopener">The Academic Corner newsletter archive</a>
```

In WordPress, you would paste the URL, select the link text, and use the
**Open in new tab** toggle in the link settings. WordPress adds `rel="noopener"`
on its own.

Two notes on that markup. `rel="noopener"` is not optional; without it the newly
opened page gets a scripting handle back to the page that opened it. And the
link text should say where it goes, since "click here" gives a screen reader
user nothing to work with when they pull up a list of links on the page.

Link to the landing page rather than to an individual issue. The landing page
never goes stale.

## Monthly workflow, once this is running

1. Finish the issue as usual.
2. Create `issues/YYYY-MM/` in the archive folder and save the newsletter inside
   it as `index.html`. The name is always `index.html`, which is what produces a
   clean URL with no file extension.
3. Open the root `index.html` in a text editor and find the comment block marked
   `ADD A NEW ISSUE HERE`. Copy the entry below it, paste the copy above the
   original, and edit the five marked pieces. Move the prior entry down into the
   Past issues list.
4. In GitHub Desktop: commit, then push. Live in about a minute.

Roughly a five minute task. If it starts feeling like a chore around issue six,
that is the point at which generating the landing page from a small list of
issues would earn its keep, and it is worth revisiting then rather than now.

## Rules that keep the links alive

The value of an archive is that old links still work. Three rules protect that:

- **Never rename or delete a published issue folder.** Once a URL has been in a
  provost email, it is permanent. A moved page is a broken link in someone's
  inbox two years from now.
- **Never put spaces, parentheses, or dates in a published path.** Your file
  naming convention is right for working documents and wrong for URLs. A space
  becomes `%20`, a parenthesis becomes `%28`, and some email clients truncate
  the link at the first one.
- **Keep the local folder and the repository as the same thing.** Editing a copy
  somewhere else and pasting it back is how archives drift out of sync.

## What must never go in this repository

The repository is public, and a public repository exposes its full commit
history, not just its current files. Anything committed here remains readable
forever, even after you delete the file and commit the deletion. Deleting a file
removes it from the current view; it does not remove the object from history.

So: finished, already-distributed issues only. Drafts, held items, contributor
submissions, and anything with a name or an email address in it belong in the
private submissions repository. This is the one real cost of choosing Pages over
Vercel, and it is entirely manageable as long as the rule stays a rule.

## Three defects in the teaser placeholder

The teaser was built as a screenshot preview, not as a page meant to be
published, and it shows in three places. None of them block the setup, and all
three would matter on a real issue:

1. **No `<h1>`.** The page starts at `<h2>`. A screen reader user landing on the
   page gets no top-level heading telling them what they are reading.
2. **Seven dead links.** Every `href="#"` in the teaser goes nowhere. In a
   screenshot that was invisible. On a published page a reader will click one.
3. **Heading order skips.** The sequence runs h2, h3, h2, h2, h3, h4, which
   makes the document outline harder to navigate by headings.

Whether to fix these in the teaser is your call, since it is a placeholder that
may be replaced in a few weeks anyway. Fixing them in the September template
before the first real issue ships would be the higher-value move. Say the word
and it can be done in either place.

## A brand inconsistency worth resolving

The teaser uses a palette and typeface set (`#004175` blue, Barlow, Newsreader
Display, Barlow Condensed) that differ from the standards recorded in your
`voice-and-style.md` (`#005A8B` Berea Blue, Proxima Sera, Proxima Nova). The
archive landing page has been built to match the teaser, on the assumption that
the newsletter is on the current brand and the context file has not caught up.

[Inference] This is based on the teaser's own comment describing itself as using
the "New Berea College brand," not on a brand document. If that assumption is
backwards, the landing page palette should change rather than the newsletter.

## Optional: a custom domain

If Berea's web administrators would create a CNAME record pointing something
like `academiccorner.berea.edu` at `bereacollege-ie.github.io`, that hostname can
be entered under Settings > Pages > Custom domain, and GitHub will issue a
certificate for it.

Worth weighing before doing it: the `github.io` URL keeps working after a custom
domain is added, so nothing breaks, but the reverse is not true. If a custom
domain is ever removed, every link that used it dies. A custom domain is
therefore easier to add later than to walk back, which argues for launching on
the `github.io` address and revisiting once the archive has a few issues in it.

## Files in the archive folder

```
Newsletter Archive Web App/
  index.html                        Landing page (edit monthly)
  README.md                         Notes for anyone who inherits this
  .nojekyll                         Serve files as-is
  .gitignore                        Keeps .DS_Store out of the repository
  assets/fonts/                     Brand fonts, landing page only
  assets/img/                       Academic Affairs logo
  issues/2026-08/index.html         August teaser placeholder
```

Issue files stay fully self-contained, with fonts and images embedded, because
the same file gets emailed. Only the landing page uses the shared `assets`
folder, which is why it loads in a fraction of the size.

---

*This guide and the archive site were created in collaboration with Claude AI.*
