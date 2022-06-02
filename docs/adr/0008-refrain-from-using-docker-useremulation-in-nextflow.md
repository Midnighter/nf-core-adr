# 8. Refrain from using docker userEmulation in Nextflow

Date: 2022-06-02

## Status

Accepted

## Context

There were multiple discussions over  the time around whether to utilize the `userEmulation` feature in Nextflow when using the `docker` scope as this both resolves issues with users running docker as root as well as causes issues for users with running any Spark based tool. 

## Decision

We made the decision to refrain from using the `userEmulation` feature to keep compatibility with the majority of users who might want to use Spark based tools. Docker can be configured in a way on the host system to enable running perfectly fine without userEmulation enabled.

## Consequences

This might affect users running Docker as root, who might generate output files that then are missing the right permissions for their regular user accounts to access these files. For those affected, there are several options available:

- Overwriting the docker configuration scope provided by default with nf-core pipelines
- Reconfiguring their Docker installation in a way that it does not run as root
- Switching to utilizing other options of containerization that are supported by nf-core, e.g. Singularity, Podman or Shifter. 
