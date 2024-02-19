# My Isso Docker Images

This is a personal repository that builds Docker instances of the [Isso commenting system](https://github.com/posativ/isso/), used on <https://alexn.org>.

Notes to self for upgrading the Docker builds:

1. Sync with upstream (e.g., on GitHub tap the "Sync fork" button);
2. All pushes on master will build the Docker images, using the [Deploy](https://github.com/alexandru/isso/actions/workflows/Deploy.yml) action.

Current `docker-compose.yaml` configuration:

```yaml
  isso:
    container_name: isso
    image: 'ghcr.io/alexandru/isso:latest'
    restart: always
    healthcheck:
      test: ['CMD-SHELL', 'wget -q --spider --proxy=off http://localhost:8080/alexn/?uri=test&limit=10&nested_limit=5 || exit 1']
    ports:
      - "5544:8080"
    tty: true
    networks:
      - external_network
    environment:
      ISSO_SETTINGS: "/etc/isso/alexn.org.cfg;/etc/isso/monix.io.cfg"
    volumes:
      - /var/lib/isso:/var/lib/isso
      - /etc/isso:/etc/isso
    command: isso.dispatch
```
