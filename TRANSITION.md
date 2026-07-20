# Transition to the canonical public surface

**Status: PREPARED, NOT ACTIVATED.** This change lives only on the branch
`transition/canonical-surface`. It is not pushed, not merged, and GitHub Pages is
unaffected until the branch is merged into `main` by the author.

## Why

Every public intellectual work in the Agent Manifest ecosystem has one canonical
public representation of record under `agent-manifest-spec.org` (see the ecosystem
GOVERNANCE — "Public surface"). The canonical public page for the ∈ Principle is
now:

> https://agent-manifest-spec.org/works/e-principle/

The GitHub Pages site (`https://agent-manifest.github.io/e-principle/`) should no
longer compete with that canonical surface as a second indexable copy of the same
work.

## What this branch changes

- **`docs/index.html`** — replaced with a minimal transfer page:
  - `rel="canonical"` → the new landing;
  - `meta http-equiv="refresh"` → client redirect to the new landing (GitHub Pages
    cannot issue a server-side 301);
  - `meta robots: noindex, follow` → the old page drops out of the index without
    breaking outbound links.

## What this branch deliberately does NOT change

- **The repository is not deleted.** Source, history, and branches are intact.
- **Releases are untouched** (`v1.0` and any future release remain).
- **The book PDFs remain** under `book/` (English and Spanish editions), with their
  own Zenodo DOIs — no links to files or releases are broken.
- **Citation metadata is unchanged** (`CITATION.cff`, `codemeta.json`, `README.md`).

## Exactly what happens on merge

1. The author merges `transition/canonical-surface` into `main`.
2. GitHub Pages rebuilds from `main`/`docs`.
3. `https://agent-manifest.github.io/e-principle/` then serves the transfer page:
   visitors are redirected to the canonical landing; crawlers see `canonical` +
   `noindex` and consolidate ranking signals onto the canonical surface.
4. Direct links to releases and to the book PDFs continue to resolve unchanged.

## Recommended follow-up (optional, author's decision)

The secondary Jekyll pages (`docs/e-principle.md`, `docs/citation.md`) still render
under `/e-principle/…`. To fully avoid duplicate indexable content, add
`noindex, follow` + a `canonical` to the new landing in
`docs/_includes/head-custom.html` (which those pages include). This is left as a
separate, explicit decision and is **not** applied on this branch.

## Rollback

Delete the branch, or revert `docs/index.html`. Nothing outside this branch is
affected until merge.
