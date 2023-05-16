# Plex Media Server Helm Chart

This helm chart uses the [linuxserver/plex](https://hub.docker.com/r/linuxserver/plex)
docker images, which work for both amd64 and arm64 architectures.
Plex runs as an unprivileged container by default, as `user:group`
`1000:1000`.

The following custom values have been added:

| value                                   | default                                        | purpose                                                                                                                                                     |
| --------------------------------------- | ---------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `plex.hostname`                         | `plex`                                         | Sets the hostname inside the docker container. For example will set the servername to PlexServer. Not needed in Host Networking (`service.type: HostPort`). |
| `plex.claim.secret`                     |                                                | Name of the secret containing the claim token from [https://plex.tv/claim]. These tokens expire after 4 minutes.                                            |
| `plex.claim.key`                        |                                                | Key in the secret containing the claim value.                                                                                                               |
| `plex.claim.value`                      |                                                | Alternative, but insecure method of providing the claim value.                                                                                              |
| `plex.features.{feature}.enabled`       | `false`                                        | Expose additional ports on the `Service` to enable  the `{feature}`, which are `DLNA`, `homeTheater`, `bonour`, `roku`, and `gdm`.                          |
| `plex.features.DLNA.portUDP`            | `31900`                                        | The UDP port for the DLNA service.                                                                                                                          |
| `plex.features.DLNA.portTCP`            | `32469`                                        | The TCP port for the DLNA service.                                                                                                                          |
| `plex.features.homeTheater.port`        | `30005`                                        | The port for the Plex Home Theater via Plex Companion.                                                                                                      |
| `plex.features.bonjour.port`            | `5353`                                         | The port for the Bonjour/Avahi network discovery.                                                                                                           |
| `plex.features.roku.port`               | `8324`                                         | The port for the Plex for Roku via Plex Companion.                                                                                                          |
| `plex.features.roku.gdm.ports.gdm{1-3}` | `32410`, `32412`, `32413`, `32414`             | Ports for the GDM network discovery.                                                                                                                        |
| `volumes.{type}.enabled`                | `false`                                        | Enable the creation of a Persistent Volume Claim for `{type}`, which are `root`, and `media`.                                                               |
| `volumes.{type}.size`                   | `false`                                        | Size of the volume claim.                                                                                                                                   |
| `volumes.{type}.className`              | `false`                                        | Class name to define the type of PVC.                                                                                                                       |
| `certificate.enabled`                   | `false`                                        | Enable the creation of a cert-manager `Certificate` for the ingress resource.                                                                               |
| `certificate.domain`                    | `chart-example.local`                          | The domain for the certificate. Should match (one of) the ingress host names.                                                                               |
| `certificate.issuerRef`                 | `{name: letsencrypt,     kind: ClusterIssuer}` | The issuer reference.                                                                                                                                       |
