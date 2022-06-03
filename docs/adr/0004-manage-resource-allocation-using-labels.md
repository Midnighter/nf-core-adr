# 4. Manage resource allocation using labels

Date: 2022-01-01

## Status

Accepted

## Context

[Executors](https://www.nextflow.io/docs/latest/executor.html) require insight into the desired resources of a particular process in order to schedule the process execution correctly. Mostly, we are talking about the desired number of [CPUs](https://en.wikipedia.org/wiki/Central_processing_unit), memory, and time. These resources can be defined for a process using [directives](https://www.nextflow.io/docs/latest/process.html#directives) either in the process itself or using one of the configuration mechanisms, i.e., the [process scope](https://www.nextflow.io/docs/latest/config.html#scope-process), the [`withLabel`, or `withName` selectors](https://www.nextflow.io/docs/latest/config.html#process-selectors).

## Decision

We use labels to create categories of processes with the same resource needs. We will generally use the labels: `'process_low'`, `'process_medium'`, `'process_high'`, and some more specialized ones. The pipeline template contains a [base configuration](https://github.com/nf-core/tools/blob/master/nf_core/pipeline-template/conf/base.config) that defines the resources for these labels.

## Consequences

Using labels to configure resource needs, forms a nice middleground between optimizing each individual process in a pipeline and running all processes with the same default resources. One can then use these labels to quickly configure groups of processes either when creating a pipeline or when overriding defaults with a local configuration. If one wishes to modify the resource allocation of a particular process, it is probably best to use the `withName` selector.
