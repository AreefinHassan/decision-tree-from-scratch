# Decision Tree from Scratch

[![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![No dependencies](https://img.shields.io/badge/dependencies-none-brightgreen)](#how-to-run)

A decision tree classifier built from scratch in pure Python — no imports, no libraries. This notebook implements the core building blocks of a decision tree by hand: counting class instances, measuring node impurity with the Gini index, scoring candidate splits, and partitioning data on a threshold.

## Key Results

On the toy two-class dataset (7 points: 4 of class A, 3 of class B):

| Measure | Value |
|---|---|
| Class counts | `{'A': 4, 'B': 3}` |
| Parent Gini impurity | `0.4898` |
| Weighted Gini after split (`x ≤ 1.5`) | `0.2286` |
| Impurity reduction from the split | `0.4898 → 0.2286` (≈ 53% lower) |

Thresholding the first coordinate at `1.5` isolates class B's two points at `x = 2` on the right while keeping everything else on the left — a single split cuts impurity by more than half.

## What it builds

Starting from a small two-class, two-dimensional toy dataset, the notebook defines four functions that together form the split-selection machinery of a decision tree:

| Function | What it does |
|---|---|
| `count_of_class(data)` | Counts how many instances belong to each class. |
| `gini_index(counts)` | Computes Gini impurity, `1 − Σ pᵢ²`, for a set of class counts. |
| `gini_split(parent, left, right)` | Scores a candidate split as the size-weighted average of the children's Gini impurities. |
| `data_split(data, threshold, dim)` | Partitions the points into two sets on `point[dim] <= threshold`. |

## The data

The notebook works on a tiny hand-made dataset of 2D points in two classes:

```python
data = {
    'A': [(0, 0), (0, 1), (1, 0), (1, 1)],
    'B': [(0, 2), (2, 2), (2, 0)]
}
```

## Worked results

Running the notebook's examples gives:

- `count_of_class(data)` → `{'A': 4, 'B': 3}`
- `gini_index({'A': 4, 'B': 3})` → `0.4898`
- `gini_split({'A': 4, 'B': 3}, {'A': 0, 'B': 2}, {'A': 4, 'B': 1})` → `0.2286`
- `data_split(data, 1.5, 0)` → left `{'A': [(0, 0), (0, 1), (1, 0), (1, 1)], 'B': [(0, 2)]}`, right `{'A': [], 'B': [(2, 2), (2, 0)]}`

The split example shows the idea in action: thresholding the first coordinate at 1.5 isolates class B's two points at `x = 2` on the right while keeping everything else on the left, and the weighted Gini score of `0.2286` (down from the parent's `0.4898`) quantifies the impurity reduction.

## How to Run

Open `decision_tree_from_scratch.ipynb` in Jupyter or Google Colab and run the cells top to bottom. No packages are required — the notebook uses only built-in Python.

```bash
jupyter notebook decision_tree_from_scratch.ipynb
```

## Notes

The notebook contains two equivalent definitions of `gini_index` (an early draft and a tidier rewrite); the later one takes effect. Both compute the same value, so the results are unaffected.

## Files

```
├── README.md
├── LICENSE
├── decision_tree_from_scratch.ipynb   # the notebook
└── notebooks/
    └── Decision_Tree_Colab_Printout.pdf   # printable Colab export of the notebook
```

## License

MIT — see [LICENSE](LICENSE).
