# ProsperoAI Pro (unofficial build)

An **unofficial** build of [ProsperoAI](https://github.com/blackbearreloaded/ProsperoAI)
by BlackBearReloaded, tuned for the **PS5 Pro**. It is not made, endorsed or
supported by the ProsperoAI author: report problems with this build to
https://github.com/obl1vn/ProsperoAI/issues, not upstream.

Source: the `ps5pro` branch of https://github.com/obl1vn/ProsperoAI
(ProsperoAI 01.005.000 plus the changes below). License: GPL-3.0-or-later, like
ProsperoAI.

## What is different

| Change | Effect on a PS5 Pro (Mistral 7B Q4_0) |
| --- | --- |
| llama.cpp mat-vec tuning (`vulkan_env.txt`) | faster generation |
| batch/ubatch 512 (`batch_size.txt`, `ubatch_size.txt`) | faster prompt reading |
| fewer interface frames while a model writes (`ui_sleep_ms.txt`) | faster generation |
| Pro memory mode (`param.json` attribute3 bit 22) | 12.63 GiB for models instead of 11.44 GiB |
| no update check | an official update would replace this build |

Together: **86.9 -> 96.6 tokens/s** generation and **692 -> 740 tokens/s**
prompt reading, measured on a PS5 Pro, firmware 13.60. Details:
https://github.com/obl1vn/Unlock-ps5-pro-memory

Only Mistral 7B Q4_0 has been measured; other models use the same settings but
were not benchmarked. Not tested on a base PS5.

## Install

It uses the same title ID as ProsperoAI (`PPSA99004`) and replaces it:

1. Delete the old `/data/homebrew/PPSA99004` (models in `/data/prosperoai/models`
   stay).
2. Upload this folder as `/data/homebrew/PPSA99004`.
3. Register it again in your homebrew loader and launch **ProsperoAI Pro (unofficial)**.

To go back to the official app, install the official release the same way.

## Settings

All files sit next to `eboot.bin` and are read when the app starts:

- `vulkan_env.txt`: llama.cpp / ggml-vulkan switches (see `docs/PS5_PRO_TUNING.md`
  in the source).
- `ui_sleep_ms.txt`: pause after each interface frame while a model writes,
  0-1000 ms; `0` draws every frame like the official app.
- `batch_size.txt`, `ubatch_size.txt`: prompt batch sizes.
