# Egyptian Pharmacies Directory (دليل صيدليات مصر)

Comprehensive, structured open dataset containing **45,910 registered and licensed community pharmacies** across all 27 governorates in Egypt, sourced and aggregated from the official Egyptian Drug Authority (EDA) e-Services directory.

---

## 📦 Dataset Files

| File | Size | Records | Description |
|---|---|---|---|
| [`pharmacies.json`](./pharmacies.json) | ~34 MB | 45,910 | Formatted UTF-8 JSON dataset with coordinates & Google Maps URLs |
| [`pharmacies.csv`](./pharmacies.csv) | ~26 MB | 45,910 | UTF-8 with BOM (`utf-8-sig`) CSV for full compatibility with Excel and data tools |

---

## 📋 Schema & Fields

Each record contains:

```json
{
  "id": 1,
  "pharmacy_name": "( ام القري) صالح عبد الستار",
  "pharmacy_type": "community pharmcay",
  "governorate": "المنيا",
  "address": "منشأه المغالقه",
  "license_number": "611",
  "location_query": "( ام القري) صالح عبد الستار, منشأه المغالقه, المنيا, Egypt",
  "google_maps_url": "https://www.google.com/maps/search/?api=1&query=%28+%D8%A7%D9%85+%D8%A7%D9%84%D9%82%D8%B1%D9%8A%29+%D8%B5%D8%A7%D9%84%D8%AD+%D8%B9%D8%A8%D8%AF+%D8%A7%D9%84%D8%B3%D8%AA%D8%A7%D8%B1%2C+%D9%85%D9%86%D8%B4%D8%A3%D9%87+%D8%A7%D9%84%D9%85%D8%BA%D8%A7%D9%84%D9%82%D9%87%2C+%D8%A7%D9%84%D9%85%D9%86%D9%8A%D8%A7%2C+Egypt"
}
```

| Field | Type | Description |
|---|---|---|
| `id` | `integer` | Unique sequential record ID (`1` to `45910`) |
| `pharmacy_name` | `string` | Official registered pharmacy name in Arabic |
| `pharmacy_type` | `string` | Licensing classification (e.g. `community pharmcay`) |
| `governorate` | `string` | Egyptian governorate (e.g. `القاهرة`, `المنيا`, `الإسكندرية`) |
| `address` | `string` | Detailed physical street address |
| `license_number` | `string` | Official license registration number (رقم الترخيص) |
| `location_query` | `string` | Combination: `<Pharmacy Name>, <Address>, <Governorate>, Egypt` |
| `google_maps_url` | `string` | Direct link to view and navigate to the pharmacy on Google Maps |

---

## ⚡ Direct CDN Access

Access the full dataset directly via jsDelivr CDN:

```
https://cdn.jsdelivr.net/gh/mahmoudfalous/eg-pharmacies@main/pharmacies.json
```

### Quick Usage Examples

#### JavaScript / Node.js
```javascript
const res = await fetch("https://cdn.jsdelivr.net/gh/mahmoudfalous/eg-pharmacies@main/pharmacies.json");
const pharmacies = await res.json();
console.log(`Loaded ${pharmacies.length} pharmacies.`);
```

#### Python
```python
import pandas as pd

url = "https://cdn.jsdelivr.net/gh/mahmoudfalous/eg-pharmacies@main/pharmacies.json"
df = pd.read_json(url)
print(df.head())
```

---

## 🏛️ Data Source
- **Source**: [Egyptian Drug Authority (EDA) e-Services](https://eservicesdata.edaegypt.gov.eg/EDAPharmacy)
- **Scope**: Egypt National Directory
- **Total Records**: 45,910
