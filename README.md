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


---

## 💡 Parameter Explanation

| Key           | Description |
|---------------|-------------|
| appid         | Steam app ID (730 = CS:GO, 570 = Dota 2, 440 = TF2) |
| currency      | Steam currency ID (6 = PLN, see full list in Steam API docs) |
| output_file   | Path to Excel file (must be inside an existing folder) |
| sleep_seconds | Delay between requests (to avoid blocking) |
| items         | Dictionary of items: "Item Name or URL": Buy Price |

---

## 🧩 Installation & Setup

### 🐧 Linux (Python 3.13)

Install Python 3.13:
```bash
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update
sudo apt install python3.13 python3.13-venv python3.13-dev
```

Create a virtual environment:
```bash
python3.13 -m venv venv
source venv/bin/activate
```

Install dependencies:
```bash
pip install --upgrade pip
pip install requests pandas openpyxl
```

Run the script:
```bash
python main.py
```

> ⚠️ Make sure the folder for the Excel file (e.g., data/) exists before running the script.

### 🪟 Windows (Python 3.13)

Install Python 3.13:
Download from: https://www.python.org/downloads/release/python-3130/

Create a virtual environment (optional):
```powershell
python -m venv venv
.
env\Scripts\Activate.ps1
```

Install dependencies:
```powershell
pip install --upgrade pip
pip install requests pandas openpyxl
```

Run the script:
```powershell
python main.py
```

> ⚠️ Ensure that the output directory for the Excel file already exists.

---

## 📘 License

This project is released under the MIT License.
Feel free to fork, modify, and improve it!
