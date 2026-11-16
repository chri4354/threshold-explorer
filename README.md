# Threshold Explorer

A single-page, dependency-free rebuild of the precision–recall Shiny app, so it can be
served as a static site (GitHub Pages) instead of needing a Python server.

Open `index.html` in a browser. There is no build step and nothing to install.

## What it does

Two classes score on overlapping normal distributions. Three sliders control the
base rate, how far apart the two groups sit, and where the decision threshold goes.
Everything else updates live: the distributions, a confusion matrix, five metrics,
a ROC curve and a precision–recall curve.

## What it adds over the Shiny version

- **A base-rate slider**, from 0.1% to 50%. The Shiny app sampled a fixed number per
  class, so the classes were always balanced and precision could not be shown to depend
  on prevalence. That is the main thing week 7 needs to demonstrate.
- **Curves drawn at their real size**, so a rare positive class visibly shrinks to a
  sliver against the negative one.
- **A precision–recall curve** alongside the ROC curve, with the base-rate floor marked.
  Holding the threshold fixed and dragging prevalence shows the ROC curve standing still
  while the PR curve collapses.
- **Analytic, not sampled.** Metrics come from the normal CDF rather than a random draw,
  so nothing jitters when a slider moves and the numbers are exact.
- **Presets that match the lecture slides** — the chihuahua/muffin and smoke-alarm
  examples reproduce the figures used in class (30% and 2% precision).

## Conventions

The confusion matrix is laid out the way scikit-learn returns it: **truth down the rows,
prediction across the columns**, matching `confusion_matrix(y_true, y_pred)` and
`ConfusionMatrixDisplay`. Note this is the transpose of the square used in the week 7
slides, which puts truth in the columns so that column width reads as the base rate.

## Publishing

Any static host works. For GitHub Pages, push to a repository and enable Pages on the
default branch, root folder.
