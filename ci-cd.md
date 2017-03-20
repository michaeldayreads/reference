# Continuous Integration and Continuous Delivery

This document collects concepts, usage notes, and documentation references for CI/CD tools.

## concepts

### Continuous Integration

### Continuous Delivery

## by platform

### gitlab

#### .gitlab-ci.yaml reserved words

`image`  

A docker image. In this case, the one that defines the container for the jobs to be run.  

`services`

Docker services. These are additional docker images/containers that are made available to the primary testing image. The most common example is a database.

`stages`  

Define build stages.

`types`  an alias for `stages`  

`before_script`  

Commands that run before each job's script.

`after_script`  

Commands that run after each job's script.

`variables`  

Define build variables.

`cache`  

Define list of files that should be cached between runs.

#### Variables

GitLab Runner >= 0.5.0 passes all YAML defined variables to service containers.
