Hello.

This is a fork of the "beats" repo from Elastic.

We would rather not have a fork of this code, but there are some issues that we can't work
around otherwise:

* We're not shipping to an Elastic (ELK) cluster, so we must use the "OSS" (open source) version
* The open source version isn't published in a public way to a Docker Hub that we know of
  https://container-registry-test-ui.elastic.co/r/beats/metricbeat-oss <- requires user/pass
* We need to run the beat within Docker, so we need to use the "hostfs" feature to make local
  resources available to metricbeat within the confines of the container.
* This is possible with a command line flag (`-e --hostfs=/hostfs`) but we're using Ansible
  to manage infrastructure and the provider does not expose a way to add command line args
  to the RUN command within the container.

So, these few commits are here to add "hostfs" as a config feature (as is the case in the "linux")
module.  And to publish the OOS container to somewhere we can use.

To build: `PLATFORMS=linux/amd64 BEATS=metricbeat make release`

