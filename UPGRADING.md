# Upgrading versions

The following places need updates for new versions of docker and buildkite:

 * [scripts/list.sh](scripts/list.sh) - Add new versions of docker
 * [scripts/build.sh](scripts/build.sh) - Add new versions of docker-compose to `docker_compose_version_from_docker`
 * [alpine/Dockerfile](alpine/Dockerfile) - Check if Alpine has a docker revision > r0
 * [README.md](README.md) - Update the latest docker tag in docs
