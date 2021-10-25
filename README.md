## What

[setup-signore](https://github.com/hashicorp/setup-signore) reimagined as a composite GitHub Action that copies the [signore](https://github.com/hashicorp/signore) binary from a Docker image to the local disk

## Why

- the current implementation of the setup-signore GitHub Action requires users to supply a GitHub
personal access token - this version automatically uses the `GITHUB_TOKEN` vended to a running Action to
authenticate to the GitHub container registry (ghcr.io)
- the current implementation of the setup-signore GitHub Action allows users to supply client-id and
  client-secret values, and writes them to disk. This is not ideal for a number of reasons.

## How

Add a step to your workflow like so:

```
    steps:
      - name: install signore
        uses: hashicorp/setup-signore-test@v1
```

With no inputs, the `GITHUB_TOKEN` is passed automatically, and a default version of `signore` is used.

Optionally, `token`, `version`, and `signer` can be set:

```
    steps:
      - uses: hashicorp/setup-signore-test@v1
        with:
          version: v0
          signer: test_signer
          token: ${{ secrets.GITHUB_TOKEN }}
```