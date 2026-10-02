# HuggingFace VFS Plugin

Native Total Commander file system plugin for browsing Hugging Face models,
datasets, organizations, collections, and repository files as a virtual folder tree.
It has been built using claude/codex AI. Hope you find it useful.

`hf_wfx` is a single `.wfx64` plugin for 64-bit Total Commander on Windows.
It does not require Python, Git LFS, or a separate runtime.

## NEWS v1.6
- **Much faster downloads.** Large files are fetched over up to 8 parallel
  connections, with a separate disk-writer thread — no more slowdown on
  multi-GB files. Broken connections resume from where they stopped, and an
  expired download link is renewed automatically.
- **Resume.** An aborted or failed copy keeps what was downloaded; copy again
  and choose *Resume* in TC's overwrite dialog. Resumed files are verified
  against HuggingFace's sha256.
- **Fast folder opening.** Repos are listed one folder at a time (no more
  waiting for the whole tree of a huge dataset), and every folder you have
  seen is served from the cache.
- **Real dates everywhere.** Model folders in org listings and collections show
  the model's last change; inside a repo every file shows its own last commit
  and every folder the latest change within it — sort by date to see what was
  updated recently. (Folders with more than 500 items, e.g. dataset shards,
  show the repo's date instead to stay fast.)
... and more
  
## NEWS v1.4
- **`***_TEMPORARY_***` browse slot.** A virtual folder pinned at the top of the
  root. Entering it prompts for a HuggingFace org or model URL, then lets you
  browse and download that repo exactly like a saved entry — but it is never
  written to `favorites.json`
- **Dataset support.** Browse and download HuggingFace datasets

## What It Does

- Browse Hugging Face organizations as model / dataset folders.
- Browse organization collections and the models inside them.
- Pin a single model or dataset repository as a top-level folder.
- View small files directly with Total Commander's viewer.
- Copy files to local storage with Total Commander's normal copy flow.
- Use an optional Hugging Face API token for private or gated repositories.
- Cache listings locally for faster repeated browsing.

## Video
how it works, add repo, delete, rename ...  

https://github.com/user-attachments/assets/72104be6-0c45-4fe9-9f11-5cef0e6eda4b

## Browsing Modes

| Mode | Example | Result |
|---|---|---|
| Organization models | `https://huggingface.co/google` | Adds `google - models` |
| Organization datasets | `https://huggingface.co/google` | Adds `google - datasets` |
| Organization collections | `https://huggingface.co/google` | Adds `google - collections` when collections exist |
| Single model | `https://huggingface.co/meta-llama/Llama-3.1-8B-Instruct` | Adds one model folder |
| Single dataset | `https://huggingface.co/datasets/HuggingFaceFW/fineweb-edu` | Adds one dataset folder |

## Main Options

| Option | Purpose |
|---|---|
| API key | Enables private/gated access and improves rate limits |
| Config folder | Where `favorites.json` is kept, default `%APPDATA%\hf_wfx` |
| Cache folder | Stores local JSON listings, default `%APPDATA%\hf_wfx\cache` |
| Cache TTL | How long cached listings are considered fresh (Ctrl+R overrides) |
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
| F7 inside an entry | Entry settings |
| F5 | Copy files locally (resumable) |
| Ctrl+R | Refetch the current folder from HuggingFace |
| Delete on a root entry | Remove the virtual entry only |
| Properties at plugin root | Show plugin name, version, author, repo count, and config folder |

## Data Locations

| Path | Contents |
|---|---|
| `hf_wfx.ini` next to the plugin file | `ConfigPath=` — folder of `favorites.json` (env vars allowed, relative = plugin folder) |
| `<ConfigPath>\favorites.json` | API key (encrypted), options, saved entries |
| `<cache folder>\` | Cached organization, collection, and repo-folder listings |

Default `hf_wfx.ini`:

```ini
[hf_wfx]
ConfigPath=%APPDATA%\hf_wfx
```


