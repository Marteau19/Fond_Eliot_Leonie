# Investment Tracking Dashboard for Léonie & Éliot

A simple, beautiful web page to track and share investment information with your kids.

## Features

- Clean, responsive design that works on all devices
- **Pulls data directly from Google Sheets** - update your sheet and the page updates automatically!
- Fallback to local JSON data file
- Automatic calculations and formatting
- Beautiful gradient design with card-based layout
- Color-coded returns (green for positive, red for negative)
- Auto-refreshes every 5 minutes

## Setup: Connect Your Google Sheet

### Step 1: Prepare Your Google Sheet

Your Google Sheet should match this structure (same as the screenshot you provided):

**Tip:** You can import the `google-sheet-template.csv` file to get started quickly!

| Row | Column A               | Column B | Column C | Column D | Column E (Investissement) | Column F (Nbs Actions) | Column G (Valeurs) | Column H (Rendement) |
|-----|------------------------|----------|----------|----------|---------------------------|------------------------|--------------------|--------------------|
| 1   | (headers)              |          |          |          | Investissement            | Nbs Actions            | Valeurs            | Rendement          |
| 2   | (blank)                |          |          |          |                           |                        |                    |                    |
| 3   | Valeur du fond         | $500.00  |          | Léonie   | $180.00                   | 18                     | $225.00            | 45.00%             |
| 4   | Nombres d'actions      | 40       |          | Éliot    | $220.00                   | 22                     | $275.00            | 55.00%             |
| 5   | Valeurs de l'action    | $13      |          |          |                           |                        |                    |                    |
| 6   | (blank)                |          |          |          |                           |                        |                    |                    |
| 7   | (blank)                |          |          |          |                           |                        |                    |                    |
| 8   | Rendement du fond      |          |          |          |                           |                        |                    |                    |
| 9   | Année à date           | 0%       |          |          |                           |                        |                    |                    |
| 10  | 1 an                   | 0%       |          |          |                           |                        |                    |                    |
| 11  | 2 ans                  | 0%       |          |          |                           |                        |                    |                    |

### Step 2: Publish Your Google Sheet

1. Open your Google Sheet
2. Click **File > Share > Publish to web**
3. In the dialog:
   - Under "Link", select the specific **sheet tab** you want to publish
   - Change the dropdown from "Web page" to **"Comma-separated values (.csv)"**
   - Click **"Publish"**
   - Click **"OK"** to confirm
4. **Copy the published URL** (it will look like: `https://docs.google.com/spreadsheets/d/e/...`)

### Step 3: Add the URL to Your Web Page

1. Open `index.html` in a text editor
2. Find this line near the top of the `<script>` section (around line 249):
   ```javascript
   const GOOGLE_SHEET_CSV_URL = '';
   ```
3. Paste your Google Sheets URL between the quotes:
   ```javascript
   const GOOGLE_SHEET_CSV_URL = 'https://docs.google.com/spreadsheets/d/e/2PACX-...';
   ```
4. Save the file
5. Commit and push to GitHub

**That's it!** Now whenever you update your Google Sheet, the webpage will automatically fetch the latest data (refreshes every 5 minutes, or when you reload the page).

## Deploying to GitHub Pages

1. Push this repository to GitHub
2. Go to your repository settings
3. Navigate to "Pages" in the left sidebar
4. Under "Source", select the branch (usually `main` or `master`)
5. Click "Save"
6. Your site will be available at: `https://[your-username].github.io/Fond_Eliot_Leonie/`

## How to Update Your Data

Once connected to Google Sheets:

1. Open your Google Sheet
2. Update any values (fund value, share counts, returns, etc.)
3. Save the sheet (it auto-saves)
4. **Done!** The webpage will automatically pull the new data within 5 minutes, or immediately when you refresh the page

### Important: Keep the Sheet Structure

Make sure to keep the same structure as shown above. The parser expects:
- Row 1: Headers (Investissement, Nbs Actions, Valeurs, Rendement in columns E-H)
- Row 2: Blank row
- Row 3: Valeur du fond, value (B), (blank), Léonie (D), investment (E), shares (F), value (G), return% (H)
- Row 4: Nombres d'actions, value (B), (blank), Éliot (D), investment (E), shares (F), value (G), return% (H)
- Row 5: Valeurs de l'action, value (B)
- Row 9: Année à date, value (B)
- Row 10: 1 an, value (B)
- Row 11: 2 ans, value (B)

### Formulas for Calculations

You can use Google Sheets formulas to auto-calculate:

- **Current Value** (Column G) = shares (Column F) × sharePrice (Cell B5)
  - For Léonie (Row 3): `=F3*$B$5` → `=18*$B$5` → $225.00 (if share price is $12.50)
  - For Éliot (Row 4): `=F4*$B$5` → `=22*$B$5` → $275.00
- **Return %** (Column H) = ((currentValue - investment) / investment) × 100
  - For Léonie (Row 3): `=(G3-E3)/E3*100` → `=($225-$180)/$180*100` → 25%
  - For Éliot (Row 4): `=(G4-E4)/E4*100` → `=($275-$220)/$220*100` → 25%

**Note:** Use absolute reference `$B$5` for share price so it doesn't change when copying formulas.

## Alternative: Manual JSON Updates

If you prefer not to use Google Sheets, you can still manually update `data.json`:

1. Leave `GOOGLE_SHEET_CSV_URL` empty in `index.html`
2. Edit `data.json` directly on GitHub or locally
3. The page will load from the JSON file instead

## Customization

You can easily customize the appearance by editing `index.html`:
- Colors: Search for `#667eea` and `#764ba2` to change the gradient
- Font: Change the `font-family` in the CSS section
- Add more investors: Just add more objects to the `investors` array in `data.json`

## Files

- `index.html` - The main web page (includes HTML, CSS, and JavaScript)
- `google-sheet-template.csv` - Template for your Google Sheet structure
- `data.json` - Fallback data file (optional if using Google Sheets)
- `README.md` - This file

## Support

If you need help, feel free to reach out or consult the GitHub Pages documentation.

---

Made with ❤️ for Léonie & Éliot
