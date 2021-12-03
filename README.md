# private-checkout

If you are working in a private organisation which uses submodules and/or private github actions its a hassle to checkout.

This is a reusable composite action to reduce copy pasta in your workflows.

This action will (depending on inputs) checkout the appropriate things. If you are using

If `submodules_key` is not set, submodules will be skipped.
If `actions_key` is not set, private actions will be skipped.


```yaml
name: CI
on: pull_request

jobs:
  hello-world:
    - uses: doktor-se/private-checkout@v1
      with:
        submodules_key: ${{ secrets.SSH_SUBMODULES_KEY }}
        actions_key: ${{ secrets.SSH_ACTIONS_KEY }}

    - uses: ./.github/composite-actions/some-private-action

    - run: echo "hello world"
```
