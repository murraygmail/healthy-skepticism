# Healthy Skepticism — course site

Source for healthy-skepticism.com, served by GitHub Pages from `main`.

This folder is the master copy. It replaces the earlier `New Website` folder.

## Structure

| File | What it is |
|---|---|
| `index.html` | Landing page: what the course is, the five faults, where it is offered, and **New on the site** |
| `papers.html` | The paper library. Public and indexable. Two sections: Fault Related, General Interest |
| `students.html` | Course materials, behind the class password. One block per session. No dates, no venue names |
| `site.css` | All styling for all three pages |
| `papers/` | Public paper PDFs |
| `materials/` | Student PDFs: `sessionN-takehome.pdf`, `sessionN-slides.pdf` |
| `CNAME` | Custom domain for GitHub Pages |

One stylesheet, three pages. A colour or a font changes in `site.css` and all
three follow. If you edit `site.css`, upload it along with the pages, and
hard-reload (Cmd-Shift-R) when checking, because browsers cache stylesheets.

## Posting a paper

Two edits, in this order:

1. Drop the PDF in `papers/`. Copy an `<article class="paper">` block into the
   right section of `papers.html`, and give it an `id`.
2. Add one `<li>` at the top of the NOTICES list in `index.html`, linking to
   `papers.html#that-id`. Drop the oldest notice off the bottom, four or five
   is plenty.

Both blocks carry a copy-me template in a comment.

`papers.html` has two sections. **Fault Related** holds papers that teach one
of the five faults: each entry carries its fault as a `<p class="tag">` and an
`fN` class for the accent colour (f1 relative reporting, f2 probability
reversal, f3 arbitrary categories, f4 the Bernoulli fallacy, f5 the causal
leap), ordered by fault. **General Interest** holds papers that work through
the evidence on one medical subject: no tag, no `fN` class, newest first.

Which section: if the paper teaches a fault it goes in the first, even when it
is built around one subject. If the subject is the point and the fault is
incidental, it goes in the second. Fault names are canonical and never get
renamed.

## Adding a venue

Copy one `<dt>`/`<dd>` pair inside the OFFERINGS block in `index.html`.
Nothing else on the site names a venue or a date, so the materials page
serves every offering unchanged.

## Changing the class password

The gate is client-side, in the script at the foot of `students.html`. Get the
hash of the new password with

    echo -n 'yournewpassword' | shasum -a 256

and paste the hex string over `PASSWORD_SHA256`.

The gate is a courtesy screen, not security. Anyone reading the page source
can find the file paths, and the PDFs in `materials/` are served by GitHub
Pages to anyone who knows the URL. Nothing sensitive belongs there.

## Workflow

Edit here, serve it locally to check it, then upload the changed files to
GitHub.

    cd "<this folder>"
    python3 -m http.server

Then open http://localhost:8000. Check `students.html` in a private window so
the session flag from an earlier visit does not let you past the gate without
typing the password. GitHub Pages redeploys within a minute or two of the
upload.

## Housekeeping still open in the repo

- `slides/` and the root `day1.pdf` hold full decks and are served publicly to
  anyone with the URL, which undercuts the password gate. Delete them.
- `materials/` in the repo also holds `.pptx` and `.docx` copies that nothing
  links to. They are not in this folder. Delete them from the repo too.
- Enforce HTTPS in the GitHub Pages settings.
