# 7. Record tool versions in a YAML file

Date: 2022-01-01

## Status

Accepted

## Context

With nf-core, we want to facilitate reproducibility and enable good practices when it comes to pipeline reporting. An important element of this is a clear overview on what tools were used and which versions of them. It is true that a pipeline's state - given by a version (git tag) or a git commit - in combination with the defined container images provides the most accurate account of the tools and their versions, however, looking up that information is cumbersome and not suitable for human consumption.

## Decision

Every process must generate and emit a YAML file that records the versions of the relevant tools used in the process. The output shall be defined as

```groovy
output:
path 'versions.yml', emit: versions
```

## Consequences

We can aggregate the versions recorded by all the process in a pipeline and provide an overview that is ideal for a report or academic paper. In order for this to work properly, we need to parse tool versions in every process, for example, with the below bash snippet which should be placed in the `script` block of the process.

```bash
cat <<-END_VERSIONS > versions.yml
"${task.process}":
    samtools: \$(echo \$(samtools --version 2>&1) | sed 's/^.*samtools //; s/Using.*\$//' ))
END_VERSIONS
```

For tools that do not provide an output of their version, this may be hardcoded to the version provided in the container image. Define a `VERSION` variable within the module but outside of the process definition as shown below.

```groovy
def VERSION = '1.4.1'

process {
    ...

    script:
    """
    cat <<-END_VERSIONS > versions.yml
    "${task.process}":
        samtools: $VERSION
    END_VERSIONS
    """
}
```
