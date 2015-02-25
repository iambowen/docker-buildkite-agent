# buildkite-agent

This is a Docker image for running the [Buildkite](https://buildkite.com/) Agent, a small runner [written in golang](https://github.com/buildkite/agent) that waits for build jobs, executes them, and reports back their log and exit status.

Usage:

```bash
docker run -e BUILDKITE_AGENT_TOKEN=xxx buildkite/agent
```

* To run it as a background daemon, add `-d`.
* To enable debug output set `-e BUILDKITE_AGENT_DEBUG=true`.

And don't forget: because it's Docker, you can run as many parallel agents as your machine can handle.

## Docker-based builds

If you want to use buildkite-agent's Docker (so the build jobs themselves are run within self-contaned containers) you'll need to make Docker available inside the container. You can do this by linking in the binary and the unix socket like so:

```bash
docker run -e BUILDKITE_AGENT_TOKEN=xxx \
           -v /var/run/docker.sock:/var/run/docker.sock \
           -v `which docker`:/usr/bin/docker \
           buildkite/agent
```

If you're using Docker via a TCP socket (like boot2docker) then you'll need to set the `DOCKER_HOST` environment variable and expose the TCP socket in some way.

## Customising your agent image

The base image includes Ubuntu, git, the agent, and little else. If you want to add hooks, ssh keys, etc. you can easily extend the base image.

To add hooks simply copy them into `/hooks`:

```
FROM buildkite/agent

ADD hooks/* /hooks
```

If you need to test private code simply copy the relevant access credentials into the container, for example:

```
FROM buildkite/agent

ADD repo_access_rsa ~/.ssh/id_rsa
```

## Say Hi

Come and say hi in the #docker channel in the Buildkite Chat slack room!
