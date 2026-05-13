# JOSS submission checklist for `delab-trees`

State of the repo as of 2026-05-13. Source: <https://joss.readthedocs.io/en/latest/submitting.html>.

## Status

| Requirement | State | Action |
|---|---|---|
| Open-source repo, OSI license | ✅ MIT in `LICENSE` | — |
| Public version-controlled repo | ✅ GitHub | — |
| `CITATION.cff` | ✅ updated to `0.4.2`, date `2024-10-24` (matches last `setup.py` commit) | — |
| `README.md` with install + usage | ✅ thorough, function table, examples | — |
| Tests | ✅ five test files in `tests/`, `run_tests.py` | confirm they pass on a fresh checkout |
| `paper.md` (JOSS submission paper) | ✅ **drafted** in `paper.md` | author review of statement-of-need claims |
| `paper.bib` | ✅ **drafted** in `paper.bib` (10 entries) | swap `Dehne2024moderation` / `Dehne2024delabbot` for real DOIs/arXiv IDs when available |
| Substantial scholarly effort | ✅ used in 3 papers ([@Dehne2023cccp], `pub_delab_quant`, `pub_delab_bot`) | — |
| Documentation of API | ✅ function table in README + tutorial notebook | consider Sphinx/MkDocs at some point — not blocking |
| Example data | ✅ anonymised Reddit + Twitter datasets shipped with package | — |
| Statement of need | ✅ in `paper.md` | author review |
| Authors + ORCIDs | ✅ Julian Dehne, ORCID 0000-0001-9265-9619 | confirm sole author or add coauthors |

## Gaps and concerns

### Blocking before submission

1. ✅ **`CITATION.cff` bumped** to v0.4.2, date 2024-10-24 (matches the last `setup.py` commit).
2. ✅ **Author list confirmed solo** (Julian Dehne) per author decision 2026-05-13. JOSS authorship is for the *software*, not the connected research papers — coauthors on those papers are not coauthors on this JOSS submission.
3. ✅ **Placeholder bib entries retained as `@unpublished`** for the two in-flight companion papers (`Dehne2024moderation`, `Dehne2024delabbot`). The CCCP arXiv preprint (`Dehne2023cccp`) is already a real reference and is sufficient to establish "substantial scholarly effort" on its own. The unpublished entries can be swapped for real DOIs/preprint IDs as the companion papers progress.

### Strongly recommended

4. ✅ **CI added.** `.github/workflows/tests.yml` runs `python -m unittest discover -s tests -p '*_tests.py'` on push, PR, and manual dispatch (Python 3.9 to match `setup.py`'s `python_requires`). First run will surface any environment-specific test issues — fix those before submission.
5. ⏸ **Dependency pinning kept as-is** per author decision 2026-05-13 (this was the working setup for the empirical studies; relaxation can wait). Reviewers may still ask — be ready to point at the existing pins and explain they reproduce the published results.
6. ⏸ **TF/Keras hard dependencies kept as-is** per author decision 2026-05-13 (same reasoning). Reviewers may suggest an `[ml]` extra; mention that you'd rather keep the install-once experience for the typical user.

### Nice-to-have

7. **Sphinx or MkDocs site** — the README is already strong; this is not a JOSS requirement. Lower priority.
8. **`pyproject.toml`** — modern Python packaging. `setup.py` works but is being deprecated. Not blocking for JOSS.
9. **Coverage reporting** — codecov badge alongside CI. Nice but not required.

## Suggested submission sequence

1. ✅ Bump `CITATION.cff` version and date.
2. ✅ Add `.github/workflows/tests.yml`.
3. Commit and push these changes to the `delab-trees` repo; confirm CI passes on GitHub.
4. Review `paper.md` for accuracy (statement-of-need framing especially).
5. Tag a release (`v0.4.2` if no code changed since, otherwise `v0.5.0`) on GitHub.
6. Archive the tagged release on Zenodo (gets a DOI for citation).
7. Submit to JOSS at <https://joss.theoj.org/papers/new> with the repo URL, the release tag, and the Zenodo DOI.

## Next concrete pieces of work

In rough order of effort:

- [x] Bump `CITATION.cff` version → matches setup.py
- [x] Add CI workflow `tests.yml`
- [x] Decide author list (solo) + affiliations for `paper.md`
- [ ] Commit and push the three new files (`paper.md`, `paper.bib`, `.github/workflows/tests.yml`) plus the `CITATION.cff` update to the `delab-trees` repo
- [ ] Watch the first CI run; fix any environment-specific issues
- [ ] Review `paper.md` for accuracy (statement-of-need framing especially)
- [ ] Tag release + archive on Zenodo
- [ ] Submit

The remaining blocker is your review of the paper.md framing — once that lands, the mechanical steps (push, tag, Zenodo, submit) take under an hour.
