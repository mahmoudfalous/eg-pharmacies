<div align="center">

# Egyptian Pharmacies Directory
### دليل صيدليات مصر

**An open, structured directory of community pharmacies across Egypt.**

[![Dataset](https://img.shields.io/badge/records-45%2C910-2ea44f)](#dataset-overview)
[![Coverage](https://img.shields.io/badge/coverage-27%20governorates-blue)](#geographic-coverage)
[![Format](https://img.shields.io/badge/formats-JSON%20%7C%20CSV-orange)](#download-the-dataset)
[![Data License](https://img.shields.io/badge/data-CC%20BY%204.0-lightgrey)](LICENSE-DATA)
[![Code License](https://img.shields.io/badge/code-MIT-green)](LICENSE-MIT)

</div>

A structured dataset of **45,910 pharmacy directory records** covering Egypt's 27 governorates. The records were collected and organized from the [Egyptian Drug Authority (EDA) e-Services pharmacy directory](https://eservicesdata.edaegypt.gov.eg/EDAPharmacy).

The dataset is intended for data analysis, geographic discovery, mapping, research, directory applications, and other software projects.

> **Important:** This is an independently maintained data project, not an official EDA publication or service. A record in this dataset should not be treated as confirmation that a pharmacy is currently operating or that its license is currently valid. Verify important information with the relevant authority before relying on it.

---

## Dataset Overview

| Metric | Value |
|---|---:|
| Records | **45,910** |
| Geographic coverage | **27 Egyptian governorates** |
| Languages | Arabic (primarily) |
| Formats | JSON, CSV |
| Source | EDA e-Services pharmacy directory |
| Last verified | See the repository's latest dataset update / commit |

## Download the Dataset

The files are available directly from this repository:

| File | Format | Approx. size | Description |
|---|---|---:|---|
| [`pharmacies.json`](./pharmacies.json) | JSON | ~34 MB | UTF-8 JSON array |
| [`pharmacies.csv`](./pharmacies.csv) | CSV | ~26 MB | UTF-8 CSV with BOM (`utf-8-sig`) for spreadsheet compatibility |

### Direct CDN access

You can load the JSON file from jsDelivr:

```text
https://cdn.jsdelivr.net/gh/mahmoudfalous/eg-pharmacies@main/pharmacies.json
```

For production applications, consider downloading and caching the file rather than fetching the full dataset on every request.

## Data Schema

Each record contains the following fields:

| Field | Type | Description |
|---|---|---|
| `id` | Integer | Sequential record identifier |
| `pharmacy_name` | String | Pharmacy name as listed in the source directory |
| `pharmacy_type` | String | Pharmacy classification as provided by the source |
| `governorate` | String | Egyptian governorate |
| `address` | String | Address text as listed in the source |
| `license_number` | String | License number shown in the source directory |
| `location_query` | String | Search-friendly combination of pharmacy name, address, governorate, and country |
| `google_maps_url` | String | Google Maps search URL generated from the location query |

### Example record

```json
{
  "id": 1,
  "pharmacy_name": "( ام القري) صالح عبد الستار",
  "pharmacy_type": "community pharmcay",
  "governorate": "المنيا",
  "address": "منشأه المغالقه",
  "license_number": "611",
  "location_query": "( ام القري) صالح عبد الستار, منشأه المغالقه, المنيا, Egypt",
  "google_maps_url": "https://www.google.com/maps/search/?api=1&query=..."
}
```

**Location note:** `google_maps_url` is a search link, not a verified latitude/longitude coordinate. Google Maps may return approximate or ambiguous results, especially when addresses are incomplete or duplicated.

**Source values:** Names, classifications, addresses, and license numbers are preserved from the collected directory data. Spelling inconsistencies or missing values may exist.

## Usage

### JavaScript / Node.js

```javascript
const response = await fetch(
  "https://cdn.jsdelivr.net/gh/mahmoudfalous/eg-pharmacies@main/pharmacies.json"
);

if (!response.ok) {
  throw new Error(`Dataset request failed: ${response.status}`);
}

const pharmacies = await response.json();

console.log(`Loaded ${pharmacies.length} pharmacy records.`);

// Find pharmacies in a governorate
const inMinya = pharmacies.filter(
  (pharmacy) => pharmacy.governorate === "المنيا"
);

console.log(inMinya.slice(0, 5));
```

### Python

```python
import pandas as pd

url = (
    "https://cdn.jsdelivr.net/gh/"
    "mahmoudfalous/eg-pharmacies@main/pharmacies.csv"
)

df = pd.read_csv(url, encoding="utf-8-sig")

print(f"Loaded {len(df):,} pharmacy records")

# Filter by governorate
minya_pharmacies = df[df["governorate"] == "المنيا"]

print(minya_pharmacies.head())
```

### CSV with Python's standard library

```python
import csv

with open("pharmacies.csv", encoding="utf-8-sig", newline="") as file:
    reader = csv.DictReader(file)

    for pharmacy in reader:
        print(
            pharmacy["pharmacy_name"],
            pharmacy["governorate"],
            pharmacy["address"],
        )
        break
```

## Geographic Coverage

The dataset is intended to cover all **27 governorates of Egypt**. Governorate names are represented in Arabic as provided by the source.

## Data Source & Methodology

- **Source:** [Egyptian Drug Authority (EDA) — Pharmacy Directory](https://eservicesdata.edaegypt.gov.eg/EDAPharmacy)
- **Collection:** Records were collected from the publicly accessible EDA e-Services directory.
- **Organization:** Records were structured into JSON and CSV formats.
- **Location links:** Google Maps search URLs were generated using the pharmacy name and address fields.

This repository is an independent compilation. It is not affiliated with, endorsed by, or officially maintained by the Egyptian Drug Authority.

### Data quality considerations

- The source directory may change over time; this repository may not reflect every change immediately.
- Addresses and names may contain spelling variations, incomplete details, or duplicate-looking entries.
- A Google Maps search URL does not guarantee an exact location.
- A listed license number is reproduced from the source and is not a live license-status check.
- Always verify critical or time-sensitive information against the original source.

## License & Attribution

This repository separates the licensing of its original code from the licensing of its original dataset compilation:

- **Original code and scripts:** MIT License — see [`LICENSE-MIT`](./LICENSE-MIT).
- **Original dataset compilation and arrangement:** CC BY 4.0 — see [`LICENSE-DATA`](./LICENSE-DATA).

The licenses above apply only to material the repository author has the rights to license. They do **not** relicense third-party source material, government records, trademarks, or other rights held by the EDA or other parties. Users are responsible for checking and complying with the source website's terms and any applicable laws before reusing source records.

If you use or redistribute this compilation, provide attribution:

> Egyptian Pharmacies Directory (`eg-pharmacies`) by Mahmoud Mohamed. Source: Egyptian Drug Authority (EDA) e-Services pharmacy directory. https://github.com/mahmoudfalous/eg-pharmacies

If you modify the dataset, indicate that changes were made and do not imply that your version is official or endorsed by the EDA.

## Citation

For academic work, research, or applications, cite this repository:

```text
Mahmoud Mohamed. Egyptian Pharmacies Directory (eg-pharmacies).
45,910 pharmacy directory records from Egypt.
Source: Egyptian Drug Authority (EDA) e-Services pharmacy directory.
https://github.com/mahmoudfalous/eg-pharmacies
```

A machine-readable citation is available in [`CITATION.cff`](./CITATION.cff).

## Contributing

Corrections, reproducible data-quality reports, and improvements to the documentation are welcome.

1. Open an issue describing the problem or proposed improvement.
2. Include examples and the source reference when reporting a data issue.
3. For code or documentation changes, open a pull request with a clear description.

Please do not submit private personal information or claim that an unverified record is current.

## Contact

- **GitHub Issues:** [Report a problem or request an improvement](https://github.com/mahmoudfalous/eg-pharmacies/issues)
- **GitHub:** [@mahmoudfalous](https://github.com/mahmoudfalous)

---

<div align="center">

**Built to make Egyptian public directory data easier to explore and use.**

  </div>