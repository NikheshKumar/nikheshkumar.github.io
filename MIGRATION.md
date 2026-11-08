# Moving nikheshkumar.github.io from Jekyll (AcademicPages) to Hugo + PaperMod

The address stays https://nikheshkumar.github.io/. Every post, page, feed and redirect with your own content keeps its URL.

## Steps

1. Make a backup branch of the current Jekyll site:
   `git switch master && git switch -c jekyll-archive && git push -u origin jekyll-archive && git switch master`
2. Start a migration branch: `git switch -c papermod`
3. Remove the Jekyll files (everything except `.git`):
   `git rm -r -q . && git clean -fdx`
4. Unzip this folder's contents into the repo root.
5. Add the theme, pinned to the tested commit:
   `git submodule add https://github.com/adityatelange/hugo-PaperMod themes/PaperMod`
   `git -C themes/PaperMod checkout 118119693d8b5ac211b939775678310973bcb232`
6. Preview locally with Hugo v0.169.0: `hugo server`, then open http://localhost:1313/
7. Commit and push: `git add -A && git commit -m "Move site to Hugo + PaperMod" && git push -u origin papermod`
8. In GitHub, open Settings → Pages → Build and deployment → Source and choose **GitHub Actions**.
9. Merge `papermod` into `master`. The workflow in `.github/workflows/hugo.yaml` builds and deploys on every push to `master`.

To roll back: Settings → Pages → Source → Deploy from a branch → `jekyll-archive` / root.

## Writing posts

- New post: `content/posts/YYYY-MM-DD-slug.md`, with front matter `title`, `date`, `tags`, and optionally `url: /posts/YYYY/MM/slug/` to keep the old URL style.
- Math: `$...$` inline and `$$...$$` display. KaTeX renders it at build time, and bad LaTeX fails the build with the file and line.
- A literal dollar sign in prose is written `\$`.
- Set `lastmod:` to show "Last updated" on a post.
