# SciPost Physics Codebases manuscript

This folder contains the LaTeX source for the manuscript

> **`exact_diagonalization_cpp`: a five-axis C++/CUDA/MPI toolkit for
> exact diagonalization of quantum lattice models**

prepared for submission to
[SciPost Physics Codebases](https://scipost.org/SciPostPhysCodeb).

## Files

| File | Purpose |
|---|---|
| `main.tex` | Main manuscript source. |
| `refs.bib` | BibTeX bibliography. DOIs are included on every reference that has one (SciPost requires DOIs). |
| `SciPost.cls` | SciPost LaTeX class, vendored from [git.scipost.org](https://git.scipost.org/scipost/SciPost_LaTeX_Templates_Submission/-/blob/master/SciPost.cls) under CC0. The local copy adds a `PhysCodeb` option that produces the "SciPost Physics Codebases" header. |
| `SciPost_bibstyle.bst` | SciPost BibTeX style, vendored from [git.scipost.org](https://git.scipost.org/scipost/SciPost_LaTeX_Templates_Submission/-/blob/master/SciPost_bibstyle.bst) under CC0. |
| `Makefile` | Convenience targets (`make`, `make clean`, `make view`). |
| `figures/` | Folder for figure PDFs. The manuscript currently uses framed placeholders for figures whose data is not reproducible on a workstation; the corresponding "required run" callouts in the manuscript give the exact command, hardware, and expected wall-clock time to produce each figure. |

## Build

Requires `pdflatex` and `bibtex` (TeX Live 2022+ recommended). If
`latexmk` is available the Makefile uses it; otherwise it runs the
standard four-pass pdflatex+bibtex loop.

```bash
make            # produces main.pdf
make clean      # removes build by-products (keeps main.pdf)
make distclean  # removes build by-products and main.pdf
make view       # opens main.pdf in the system viewer
```

The vendored `SciPost.cls` and `SciPost_bibstyle.bst` are CC0-licensed
and bundled here so that `make` works on a stock TeX Live install
without internet access. To upgrade to a newer SciPost class/style,
overwrite the two files from the upstream GitLab repository.

## Required runs

Six figures in the manuscript (`Figure 1` through `Figure 7`) report
on distributed-memory and multi-GPU experiments that cannot be run on
a single workstation. Each is wrapped in a "Required run" callout box
that specifies:

* the hardware (e.g. *"4 H100 80GB SXM5 GPUs on NVLink"*),
* the exact command line to reproduce the data (e.g. `mpiexec -n 64 ./build/...`),
* the postprocessing/plotting command, and
* the expected wall-clock time.

When the figure PDFs are generated and dropped into `figures/`, the
manuscript's `\figureplaceholder{...}` calls should be replaced with
the corresponding `\includegraphics{figures/...}` calls. The exact
PDF filenames are written next to each `--out` flag in the manuscript.

## License

The manuscript text is released under the
[Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/),
matching the SciPost open-access policy. The vendored
`SciPost.cls` and `SciPost_bibstyle.bst` files are CC0.
