> **⚠️ This repository is no longer maintained.**
  > Development continues at [comfyui-cyberdelia-prompt-format](https://github.com/cyberdeliaAI/comfyui-cyberdelia-prompt-format) under the Cyberdelia AI Lab umbrella. Please install the new repo for the latest version and bugfixes.


# Prompt Format

A lightweight client-side prompt formatter for [AUTOMATIC1111](https://github.com/AUTOMATIC1111/stable-diffusion-webui) and [Forge](https://github.com/lllyasviel/stable-diffusion-webui-forge) that automatically cleans and normalizes your prompts on every generation.

No pip dependencies. Pure JavaScript. ~20 KB.

---

## Features

### Auto Format
Cleans up prompts automatically when you click **Generate** (or manually with the **Format** button):

- Normalizes spacing around commas, brackets, pipes, and colons
- Removes empty brackets `()` `[]`
- Prunes empty tag chunks
- Fixes misplaced commas inside/outside brackets
- Optionally appends commas at the end of each line (for multi-line prompts)

**Before:**
```
( masterpiece ),  best quality  ,  1girl ,   long hair,  ,  blue eyes  ,  ( dress  :1.3) ,
```

**After:**
```
(masterpiece), best quality, 1girl, long hair, blue eyes, (dress:1.3)
```

### Remove Duplicates
Strips repeated tags from your prompt. Supports custom **tag aliases** — for example, treating `girl`, `woman`, and `lady` as the same tag `1girl`. Aliases support regex patterns.

### Remove Underscores
Converts underscored tags to spaces (`long_hair` → `long hair`) while preserving:
- **Embedding names** — detected automatically from your embeddings folder
- **Custom exclusions** — e.g. `score_9, score_8_up` (configurable in settings)

### Paste Formatting
Optionally formats text as you paste it into prompt fields, including support for **Booru-style** tag structures (strips category labels, vote counts, and auto-escapes franchise names).

### LoRA Awareness
Temporarily substitutes `<lora:...>` tags and LoRA Block Weight values before formatting, so they don't get mangled by comma/space normalization.

### Wide Compatibility
Works with all prompt fields: **txt2img**, **img2img**, **hires fix**, and **ADetailer** prompts.

---

## Installation

### From the Extensions tab
Use **Install from URL** and paste this repository's URL.

### Manual install
```bash
cd /path/to/stable-diffusion-webui/extensions
git clone https://github.com/kaosnews/sd-webui-prompt-format.git
```

No additional dependencies required.

---

## Usage

After installation, a toolbar appears below the quicksettings bar with these controls:

| Control | Description |
|---------|-------------|
| **Auto Format** | Toggle automatic formatting on Generate |
| **Format** | Manual format button (visible when Auto Format is off) |
| **Remove Duplicates** | Toggle duplicate tag removal |
| **Remove Underscores** | Toggle underscore-to-space conversion |
| **Reload** | Reload exclusion list and aliases (visible when Remove Underscores is on) |

### Keyboard shortcut

Press `Alt + Shift + F` to format all prompt fields at any time.

---

## Settings

Find additional options under **Settings → Prompt Format**:

| Setting | Default | Description |
|---------|---------|-------------|
| Disable automatic updates | Off | Enable if extensions like [TagComplete](https://github.com/DominikDoom/a1111-sd-webui-tagcomplete) conflict with text editing events |
| Launch with Auto Format | On | Start the WebUI with auto formatting enabled |
| Launch with Remove Duplicates | On | Start with duplicate removal enabled |
| Launch with Remove Underscores | On | Start with underscore removal enabled |
| Append comma at end of line | On | Add trailing commas to multi-line prompts |
| Format pasted text | Off | Clean text as you paste from clipboard |
| Process Booru Structure | Off | Strip Booru metadata when pasting (requires paste formatting) |
| Exclusion tags | — | Comma-separated tags to exclude from underscore removal (e.g. `score_9, score_8_up`) |
| Tag Alias | — | Define aliases for deduplication using `main_tag: alias1, alias2, regex_pattern` syntax |

### Tag Alias examples

```
1girl: girl, woman, lady
adult: \d+\s*(y\.?o\.?|[Yy]ear[s]? [Oo]ld)
```

The first line treats `girl`, `woman`, and `lady` as duplicates of `1girl`. The second uses a regex to match age descriptions like `25 years old` or `30y.o.` and replaces them with `adult`.

---

## License

[MIT](LICENSE)
