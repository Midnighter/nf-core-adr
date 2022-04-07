# 3. Tag processes with sample identifiers

Date: ?

## Status

Accepted

## Context

From the nextflow documentation on [tagging processes](https://www.nextflow.io/docs/latest/process.html#tag):

> The `tag` directive allows you to associate each process execution with a custom label, so that it will be easier to identify them in the log file or in the trace execution report.

By default, nextflow tags process executions with the internal task identifier. This is a numeric, sequential identifier that has no particular meaning to us.

## Decision

Since we [pass around sample metadata to virtually all processes](0002-input-sample-metadata.md), we use the sample identifier as a tag, e.g.,

```groovy
process NAME {
    tag "$meta.id"

    ...
}
```

## Consequences

The sample identifier has meaning to us human operators. We can thus quickly see which samples passed and which samples cause an error. Additionally, we can now aggregate
metrics from the trace execution report on the sample identifier. There are no negative consequences as far as we can tell.
