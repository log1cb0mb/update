# k0s Update Server - Reference implementation

This repo serves as k0s update server reference implementation. It provides the basic channels descriptions that is expected from an update server.

Essentially k0s autopilot assumes the folowing structure for update channels:

```text
channels/
    <channel-name>/
        index.yaml
```

Each the channel name can contain e.g. forward slashes so you can structure the channels for example like so:

```text
channels/
    stable/v1.28/
        index.yaml
    unstable/v1.28/
        index.yaml
```

Each channel `index.yaml` need to provide following information:

```yaml
channel: v1.27
eolDate: "2024-06-28"
version: 1.27.8+k0s.0
downloadURLs:
- arch: amd64
  os: linux
  k0s: https://github.com/k0sproject/k0s/releases/download/v1.27.0%2Bk0s.0/k0s-v1.27.0+k0s.0-amd64
  k0sSha256: deadbeef
  airgapBundle: someurlhere
  airgapSha256: deadbeef
- arch: arm64
  os: linux
  url: https://github.com/k0sproject/k0s/releases/download/v1.27.0%2Bk0s.0/k0s-v1.27.0+k0s.0-arm64
- arch: arm
  os: linux
  url: https://github.com/k0sproject/k0s/releases/download/v1.27.0%2Bk0s.0/k0s-v1.27.0+k0s.0-arm
- arch: amd64
  os: windows
  url: https://github.com/k0sproject/k0s/releases/download/v1.27.0%2Bk0s.0/k0s-v1.27.0+k0s.0-amd64.exe
```

So each channel can offer only single version to k0s autopilot client. In general the design pattern here is that each major.minor version will have their own channel where the latest patch release is offered.