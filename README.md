# web-data-store

Centralized data repository for static web projects. Stores JSON, CSV, and other data files served via GitHub Pages or jsDelivr CDN.

## Usage

### Via jsDelivr CDN (recommended)

```
https://cdn.jsdelivr.net/gh/USERNAME/web-data-store@main/{project}/{file}
```

### Via GitHub Raw

```
https://raw.githubusercontent.com/USERNAME/web-data-store/main/{project}/{file}
```

### Example

```js
// Fetch JSON
fetch(
  "https://cdn.jsdelivr.net/gh/USERNAME/web-data-store@main/padang-culinary/places.json",
)
  .then((res) => res.json())
  .then((data) => console.log(data));

// Fetch CSV (with Papa Parse)
Papa.parse(
  "https://cdn.jsdelivr.net/gh/USERNAME/web-data-store@main/padang-culinary/menus.csv",
  {
    download: true,
    header: true,
    complete: (results) => console.log(results.data),
  },
);
```

## Directory Structure

```
web-data-store/
├── padang-culinary/       # Peta Kuliner Padang project
│   ├── places.json
│   └── menus.csv
├── personal-site/         # Personal website data
│   └── blog-metadata.json
└── ...                    # Future project folders
```

## Data Guidelines

| Format  | When to Use                                             |
| ------- | ------------------------------------------------------- |
| `.json` | Structured data, nested objects, direct browser parsing |
| `.csv`  | Tabular/spreadsheet-origin data, large flat datasets    |
| `.js`   | Small datasets embedded as JS modules (no fetch needed) |

### File Size Recommendations

- **< 1 MB** — load directly, no special handling needed
- **1–5 MB** — add a loading indicator in the consuming app
- **5–10 MB** — consider splitting by category or region
- **10+ MB** — compress or paginate; avoid single-file loads

### Optimization Tips

- Use short key names in JSON (`lat` instead of `latitude`)
- Round coordinates to 4 decimal places (~11m accuracy)
- Remove unused fields before committing
- Minify JSON for production: `jq -c . data.json > data.min.json`

## Caching

- **jsDelivr**: Cached globally, purge via `https://purge.jsdelivr.net/gh/USERNAME/web-data-store@main/{path}`
- **GitHub Raw**: ~5 minute cache, not suitable for high-traffic production use

## Adding a New Project

1. Create a new folder: `mkdir project-name`
2. Add data files to the folder
3. Update this README's directory structure section
4. Commit and push — files are instantly available via CDN

## License

Data in this repository is for personal/project use unless otherwise stated per folder.
