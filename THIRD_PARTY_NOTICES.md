# Third-Party Notices

<<<<<<< HEAD
OverDrive is distributed under the MIT License (see `LICENSE`). The application
**bundles and redistributes** several third-party programs as native executables under
`lib/arm64-v8a/` in the APK (they are packaged as `lib*.so` but are standalone binaries,
run as separate processes — see `app/tunnel-binaries.lock`). Redistributing them carries
obligations that MIT does not, and this file exists to meet them.

> **⚠️ sing-box is licensed under the GNU GPL v3.** Bundling a GPL-3 binary into this
> otherwise-MIT application has consequences the other three do not — see the dedicated
> section below. This file records the attribution required for redistribution; it does
> **not** by itself resolve the GPL-3 compatibility question.

| Component | Upstream | License |
|---|---|---|
| tailscale (`libtailscale.so`) | tailscale/tailscale | BSD-3-Clause |
| cloudflared (`libcloudflared.so`) | cloudflare/cloudflared | Apache-2.0 |
| zrok (`libzrok.so`) | openziti/zrok | Apache-2.0 |
| sing-box (`libsingbox.so`) | sagernet/sing-box | **GPL-3.0-or-later** |

Exact upstream versions, commits and digests for each are pinned in
`app/tunnel-binaries.lock`.

---

## tailscale — BSD-3-Clause

Copyright (c) 2020 Tailscale Inc & contributors.

```
BSD 3-Clause License

Copyright (c) 2020 Tailscale Inc & contributors.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this
   list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright notice,
   this list of conditions and the following disclaimer in the documentation
   and/or other materials provided with the distribution.

3. Neither the name of the copyright holder nor the names of its
   contributors may be used to endorse or promote products derived from
   this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE
FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
```

---

## cloudflared — Apache License 2.0

Copyright Cloudflare, Inc. Licensed under the Apache License, Version 2.0. The full
license text is reproduced in `LICENSES/Apache-2.0.txt`. OverDrive redistributes the
official upstream `cloudflared-linux-arm64` release binary unmodified (aside from UPX
packing and stripping — see `app/tunnel-binaries.lock`); no source changes are made.

## zrok — Apache License 2.0

Copyright NetFoundry, Inc. and the OpenZiti project. Licensed under the Apache License,
Version 2.0 (full text in `LICENSES/Apache-2.0.txt`). OverDrive redistributes the official
upstream `zrok_*_linux_arm64` release binary unmodified (aside from UPX packing and
stripping).

---

## sing-box — GNU General Public License v3.0-or-later

Copyright (C) 2022 by nekohasekai <contact-sagernet@sekai.icu>

sing-box is Free Software under the GPL v3 (or later). The full license text is in
`LICENSES/GPL-3.0.txt`. Per §4 of the sing-box license, no derivative work may use its
name or imply association without prior consent.

**This is a redistribution-compliance record, not a resolution.** The GPL is copyleft:
conveying a GPL-3 binary as part of a larger work has requirements — including a written
offer of the binary's *corresponding source* and constraints on the license of the
conveyed whole — that are in tension with this application's MIT license and its shipped
APK. That question is tracked upstream and must be resolved by the project, not papered
over by this file. Corresponding source for the exact binary shipped:
https://github.com/sagernet/sing-box (tag pinned in `app/tunnel-binaries.lock`).
=======
OverDrive's own source code is licensed under the MIT License (see [LICENSE](LICENSE)).
The MIT license applies **only** to OverDrive's own code. The application bundles and
distributes the third-party components listed below, each of which remains under its
own license — those licenses, not MIT, govern those components.

## Bundled native binaries (`app/src/main/jniLibs/`)

| Component | Upstream | Version | License | Modified? |
|-----------|----------|---------|---------|-----------|
| cloudflared | https://github.com/cloudflare/cloudflared | based on 2025.7.0 | Apache-2.0 | **Yes** — see "Modifications" below |
| zrok | https://github.com/openziti/zrok | based on v1.1.x | Apache-2.0 | **Yes** — see "Modifications" below |
| sing-box | https://github.com/SagerNet/sing-box | see upstream | **GPL-3.0-or-later** | No |
| tailscale | https://github.com/tailscale/tailscale | see upstream | BSD-3-Clause | No |

## Machine-learning models (`app/src/main/assets/models/`)

| Component | Upstream | License |
|-----------|----------|---------|
| YOLO11n (`yolo11n.tflite`) | https://github.com/ultralytics/ultralytics | **AGPL-3.0** |

## Native libraries linked into the app

| Component | Upstream | License |
|-----------|----------|---------|
| OpenCV | https://github.com/opencv/opencv | Apache-2.0 |
| OpenH264 | https://github.com/cisco/openh264 | BSD-2-Clause |
| TensorFlow Lite | https://github.com/tensorflow/tensorflow | Apache-2.0 |

## Modifications (Apache-2.0 §4(b) notice of changes)

The following components were modified from their upstream sources:

- **cloudflared** — added a proxy-aware edge dialer that routes the tunnel's edge
  connection through a SOCKS5/HTTP proxy read from the environment
  (`edgediscovery/dial.go`). This lets the tunnel operate on restricted networks.
- **zrok** — added a SOCKS5 proxy and DNS override path for Android / restricted
  networks, selected via the `ALL_PROXY` / `HTTPS_PROXY` / `HTTP_PROXY` environment
  variables (`cmd/zrok/main.go`).

## Source-derived work

- **Bangcle / white-box AES port** — derived from reverse-engineering work by
  [Niek/BYD-re](https://github.com/Niek/BYD-re) and
  [jkaberg/pyBYD](https://github.com/jkaberg/pyBYD).

## Corresponding source (copyleft components)

**sing-box** is licensed under **GPL-3.0-or-later** and **YOLO11n** under **AGPL-3.0**.
Their complete corresponding source (including any modifications, if applicable) is
available from the upstream projects linked above.

**Written offer:** for three years from the date of distribution, the maintainer will,
on request, provide the complete corresponding source code for the GPL-3.0 and AGPL-3.0
components as bundled in any given OverDrive release. Contact the maintainer via the
channels in [SECURITY.md](SECURITY.md) or the [Discord server](https://discord.gg/PZutk9fg4h).

The full text of each license (GPL-3.0, AGPL-3.0, Apache-2.0, BSD-2-Clause,
BSD-3-Clause) is available from the respective upstream repositories.
>>>>>>> upstream/main
