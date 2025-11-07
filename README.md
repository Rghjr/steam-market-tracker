# Steam Market Tracker – CS:GO / Dota / TF2

This Python script tracks the Steam Market prices of specific items (currently CS:GO, Dota 2, TF2). It fetches the lowest available market price for each item, calculates net return after Steam fees, and generates a nicely formatted Excel file with charts.

---

## How It Works

1. **Data Collection**
   - The script fetches the **lowest currently available price** for each item listed in the `config.json`.
   - Supports both regular item names and full Steam Market URLs.
   - Only works when the **Steam Market is online**. If the market is down or slow, no data will be fetched.
   - Sleep time between requests is configurable to prevent Steam from blocking requests.

2. **Excel File Generation**
   - Creates a new Excel sheet for each run with a timestamp.
   - If the Excel file does not exist, the script will create it (but the **folder must exist**).
   - Applies formatting:
     - Headers bold and centered
     - All cells centered
     - `% Return` column highlighted:
       - **Green** for positive return
       - **Red** for negative return
   - Auto-adjusts column widths.
   - Generates line charts showing net price trends per item over time.

3. **Excel Contents**
   - Columns:
     - `Item_Link` – link to the Steam Market listing
     - `Item_Name` – item name
     - `Buy_Price` – your purchase price
     - `Current_Sell_Price` – current market price
     - `Net_Sell_Price` – price after Steam fee
     - `% Return` – profit/loss percentage
   - Charts are in a separate sheet called `Charts`.

---

## Notes / Warnings

- **Excel folder must exist** before running the script.
- Sleep time between requests (`sleep_seconds` in `config.json`) should be long enough, otherwise Steam may block requests and you'll get **no price info**.
- Script works **only if the Steam Market is online**.
- Collects data for the **lowest price item currently available** (unless a URL is specified, then it fetches that exact listing).

---

## Setting Up `config.json`

Example:

```json
{
  "appid": 730,                  // Steam app ID: 730 = CS:GO, 570 = Dota 2, 440 = TF2
  "currency": 6,                 // Steam currency ID (6 = PLN)
  "output_file": "data/steam_data.xlsx", // Path to Excel output file
  "sleep_seconds": 3,            // Seconds to wait between requests
  "items": {
    "Fracture Case": 2.2,        // "Item Name": Your buy price
    "Recoil Case": 1.67,
    "Sticker | Flex": 2.9,
    "Sticker | Hypnoteyes (Holo)": 6.85,
    "https://steamcommunity.com/market/listings/730/Austin%202025%20Legends%20Sticker%20Capsule": 1.85
                                  // You can also provide full Steam Market URL instead of name
  }
}
