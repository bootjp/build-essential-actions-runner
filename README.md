# Build-essential Actions runner

This image extends the [official GitHub Actions runner image](https://github.com/actions/runner/pkgs/container/actions-runner) with Ubuntu's `build-essential` and `pkg-config` packages for jobs that compile native code.

The runner base is pinned to a version and immutable digest. Renovate proposes base image updates for review. A successful build on `main` publishes `linux/amd64` images to `ghcr.io/bootjp/build-essential-actions-runner` under the `main` and `sha-<commit>` tags. Tags are lookup aids; pin deployments to a digest, for example `ghcr.io/bootjp/build-essential-actions-runner:main@sha256:<digest>`.

This is a container image, not GitHub's hosted `ubuntu-latest` VM image. Jobs can install language runtimes with `setup-go`, `setup-node`, or similar actions. The upstream runner user has passwordless `sudo` inside the container. Docker builds require a separate Docker daemon or sidecar; avoid mounting a host Docker socket for untrusted jobs.

The image has no default command. With Actions Runner Controller, configure the runner container command as `["/home/runner/run.sh"]` and provide runner registration through ARC. A plain `docker run` does not register a runner.
