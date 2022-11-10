# elasticsearch-kibana-docker-boilerplate

## Troubleshooting

### Elasticsearch fails to start using Docker: Max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]

You need to increase the value of vm.max_map_count with `sysctl -w vm.max_map_count=262144`.

On Windows, if you are using WSL (which should be the case with Docker Desktop), you can run `wsl -d docker-desktop`, followed by `sysctl -w vm.max_map_count=262144`.

To persist this change, you can add `vm.max_map_count = 262144` to `/etc/sysctl.conf` in WSL. I.e. for Docker Desktop on Windows with a WSL backend, you can run `wsl -d docker-desktop --exec sh -c "echo 'vm.max_map_count = 262144' >> /etc/sysctl.conf"` to persist this setting. See https://stackoverflow.com/a/66547784/1334688.

Try this fix even if you cannot locate the error message above - it may be burried somewhere in the logs.