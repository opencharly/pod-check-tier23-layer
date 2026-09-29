# pod-check-tier23-layer

The `check-tier23-layer` candy of the OpenCharly candy library, as a standalone
repo (the candy de-submodule cutover, kind-prefixed naming). It is a benchmark
fixture placing tier 2 + tier 3 in a shared pod.

## What it provides

- **Tier 2** — a Python HTTP server on port `8080` returning a body containing
  `charly benchmark`.
- **Tier 3** — `curl` installed plus a persistent `/srv/bench/version.txt`
  carrying `tier3-ok`.

Both tiers share the same pod (`harness-tier23`).

| Property | Value |
|---|---|
| Service | `bench-http` (`python3 -m http.server` on `8080`, priority 20) |
| Port | `8080` |
| Package | `curl`, `python3`, `iproute`, `procps-ng` (fedora) |
| Files | `/srv/bench/version.txt`, `/srv/bench/index.html` |

## How to use it

Compose the candy into the benchmark pod:

```yaml
harness-tier23:
  candy:
    base: cachyos.cachyos
    candy:
      - '@github.com/opencharly/pod-check-tier23-layer:<tag>'
```

## Layout

- `charly.yml` — the `check-tier23-layer` candy entity (description, `require`,
  `distro`, port, `service`, plan).
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning procedure: `/charly-image:layer` — candy authoring reference.
- `/charly-check:check` — the disposable-deploy R10 bed surface.
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
