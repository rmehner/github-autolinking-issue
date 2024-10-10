# github-autolinking-issue

There seems to a bug with the packages not being linked to the repository in GitHub.
This tries to be a minimal example to reproduce the issue.

## Issue

When the docker image has the label `org.opencontainers.image.source=` with
a link to the repository, the packages are not connected to the repository. They should be though.
Without connecting, webhooks like `package.published` will not fire.

## Workaround

1. Manually connect the image to the repository.
2. Don't use buildx, but then you also lose the benefits of buildx, like the GitHub actions cache.
3. Disable [provenance](https://docs.docker.com/build/ci/github-actions/attestations/), as this makes the manifest available again.

## Branches

- `main` will publish https://github.com/users/rmehner/packages/container/package/github-autolinking-issue-main. The package is not connected, even though the label exists.
- `without-buildx` will publish https://github.com/rmehner/github-autolinking-issue/pkgs/container/github-autolinking-issue-without-buildx, where the connection works. [Commit with the changes](https://github.com/rmehner/github-autolinking-issue/commit/57c819f7b30ac7ecb83ae471d16f749d845104dc)
- `disable-provenance` will publish https://github.com/rmehner/github-autolinking-issue/pkgs/container/github-autolinking-issue-disable-provenance, where the connection also works. [Commit with the changes](https://github.com/rmehner/github-autolinking-issue/commit/2c6d2d3a230695bd76d9b58ab54dee75b72192e3)
