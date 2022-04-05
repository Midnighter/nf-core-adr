# 2. Input sample metadata

Date: ?

## Status

Accepted

## Context

In order to identify every piece of data going through a workflow as belonging
to a particular sample and to be able to derive secondary information, the best
approach seems to be, to attach those metadata as a Groovy
[`Map`](https://groovy-lang.org/groovy-dev-kit.html#Collections-Maps).

## Decision

As a rule, we include a Groovy [`Map`](https://groovy-lang.org/groovy-dev-kit.html#Collections-Maps) with sample metadata with every input. The input shall be named `meta` and provided to processes as the first element in a tuple, e.g.,

```groovy
input:
tuple val(meta), path(fastq)
```

The map must at least contain a sample identifier stored as a string under the key `id`. Other keys are pipeline dependent but often include the Boolean `single_end` which differentiates paired-end sequencing read FASTQ files.

## Consequences

Including metadata has the clear benefit of uniquely identifying what sample a piece of data is associated with. The metadata can also be used for various purposes by individual processes, such as naming files generated.

The downside of this approach is that our workflows always need to handle channels with tuples which makes operations on them more complex. Special care also has to be taken when modifying the metadata map and when joining on the map.
