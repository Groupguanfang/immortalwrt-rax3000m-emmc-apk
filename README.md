# ImmortalWrt 25.12.2 for CMCC RAX3000M eMMC

This repository builds an ImmortalWrt 25.12.2 image for the legacy
RAX3000M eMMC partition layout used by Kwrt:

- `kernel`: 64 MiB
- `rootfs`: 600 MiB
- root device: `PARTLABEL=rootfs`
- board ID: `cmcc,rax3000m-emmc`

The build keeps the existing GPT and U-Boot recovery page. It produces a
traditional `sysupgrade.bin` containing separate kernel and rootfs payloads.
The package manager is APK, as provided by ImmortalWrt 25.12.2.

The image also builds and installs:

- UA3F 3.7.0 with its matching iptables/ipset/NFQUEUE kernel modules
- OpenClash with the Firewall4/nftables dependency set
- BTF/eBPF, cgroup, TC, NFQUEUE, TUN and inet-diag support required by honk

UA3F and OpenClash APK files are included in the workflow artifact. Honk
does not currently ship an OpenWrt package definition in its upstream
repository, so this image prepares and verifies its kernel prerequisites
without packaging an unverified service wrapper.

Do not use the upstream `cmcc_rax3000m` `sysupgrade.itb` image on this legacy
layout.

## Build

Run the **Build ImmortalWrt RAX3000M eMMC** workflow from GitHub Actions.
The resulting firmware and SHA-256 file are uploaded as a workflow artifact.

## Recovery

The known-good Kwrt recovery image remains the recommended fallback:

`kwrt-10.28.2026-mediatek-filogic-cmcc_rax3000m-emmc-squashfs-sysupgrade.bin`
