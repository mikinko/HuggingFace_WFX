# HugginFace VFS Plugin

Native Total Commander file system plugin for browsing Hugging Face models,
organizations, collections, and repository files as a virtual folder tree.

`hf_wfx` is a single `.wfx64` plugin for 64-bit Total Commander on Windows.
It does not require Python, Git LFS, or a separate runtime.

## What It Does

- Browse Hugging Face organizations as model folders.
- Browse organization collections and the models inside them.
- Pin a single model repository as a top-level folder.
- View small files directly with Total Commander's viewer.
- Copy model files to local storage with Total Commander's normal copy flow.
- Use an optional Hugging Face API token for private or gated repositories.
- Cache listings locally for faster repeated browsing.

## Video
Intro.mp4
https://github.com/mikinko/HuggingFace_WFX/blob/main/Intro.mp4

## Browsing Modes

| Mode | Example | Result |
|---|---|---|
| Organization models | `https://huggingface.co/google` | Adds `google - models` |
| Organization collections | `https://huggingface.co/google` | Adds `google - collections` when collections exist |
| Single model | `https://huggingface.co/meta-llama/Llama-3.1-8B-Instruct` | Adds one model folder |

## Main Options

| Option | Purpose |
|---|---|
| API key | Enables private/gated access and improves rate limits |
| Cache folder | Stores local JSON listings under `%APPDATA%\hf_wfx\cache` by default |
| Cache TTL | Controls how long cached listings are considered fresh |
| Enable offline cache | Preloads listings for faster later browsing |
| Batch size | Loads large organizations incrementally, default `300` models |
| Refresh cache now | Clears and refetches listing data on next browse |
| Remove entry | Removes the virtual root entry only; remote Hugging Face data is not touched |

## Large Organizations

Large organizations are loaded in batches. The first listing loads 300 models by
default. If more models are available, the folder shows:

```text
[Load next 300 models]
```

Open that row to fetch the next page and append it to the cached listing.

## Total Commander Actions

| Action | Behavior |
|---|---|
| F7 at root | Add a new entry |
| F5 | Copy files locally |
| Delete on a root entry | Remove the virtual entry only |
| Properties at plugin root | Show plugin name, version, author, repo count, and config folder |

## Data Locations

| Path | Contents |
|---|---|
| `%APPDATA%\hf_wfx\favorites.json` | API key, options, saved entries |
| `%APPDATA%\hf_wfx\cache\` | Cached organization, collection, and model-tree listings |

## Build Output

The release artifact is:

```text
hf_wfx.wfx64
```

Install it through Total Commander:

```text
Configuration -> Options -> Plugins -> FS-Plugins -> Configure -> Add
```

## Current Version

Version `1.2` by `MiKi`.
