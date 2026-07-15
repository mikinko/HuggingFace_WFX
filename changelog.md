## 1.4.0 — 2026-06-30

### Added
- **Dataset support.** Browse and download HuggingFace datasets, mirroring how
  models already work:
  - An **"Add datasets"** checkbox in Add Entry creates an `org - datasets`
    listing (with the usual `[Load next N]` paging).
  - A direct `huggingface.co/datasets/org/name` URL adds a single dataset
    folder (auto-detected; previously this mis-parsed `datasets` as the org).
  - The `***_TEMPORARY_***` slot accepts dataset URLs too.

  Datasets resolve under HF's `/api/datasets` + `datasets/…/resolve` namespace,
  cached separately (`org_datasets_*`, `tree_ds_*`) so a model and dataset of
  the same `org/name` never collide. Existing `favorites.json` entries load
  unchanged (default kind = model). Datasets *inside Collections* are still
  filtered out — collections show models only for now.

## 1.3.0 — 2026-06-30

### Added
- **`***_TEMPORARY_***` browse slot.** A virtual folder pinned at the top of the
  root. Entering it prompts for a HuggingFace org or model URL, then lets you
  browse and download that repo exactly like a saved entry — but it is never
  written to `favorites.json`. Returning to the root folder clears it, so the
  next visit prompts again. Org URLs list models (with the usual
  `[Load next N models]` paging); `org/model` URLs open the model tree directly.
  Caching behaves normally (keyed by repo id), so re-downloads stay fast.

## 1.2.1 — 2026-06-30

### Fixed
- **WinHTTP timeouts.** Every request now sets `WinHttpSetTimeouts`, so a
  stalled or half-open connection can no longer freeze Total Commander's UI
  thread indefinitely.
  - Metadata calls (org models / tree / collections): 15s resolve, 15s connect,
    30s send, 30s receive.
  - File downloads: same setup bounds with a 120s receive timeout (the
    inter-chunk gap), so large weights on a slow link aren't aborted prematurely.
- **Cache folder setting was ignored.** The cache path chosen in Global Settings
  is now persisted to `favorites.json` (`cache_path`) and honored on load, and
  the folder is created immediately on save. Previously it was discarded and
  reset to `%APPDATA%\hf_wfx\cache` on every startup. Configs without the key
