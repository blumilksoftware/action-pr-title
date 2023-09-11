# PR title rules action

Github action to enforce Pull Request title conventions

## Usage

Default usage:

```yaml
steps:
- uses: blumilksoftware/action-pr-title@master
```

This will use default option values and enforce a title formatted as either `#123 - Some title` or `- Some title`.

You can customize the action by overriding default options:

```yaml
steps:
- uses: blumilksoftware/action-pr-title@master
  with:
    regex: '^(FOO\-\d+ )?- .+'
```

This will enforce a title formatted as either `FOO-123 - Some title` or `- Some title`.

See also [action.yml](./action.yml) for detailed list of options.

### Note

You might want to provide `types` field to the `pull_request` definition as by default workflows are triggered only
on `opened`, `synchronize`, or `reopened` events. Read more about
it [here](https://docs.github.com/en/free-pro-team@latest/actions/reference/events-that-trigger-workflows#pull_request).

```yaml
on:
  pull_request:
    types: [opened, edited, synchronize, ready_for_review, reopened]
```

Triggering the action on anything other than `pull_request` will cause a failure.

### Example workflow

`.github/workflows/check-pr-title.yml`:

```yaml
name: Check PR Title
on:
  pull_request:
    branches: [ "main" ]
    types: [opened, edited, synchronize, ready_for_review, reopened]

jobs:
  check-pr-title:
    name: Check PR title
    runs-on: ubuntu-20.04
    steps:
      - uses: blumilksoftware/action-pr-title@v1.2.0
```
