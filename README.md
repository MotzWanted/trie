# trie

Trie is a Python 3.12 library for building searchable ICD-10-CM/PCS tries
directly from the official CMS releases. It downloads the yearly XML/PDF
packages, normalizes the tabular structure, alphabetic indexes, and coding
guidelines, and exposes a `Trie` API for lookups, fuzzy term search, and
navigating instructional notes.

## Highlights
- `ICD10Trie` automatically fetches CMS ICD-10 files (or uses a local folder)
  and caches them under `~/.cache/trie/icd`.
- The parser ingests CM chapters, PCS tables, all alphabetic indexes, and both
  CM/PCS coding guidelines.
- The base `Trie` class provides helpers to traverse chapters/categories,
  retrieve instructional notes and guidelines, group codes, and run fuzzy term
  searches (via RapidFuzz).

## Usage
```python
from src.icd import ICD10Trie

trie = ICD10Trie.from_cms(year=2024, use_update=False)
trie.parse()
result = trie["Z66"].description
print(result)
```

If you already have the CMS XML/PDF bundle locally, replace
`ICD10Trie.from_cms(...)` with `ICD10Trie.from_dir(Path("/path/to/files"))`.
