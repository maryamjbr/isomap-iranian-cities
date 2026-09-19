# Isomap for Iranian Cities

A compact implementation of the Isomap dimensionality-reduction pipeline, applied to pairwise distances between Iranian cities and validated against scikit-learn.

The notebook builds a symmetric k-nearest-neighbor graph, estimates geodesic distances with Floyd-Warshall, and applies classical multidimensional scaling (MDS). The resulting two-dimensional embedding is then aligned and compared with `sklearn.manifold.Isomap`.

## Results

| Custom implementation | scikit-learn reference |
| --- | --- |
| ![Custom Isomap embedding of Iranian cities](custom_isomap.jpg) | ![scikit-learn Isomap embedding of Iranian cities](sklearn_isomap.png) |

After Procrustes alignment, the notebook reports a disparity of **`0.000000`** between the custom and scikit-learn embeddings. At six decimal places, the two methods therefore recover the same relative geometry up to translation, rotation, reflection, and scale.

## Method

1. Download and load the pairwise city-distance matrix.
2. Retain the five nearest neighbors of each city to form an undirected weighted graph.
3. Compute all-pairs shortest-path distances using Floyd-Warshall.
4. Apply classical MDS through double-centering and eigendecomposition.
5. Rotate and reflect the custom embedding for geographic readability.
6. Compare it with scikit-learn using Procrustes analysis.

## Repository contents

- `isomap_iranian_cities.ipynb` - executable implementation, plots, and comparison.
- `custom_isomap.jpg` - final custom Isomap visualization.
- `sklearn_isomap.png` - aligned scikit-learn visualization.
- `report-fa.pdf` - complete report in Persian, including the Isomap analysis and theoretical dimensionality-reduction questions.
- `report-fa.tex` - LaTeX source for the report; it references course-template files and fonts that are not included here.
- `requirements.txt` - Python dependencies needed to run the notebook.

## Run locally

Python 3.10 or later is recommended.

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
jupyter lab isomap_iranian_cities.ipynb
```

Run the notebook from top to bottom. Its first cells download `distances.csv` from the Google Drive file used for this project; the generated dataset file is ignored by Git.

## Implementation notes

- The graph and MDS pipeline are implemented explicitly for educational clarity.
- NumPy and SciPy provide numerical primitives, including eigendecomposition and the Floyd-Warshall shortest-path routine.
- The neighborhood size is fixed at `k = 5`, and the target embedding has two dimensions.
- The included notebook retains its saved plot outputs so the results are visible directly on GitHub.

## Report

The accompanying Persian-language report provides the derivation of classical MDS, an interpretation of the city embedding, the comparison with scikit-learn, and written answers covering PCA, covariance, SVD, reconstruction error, and feature scaling.
