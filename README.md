# nlm-ckn-paper-code

Code archive for v1.0 of **NLM-CKN: A trustworthy semantic knowledge network linking data-driven cell phenotypes to diseases and drugs**.

This repository records the exact version of the software used for the paper. Each component is a Git submodule fixed at a specific commit.

- **Paper:** Preprint under screening at bioRxiv. [Add citation and DOI when posted.]
- **Zenodo record:** [10.5281/zenodo.23407775](https://doi.org/10.5281/zenodo.23407775)
- **Knowledge network:** [nlm-ckn.org](https://nlm-ckn.org)

## Get the code

Clone this repository with its submodules:

```bash
git clone --recurse-submodules https://github.com/NIH-NLM/nlm-ckn-paper-code.git
```

The "Download ZIP" option on GitHub does not include submodule contents.

## Modules

Each module is a Git submodule in `software/`, fixed at the tag or commit shown. Each owner confirms the entries for their own modules.

| Module | Owner | Reference | Commit | Purpose |
|---|---|---|---|---|
| [cellxgene-harvester](https://github.com/NIH-NLM/cellxgene-harvester) | Anne Deslattes Mays | tag `v1.0` | `5544cf42eb523bce9fab356a2d4c74aa71c0e75e` | Selects datasets from CELLxGENE using ontology identifiers for tissue, disease, and age |
| [scsilhouette](https://github.com/NIH-NLM/scsilhouette) | Anne Deslattes Mays | tag `v1.0` | `20e2b979108f2bc53fc0be008ffa7bdf44bb5988` | Computes silhouette scores to assess clustering quality |
| [sc-nsforest-qc-nf](https://github.com/NIH-NLM/sc-nsforest-qc-nf) | Anne Deslattes Mays | tag `v1.0` | `d1fae1bafdd0b3d76b0bc2069e6df63f7aba19c6` | Runs NS-Forest marker gene discovery and silhouette quality control across datasets |
| [sc-nsforest-qc-nf, neocortex run](https://github.com/NIH-NLM/sc-nsforest-qc-nf/tree/neocortex-run) | Anne Deslattes Mays | branch `neocortex-run` | `5f2f0f3031c6a40beea98b24e08c1d53e54745ca` | Processes the Jorstad neocortex dataset |
| [sc-nsforest-qc-nf, retina run](https://github.com/NIH-NLM/sc-nsforest-qc-nf/tree/retina-run) | Anne Deslattes Mays | branch `retina-run` | `93d10d366659d2114159983b69a42426960d6c81` | Processes the Li retina dataset |
| [To be completed] | Matt Diller | [tag] | [commit] | [purpose] |
| [To be completed] | Raymond LeClair | [tag] | [commit] | [purpose] |
| [To be completed] | William Spear | [tag] | [commit] | [purpose] |

To add a module, use [`git submodule add`](https://git-scm.com/docs/git-submodule), check out the tag inside it, and open a pull request.

## Data workflows

### Runs

| Run | Datasets | Workflow | scsilhouette image | NS-Forest image |
|---|---|---|---|---|
| Main | 82 | `software/sc-nsforest-qc-nf` | `ghcr.io/nih-nlm/scsilhouette:1.5` | [digest] |
| Neocortex | Jorstad | `software/neocortex-run` | `ghcr.io/nih-nlm/scsilhouette:v1.0` | `ghcr.io/nih-nlm/sc-nsforest-qc-nf/nsforest:4c380184b7a60bbc7f26938b737130953a5b5982` |
| Retina | Li | `software/retina-run` | `ghcr.io/nih-nlm/scsilhouette:v1.0` | `ghcr.io/nih-nlm/sc-nsforest-qc-nf/nsforest@sha256:1b599d17f9639d99eb058bab5eb4b42a2f6b7616f0b047efc280e91e7956297b` |

### Why two datasets have their own runs

The paper's figures for these two datasets came from earlier analyses, so each dataset has its own documented process. Neither dataset went through the standard filtering used in the main run.

- **Neocortex (Jorstad):** NS-Forest was run on downsampled data. Silhouette scores were computed on each of the 5 superclusters, covering the entire dataset. Earlier work is available at [Zenodo DOI].
- **Retina (Li):** The run follows the 2024 analysis, which preserves the RPE65 result shown in the paper.

### Data

The h5ad input files are publicly available. Their URLs are listed in `[file name].csv` in the Zenodo record.

## How the workflows connect

1. `cellxgene-harvester` resolves tissue, disease, and age to ontology identifiers and writes them to JSON files. It uses these files to select datasets.
2. `sc-nsforest-qc-nf` uses the same JSON files to filter cells. It then runs NS-Forest and `scsilhouette`.
3. Workflow results are the input to the ETL process. [Raymond LeClair to describe.]

## Database schema

[Matt Diller to complete: repository, tag, commit, and purpose.]

## Extract, transform, load (ETL) and deployment

[Raymond LeClair to complete: repositories, tags, commits, and purpose.]

## User interface

[William Spear to complete: repositories, tags, commits, and purpose.]

## Citation

If you use this code, please cite the paper: [citation].

To cite this code, use the version DOI: [DOI].

## License

See [LICENSE](LICENSE). Each submodule is covered by the license in its own repository.
