# linux-op8

OnePlus 8 / OnePlus 8 T-Mobile (SM8250 "instantnoodle" / "instantnoodlep")
mainline kernel tree.

Based on **Linux 7.2.4** upstream with a device-support layer on top.

## Layout

- `5281b64` — Linux 7.2.4 (upstream baseline)
- `60d4ae1` — OnePlus 8 support layer (this branch)

## What's included (in the support commit)

| Component | File(s) | Upstream author / origin |
|---|---|---|
| Device tree | `arch/arm64/boot/dts/qcom/sm8250-oneplus-instantnoodle.dts`<br>`arch/arm64/boot/dts/qcom/sm8250-oneplus-instantnoodlep.dts` | Xiaoou `<xo666@postmarketos.org>` (postmarketOS) |
| Display panel | `drivers/gpu/drm/panel/panel-samsung-amb655x.c`<br>`drivers/gpu/drm/panel/panel-samsung-amb655uv01.c` | Caleb Connolly (postmarketOS) |
| Front camera | `drivers/media/i2c/imx471.c` | Eugene Lepshy, Luca Weiss |
| Speaker amplifier | `sound/soc/codecs/tfa9872.c` | Based on tfa9895.c (NXP) |
| Charger | `drivers/power/supply/qcom_pm8150b_charger.c` | Teguh Sobirin |
| Power supply API | `include/linux/power_supply.h` (`POWER_SUPPLY_PROP_CHARGING_ENABLED`) | pmOS |

All original SPDX copyright headers are preserved in the source files.

## USB-PD note

The sink PDO is limited to 5 V — `PDO_VAR(5000, 5000, 3000)` — instead of
upstream's `PDO_VAR(5000, 12000, 5000)`. On the OnePlus 8 the 12 V request
cannot actually be negotiated and removing the high-voltage request makes
PD charging behave correctly on the device.

## Building (Arch)

```
makepkg -A        # cross-compile from x86_64 using clang/LLVM
```

Produces `linux-oneplus8` and `linux-oneplus8-headers` aarch64 packages.
