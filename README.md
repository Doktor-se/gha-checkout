# gha-checkout

If you are working in a private organisation which uses submodules and/or private github actions its a hassle to checkout.

This is a reusable composite action to reduce copy pasta in your workflows.

This action will (depending on inputs) checkout the appropriate things. If you are using

# Deprecation
Private actions can now be used internally in private organisations.

If you don't need submodules update your checkout to just

```yaml
    - uses: actions/checkout@v3
```

If you need submodules update your workflow to use the normal checkout action

```yaml
    - name: Checkout
      uses: actions/checkout@v3
      with:
        token: ${{ secrets.<secret name> }}
        submodules: true
```


# V3

Uses the same github token to checkout repo, actions, and submodules.
`fetch-depth` can be set, defaults to 1, shallow checkout.

```yaml
name: CI
on: pull_request

jobs:
  hello-world:
    - uses: doktor-se/gha-checkout@v3
      with:
        token: ${{ secrets.GITHUB_PAT }}

    - uses: ./.github/composite-actions/some-private-action

    - run: echo "hello world"
```

# V2

V2 does a shallow checkout of the submodule

If `submodules_key` is not set, submodules will be skipped.
If `actions_key` is not set, private actions will be skipped.


```yaml
name: CI
on: pull_request

jobs:
  hello-world:
    - uses: doktor-se/gha-checkout@v2
      with:
        submodules_key: ${{ secrets.SSH_SUBMODULES_KEY }}
        actions_key: ${{ secrets.SSH_ACTIONS_KEY }}

    - uses: ./.github/composite-actions/some-private-action

    - run: echo "hello world"
```
# V1

V1 does a full checkout of the submodule

If `submodules_key` is not set, submodules will be skipped.
If `actions_key` is not set, private actions will be skipped.


```yaml
name: CI
on: pull_request

jobs:
  hello-world:
    - uses: doktor-se/gha-checkout@v1
      with:
        submodules_key: ${{ secrets.SSH_SUBMODULES_KEY }}
        actions_key: ${{ secrets.SSH_ACTIONS_KEY }}

    - uses: ./.github/composite-actions/some-private-action

    - run: echo "hello world"
```
