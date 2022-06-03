# 6. Processes must include a when block

Date: 2022-01-01

## Status

Accepted

## Context

With the [nf-core modules](https://nf-co.re/modules) and in future [subworkflows](https://github.com/nf-core/modules/tree/master/subworkflows/nf-core), we aim to provide well maintained building blocks for anyone's pipeline. Different pipelines have different criteria for whether or not a process should run. We want to provide ways to configure modules that are independent of specific pipeline parameters.

## Decision

Every process must include a [`when` block](https://www.nextflow.io/docs/latest/process.html#when) with the following content.

```groovy
when:
task.ext.when == null || task.ext.when
```

## Consequences

The above condition means that by default every process will run. It is only when pipeline developers configure other conditions for `task.ext.when` that things get more interesting. This is an alternative mechanism to using [`if`](https://www.nextflow.io/docs/latest/script.html#conditional-execution) statements or [channel branching](https://www.nextflow.io/docs/latest/operator.html#branch) logic. The benefit is that it can be set in a configuration and thus does not necessarily depend on specific pipeline parameters that would hinder the adoption of nf-core modules in pipelines. Furthermore, unlike other conditional logic, processes disabled by `when` do not appear in the nextflow log output.

A disadvantage is that the logic for when a process runs is not immediately clear from a workflow definition but requires checking configuration files as well (typically in a pipeline's `conf/modules.config`). We thus recommend extensive comments in a workflow if this mechanism is used.
