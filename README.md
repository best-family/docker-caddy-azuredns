[![Latest Release][version-image]][version-url]
[![Docker Build][gh-actions-image]][gh-actions-url]

# docker-caddy-azuredns

A Caddy Server Docker container with the [Azure DNS Provider](https://caddyserver.com/docs/modules/dns.providers.azure).

Based heavily on the code at [https://github.com/SlothCroissant/caddy-cloudflaredns](https://github.com/SlothCroissant/caddy-cloudflaredns)

Builds are available at the following Docker repositories:

* GitHub Container Registry: [https://ghcr.io/best-family/docker-caddy-azuredns](https://ghcr.io/best-family/docker-caddy-azuredns)

Few things to note:

1. You should add Azure client related values as environment variables to your docker run command. Example:

      ```
      docker run -it --name caddy \
          -p 80:80 \
          -p 443:443 \
          -v caddy_data:/data \
          -v caddy_config:/config \
          -v $PWD/Caddyfile:/etc/caddy/Caddyfile \
          -e AZURE_TENANT_ID=00000000-0000-0000-0000-000000000000 \
          -e AZURE_CLIENT_ID=00000000-0000-0000-0000-000000000000 \
          -e AZURE_CLIENT_SECRET= \
          -e AZURE_SUBSCRIPTION_ID=00000000-0000-0000-0000-000000000000 \
          -e AZURE_RESOURCE_GROUP_NAME= \
          -e ACME_AGREE=true \
          best-family/docker-caddy-azuredns:latest
      ```

2. You should add the following to your Caddyfile as the [tls directive](https://caddyserver.com/docs/caddyfile/directives/tls#tls).

   ```
    tls {
      dns azure {
        tenant_id {$AZURE_TENANT_ID}
        client_id {$AZURE_CLIENT_ID}
        client_secret {$AZURE_CLIENT_SECRET}
        subscription_id {$AZURE_SUBSCRIPTION_ID}
        resource_group_name {$AZURE_RESOURCE_GROUP_NAME}
      }
    }
   ```

[version-image]: https://img.shields.io/github/v/release/best-family/docker-caddy-azuredns?branch=main&style=for-the-badge
[version-url]: https://github.com/best-family/docker-caddy-azuredns/releases

[gh-actions-image]: https://img.shields.io/github/actions/workflow/status/best-family/docker-caddy-azuredns/main.yaml?branch=main&style=for-the-badge
[gh-actions-url]: https://github.com/best-family/docker-caddy-azuredns/actions
