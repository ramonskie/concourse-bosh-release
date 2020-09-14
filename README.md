# concourse-bosh-release

> A [BOSH](https://bosh.io) release for the `concourse` binary.

This repository contains the official BOSH release of
[Concourse](https://concourse-ci.org). It packages up the `concourse` binary
and exposes all flags via properties on the `web` and `worker` jobs. These jobs
represent the [`web` node](https://concourse-ci.org/concourse-web.html) and the
[`worker` node](https://concourse-ci.org/concourse-worker.html), respectively.


## Requirements

- [Bosh CLI V2](https://bosh.io/docs/cli-v2.html#install)


## Usage

Check out the [`concourse-bosh-deployment`
repository](https://github.com/concourse/concourse-bosh-deployment) repository
for a stub manifest and various ops files.

If you're not familiar with BOSH, you may want to check out the [BOSH
documentation](https://bosh.io/docs/) first.

If you're just looking to get Concourse running quickly and kick the tires, you
may want to try the [Quick Start](https://concourse-ci.org/install.html)
instead.

## Developing

If you are adding new Concourse flags to one of the job specs you must run `scripts/generate-job-templates` to add the new flags to the job templates.

**Default values**

When adding a new Concourse flag, don't define a `default` value that mirrors a default set by the Concourse binary. 

Instead, mention the default in the description. This prevents the possibility of drift if the Concourse binary default value changes.

```
containerd.max_containers:
    env: CONCOURSE_CONTAINERD_MAX_CONTAINERS
    description: |
      Maximum container capacity. 0 means no limit. Defaults to 250.
```

We understand that the comment stating the binary's default can become stale. The current solution is a suboptimal one. It may be improved in the future by generating a list of the default values from the binary.

