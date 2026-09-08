# Digital Tissue Deconvolution of a Cutaneous Squamous Cell Carcinoma Section

Exploratory analysis of a spatial transcriptomics section using cell-type deconvolution,
carried out as an internship project for M.Bio.310 Systems Biology (Summer 2026,
Georg-August-Universität Göttingen).

**Author:** Zeynep Sude KIRLI

## Summary

Eleven cell types were quantified in each of 604 spots of a cutaneous squamous cell
carcinoma section using Digital Tissue Deconvolution, with a single-cell reference
assembled from three patients of the same study. Clustering the resulting compositions
gave four spatial niches which, although the model uses no positional information, form
contiguous territories arranged along an axis from tumor to inflamed stroma. Two of them
correspond to structures described in the original publication.

## Repository contents

| Path | Description |
|---|---|
| `spatial_deconvolution.ipynb` | Full analysis |
| `figures/` | Figures produced by the notebook |
| `requirements.txt` | Package versions |

## Data

The data are not included in this repository because of their size. Both datasets are
public and come from Ji et al., *Cell* 2020, 182(2):497–514.e22
([doi:10.1016/j.cell.2020.05.039](https://doi.org/10.1016/j.cell.2020.05.039)).

**Spatial section** — sample GSM4284317 (`P2_ST_rep2`), GEO series
[GSE144239](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE144239), obtained
through the STOmicsDB entry
[STDS0000001](https://db.cngb.org/stomics/datasets/STDS0000001), accessed 10 August 2026.

**Single-cell reference** — GEO series
[GSE144236](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE144236), files
`merge10pts_counts.txt` and `patient_metadata_new.txt`.

## Running the analysis

```bash
pip install -r requirements.txt
jupyter lab
```

Run the notebook from top to bottom. A fixed random seed of 42 is used for every
stochastic step, so the results are reproducible.

## Analysis overview

1. **Curation** — MAD-based quality thresholds, no upper bound on library size,
   normalization to 10,000 counts per spot. 604 of 646 spots and 14,889 of 16,962 genes
   retained.
2. **Reference** — level-1 annotation, cell types below 100 cells excluded, each type
   subsampled to at most 5,000 cells. 11 cell types, 10,047 cells.
3. **Deconvolution** — Deconomix, 1,000 artificial mixtures, 1,000 iterations.
4. **Downstream** — *k*-means niche clustering (*k* = 4), neighbourhood validation,
   Wilcoxon differential expression, over-representation analysis against GO Biological
   Process 2023 and Reactome 2022.

## Method

Görtler F, et al. Loss-Function Learning for Digital Tissue Deconvolution.
*J Comput Biol* 2020;27(3):342–355.
[doi:10.1089/cmb.2019.0462](https://doi.org/10.1089/cmb.2019.0462)

Mensching-Buhr M, et al. Deconvolution of omics data in Python with Deconomix.
*bioRxiv* preprint.
[doi:10.1101/2024.11.28.625894](https://doi.org/10.1101/2024.11.28.625894)

## License

Code released under the MIT License. The underlying data belong to the original authors
and are subject to their terms.
