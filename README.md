# Facebook Groups Exporter (FBGroups2CSV)

A Chrome Manifest V3 extension that collects visible Facebook group details and exports CSV or JSON.

### Install in Chrome

1. Select **Code > Download ZIP** on GitHub and extract it to a permanent folder, or clone this repository.
2. Open `chrome://extensions` in Chrome and enable **Developer mode**.
3. Click **Load unpacked** and select the extracted or cloned repository folder containing `manifest.json` and `content.js`. Chrome loads the folder directly; it cannot install the ZIP.
4. Log in to Facebook in Chrome and open or refresh a Facebook Groups page. The **Groups Exporter** panel appears in the lower-right corner. You do not need to run PasteHappy to collect groups.

Keep the selected folder in place while the extension is installed. After replacing its files, click **Reload** on the extension card and refresh the Facebook tab.

### Collect groups and export CSV

1. Open a Facebook group listing or search Facebook for your topic and select the **Groups** results.
2. Click **Scan Visible** to collect group links currently loaded on the page. Scroll to load more results and scan again, or click **Auto-Scan (120s)** to scroll and scan automatically. **Auto duration** and **Scroll interval** adjust that run; click **Stop Auto-Scan** to stop early.
3. Optionally set **Min members** or **Active within** before collecting. Leave these at `0` and blank to collect without those restrictions; groups with unknown activity are excluded when an activity threshold is set. These collection filters do not remove previously saved groups. Use **Clear** first when starting a fresh collection.
4. Enable **Show list** to review results. **Sort list** controls export order, and **List filter** also limits which collected rows are exported. Groups are deduplicated by their group URL identifier, with a default limit of 5,000 collected groups.
5. Set **Format** to **CSV** and click **Export**. Chrome downloads a file named `fb-groups-YYYY-MM-DD-HH-MM-SS.csv`. **Copy** copies the selected export format to the clipboard instead.

The CSV contains `Group Name`, `Members`, `Members Num`, `Last Active`, `Privacy`, `Join Status`, `URL`, `Source URL`, and `Scanned At`. It uses UTF-8 with a BOM and quoted values for spreadsheet compatibility.

### Use the CSV in [PasteHappy-Python](https://github.com/DevSkits916/PasteHappy-Python)

PasteHappy recognizes the extension's `Group Name` and `URL` headings and ignores the extra metadata columns. The extension collects group details only; it does not generate post text.

Open the exported CSV in a spreadsheet editor, add a column named `Post`, and enter the message for each group. Save as CSV, then select **Import CSV** in PasteHappy. Alternatively, import into the manual workspace and edit each row's post text there before selecting **Queue Manual CSV**. Review names, URLs, and messages before posting.

With **Persist results** enabled, collected groups are saved in Facebook's site storage in that Chrome profile and can carry across pages and reloads. **Clear** removes the collected list. Closing the panel hides it until the page is refreshed. The extension runs on `www.facebook.com` and `m.facebook.com` URLs containing `groups`; if the panel is missing, refresh a matching page and check that the extension is enabled. Collection depends on the group links Facebook has loaded and its current page structure, so it is not guaranteed to find every group or every metadata field.
