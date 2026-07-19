# CodeRabbit organization configuration

This repository provides the central CodeRabbit configuration for repositories
in the `sjunepark` GitHub account. Repositories without a local
`.coderabbit.yaml` use the defaults in [`.coderabbit.yaml`](./.coderabbit.yaml).

## Customize a repository

To override selected settings while retaining the organization defaults, add a
`.coderabbit.yaml` at the root of the individual repository with
`inheritance: true`:

```yaml
# yaml-language-server: $schema=https://coderabbit.ai/integrations/schema.v2.json

inheritance: true

reviews:
  profile: chill
  path_instructions:
    - path: "src/api/**"
      instructions: "Ensure backward compatibility."
```

Inheritance is disabled by default. If a repository adds `.coderabbit.yaml`
without `inheritance: true`, its configuration stops the inheritance chain and
does not merge with this central file.

When inheritance is enabled:

- Repository scalar values override central values.
- Nested objects are merged.
- Arrays keep repository items first, followed by unique central items.

## Review workflow

Automatic reviews are disabled by default. Add the `coderabbit-review` label to
a pull request to request a review. Later pushes are not reviewed
automatically; comment `@coderabbitai review` to request another review.

### Who can trigger a review

- Only the repository owner and invited collaborators can manage labels on a
  personal-account repository. Ordinary external contributors cannot apply
  `coderabbit-review`.
- An invited collaborator can apply the label and trigger a review.
- `chat.allow_non_org_members: false` is configured, but CodeRabbit documents
  this restriction only for GitHub organization repositories. Repositories
  owned by the personal `sjunepark` account should not rely on it to block
  external comment interactions.
- Use an organization-owned repository when restricting comment commands to
  organization members is required.

To inspect the effective configuration and the source of each value, comment
the following on a pull request:

```text
@coderabbitai configuration
```

## Dashboard settings

Inheritance applies at every configuration level. This central file currently
does not set `inheritance: true`, so ordinary repository and organization UI
settings below it are not merged into the effective configuration. CodeRabbit
global overrides remain higher priority and still apply.

If organization UI settings should fill values omitted by the central file, add
`inheritance: true` to this repository's `.coderabbit.yaml` as well.

## Documentation

- [Central configuration](https://docs.coderabbit.ai/configuration/central-configuration)
- [Configuration inheritance](https://docs.coderabbit.ai/configuration/configuration-inheritance)
- [Configuration reference](https://docs.coderabbit.ai/reference/configuration)
