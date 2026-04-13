# ngspice-builds

Pre-built [ngspice](https://ngspice.sourceforge.io/) binaries for
[Flux EDA](https://github.com/Flux-IC/flux-eda), compiled with **full BSIM4
model binning support** required by the SkyWater SKY130 PDK.

## Why this repo exists

The official SourceForge Windows builds of ngspice are compiled without BSIM4
binned model resolution, which causes `"could not find a valid modelname"`
errors when simulating sky130 MOSFETs. This repo produces properly-compiled
binaries via GitHub Actions CI.

## Downloads

See [Releases](https://github.com/Flux-IC/ngspice-builds/releases) for
pre-built binaries. Flux EDA downloads these automatically via
`tools/ngspice_update.py`.

## Supported platforms

| Platform | Binary | Status |
|----------|--------|--------|
| Windows x64 | `ngspice-{ver}-win64.zip` | CI built via MSYS2/MinGW |
| Linux x64 | `ngspice-{ver}-linux64.tar.gz` | CI built |
| macOS arm64 | `ngspice-{ver}-macos-arm64.tar.gz` | Planned |

## Building locally

```bash
# Windows (MSYS2 MINGW64 shell)
pacman -S mingw-w64-x86_64-gcc make autoconf automake libtool
./build-windows.sh

# Linux
sudo apt-get install build-essential autoconf automake libtool
./build-linux.sh
```

## Version policy

We track ngspice stable releases. When a new ngspice version is released:
1. Update `NGSPICE_VERSION` in the workflow
2. Push a tag `v{VERSION}` to trigger the CI build
3. Flux's `ngspice_update.py` picks up the new release automatically

## License

ngspice is distributed under the
[BSD 3-Clause License](https://sourceforge.net/p/ngspice/ngspice/ci/master/tree/COPYING).
This repo only contains build scripts and CI configuration.
