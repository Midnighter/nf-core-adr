# 5. Require reproducible compute environments

Date: 2022-01-01

## Status

Accepted

## Context

One of the major goals of any pipeline manager and in particular nextflow is reproducibility. In nf-core we take this further because our templates provide an opinionated, standardized way for building pipelines. The current best practice for reproducible compute environments are containers. The most widely supported in bioinformatics being [Docker](https://www.docker.com/) and [Singularity/Apptainer](https://apptainer.org/). Since they are not necessarily supported on all compute infrastructure, we allow falling back to [conda](https://docs.conda.io/) but we discourage it because it is less isolated from the host system.

## Decision

In order to uphold our standards on reproducibility, every module submitted to [nf-core](https://nf-co.re/modules) must define a Docker and Singularity image with its dependencies. Unless absolutely impossible, those should be [BioContainers](https://biocontainers.pro/) images. In addition, conda dependencies coming from [conda-forge](https://conda-forge.org/) or [Bioconda](https://bioconda.github.io/) must be defined.

## Consequences

The path of least resistance is to use tools available from Bioconda or if they don't exist yet, [contribute a new recipe](https://bioconda.github.io/contributor/index.html) for a tool to Bioconda. Tools available from Bioconda are automatically made available as BioContainers images, as well as Singularity images. Creating such a recipe can be fairly involved and it will typically take a week from contributing a new recipe to Bioconda, it being reviewed, accepted, and the images built. It may take longer. This may seem tedious but we consider it an absolute necessity. Fortunately, both [Bioconda](https://gitter.im/bioconda/Lobby) and [BioContainers](https://gitter.im/biocontainers/Lobby) have very helpful communities.
