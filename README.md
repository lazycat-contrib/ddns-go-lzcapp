# DDNS-GO for LazyCat

- Upstream https://github.com/jeessy2/ddns-go, initial version 6.17.7. The old `jeessy/ddns-go` GitHub path is not the source repository.
- Official image is still `docker.io/jeessy/ddns-go:v6.17.7`; mirror delivery via `docker.1ms.run` requires matching source/runtime digests.
- Package `community.lazycat.app.ddns-go`, Linux amd64, minimum LazyCat OS 1.5.0.
- Native image entrypoint `/app/ddns-go` is retained. Command arguments set port 9876, interval 300 seconds and `/root/.ddns_go_config.yaml`; `/lzcapp/var/config` persists `/root`.

## Credentials and networking

The web UI retains native account setup and login behind LazyCat authentication. Create the first strong password within the upstream 30-minute initialization window, or restart the app to reopen initialization. No initial account, DNS-provider API key or real domain is provisioned.

Three-stage injection observes exact POST `/loginFunc` and `/save` only, and persists credentials only after HTTP 200 with JSON `Code: 200`. Upstream business errors also use HTTP 200, so HTTP status alone must never count as success. Blank passwords on a settings save do not erase the remembered password. Login selectors are the native `Username` and `Password` IDs. Autofill does not auto-submit.

Uses upstream-supported bridge networking, not host networking. Prefer public-IP HTTP discovery endpoints; a container interface address is not necessarily the host public IP. IPv6 needs a usable container egress and discovery endpoint. Actual provider secrets, domains and DNS changes remain user-controlled. TLS certificate verification remains enabled. No real DNS records are changed or probed during packaging.

The persistent YAML can contain provider credentials: protect configuration files and backups. No Docker socket, host-system directory or externally published host port is added.

## Publication

Reusable LazyCat workflow, versioned Release LPK. Automatic private and official publishers stay disabled; submit only the verified Release URL/SHA256 to MiaoMiao community store after full upstream/alias duplicate checks.

No file-chooser interceptor, smoke job or runtime gate. Configuration and synthetic injection-branch checks do not establish device startup, actual autofill, public-IP discovery or real DNS updates.
