# automated pipelines

This document is an anchor for automated pipeline tools (gitlab, travis, jenkins etc.) and patterns associated with them.

## ENV VAR Index

| Use Case / Solution | GitLab |
|---------------------|--------|
| In pipeline Y/N | use `CI` or another [builtin variable](https://docs.gitlab.com/ee/ci/variables/predefined_variables.hmtl) |


## YAML syntax

Nodes can be repeated by first defining or _anchoring_ with `&label` and then _aliased_ or referenced using `*label`:

```yaml
define:
  - &label content
reference:
  - *label
```

Anchors are often used with `<<` to _merge maps_ of elements:

```yaml
define:
  - &label content
define-more:
  - &another more
reference:
  <<: *label
  <<: *another
```