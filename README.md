# Invoice Desk

A complete browser-based GST service-invoicing app. There is one final app, in `index.html`. No installation, build, API keys, subscription or database setup is required.

## Publish on GitHub Pages

1. Create a **new public repository for this client** in GitHub, for example `school-invoice-desk`. This supports GitHub Pages on a free GitHub account. Only application code goes in the repository.
2. Upload `index.html` to the repository root. Keep the filename exactly `index.html`, in lowercase. You can alternatively use **Add file → Create new file**, name it `index.html`, paste the entire supplied file and commit.
3. Upload `.nojekyll` from this package too if using Upload files. The HTML app itself is self-contained.
4. Open the repository's **Settings → Pages**.
5. Under **Build and deployment**, choose **Deploy from a branch**. Choose your default branch (usually `main`) and **/(root)**, then Save.
6. Wait for GitHub to complete deployment. Use the published website URL shown on the Pages screen. Share that URL with your client. Opening the code repository itself will not open the app.
7. Your client fills **Business settings**, adds a **Customer**, and clicks **New invoice**.

Do not upload invoice backups, real customer records, bank statements or any private client data to the repository. The app starts with an empty workspace. Enter real details in the running app after deployment.

You can copy and paste the complete HTML into GitHub. The other supplied files are instructions and tests; they are not needed to run the app. Do not upload the internal preview configuration or `dist` directory; neither is included in the ZIP.

## Included

- Dashboard: taxable sales, cash received, TDS, outstanding, overdue balances, six-month billing chart and invoice status counts.
- Customer directory: add, edit, search, delete unused contacts and start invoices for customers.
- Vendor directory: add, edit, search and delete vendor contacts, including bank details and notes.
- Sales invoices: add, edit, duplicate, search and filter.
- Invoice numbering: configurable prefix and Indian financial-year series. Duplicate numbers within the same financial year are rejected.
- Multiple service lines (up to 50): descriptions, SAC/HSN, quantity, unit, rate, discount and GST rate per line.
- CGST + SGST or IGST, line-level paise rounding and optional final rounding adjustment.
- Place of supply, school/customer GSTIN or URP, contract/PO reference and service period.
- Automatic amount in words, bank details, payment terms and signature area.
- Draft, issued and cancelled stages. Unpaid, part-paid, overdue and paid statuses are calculated from receipts, TDS and due dates.
- Multiple cash/bank receipts and verified TDS credits per invoice.
- Direct multi-page PDF download and browser Print / Save PDF.
- CSV sales-register export.
- Full JSON backup and restore.
- Mobile-responsive layout. No external fonts, libraries, analytics or CDN requests.

Vendor management is a contact directory. Purchase invoices, vendor payments, stock and complete double-entry accounting are not part of this app.

## First invoice

1. **Business settings:** enter legal name, address, GSTIN, state name/code, contact and bank details. Confirm default GST rate and payment terms.
2. **Customers:** add the school with its legal name, billing address, state and code. Leave GSTIN blank if unregistered.
3. **Sales invoices → New invoice:** select the customer, dates, place of supply, contract and service period.
4. Add actual service descriptions and SAC codes. Rates are exclusive of GST. Discount is an amount in rupees per line, not a percentage.
5. Save as a draft or mark Issued. Issuing requires complete supplier GST details.
6. Open the invoice and click **Download PDF**. If the browser blocks automatic downloads, click the visible **Save [filename].pdf** link. The link remains available for five minutes; regenerate after that if necessary.
7. Alternatively select **Print / Save PDF**, choose A4, disable browser headers and footers, and save.
8. Record cash/bank receipts and actual verified TDS credits separately. The invoice total and GST do not change when payments are entered.

PDF downloads are rendered to page images inside a genuine PDF. This supports Unicode text without external fonts, but the downloaded PDF's text is not selectable. Browser Print / Save PDF is available when selectable text is needed. Print output depends on the device's fonts and print settings.

## Storage, privacy and devices — read before client use

**Records are stored only in localStorage in the client's browser, on that device. This is not a cloud-synced system.**

- The public link distributes the application code. Other visitors do not see records stored in your client's browser.
- There is no login or server-side account. Anyone with access to that browser profile can access its records. Local records and JSON backups are not encrypted by the app.
- Data does not automatically appear on another mobile, computer or browser profile. Use **Download full backup** and **Restore JSON backup** to transfer it.
- Download a backup after important changes and before moving devices, clearing browser storage, changing the URL/domain or reinstalling a browser. Keep more than one dated backup in a private folder or your own cloud drive.
- Restore replaces the current browser's records. Back up the current workspace first. A backup download by itself is not automatic cloud storage.
- Private/incognito browsing may discard records when closed. Use a normal browser profile.
- Browser storage capacity is limited and varies by device. The app reports save failures instead of silently losing edits. If storage is full, export a backup and address browser storage before continuing.
- Avoid editing the same workspace in multiple tabs simultaneously. Stale-tab writes are rejected when detected; this is not multi-user collaboration or a database transaction system.
- A new client on the same browser and website address would share that local workspace. Use a separate website/repository address per client or a separate browser profile.
- Default origin-based browser storage also means repositories under the same `username.github.io` origin share the origin. This app scopes its data key to the page path, so separate repository paths use separate workspaces. Changing the path requires backup/restore.
- Path-based keys avoid accidental record mixing; they do not provide security isolation from other JavaScript hosted under the same origin. Host untrusted apps on a different origin.

For shared team access, logins or automatic phone/computer sync, add a separate authenticated backend and database. GitHub Pages alone cannot supply those services.

## GST scope

This app is designed for INR domestic forward-charge service invoices using CGST + SGST or IGST. Confirm the actual GST registration, SAC/HSN, tax rate and place-of-supply treatment. A school customer does not automatically make the marketing supplier's services exempt.

UTGST, GST cess, reverse charge, export/SEZ invoices, credit/debit notes, e-invoice IRNs, signed QR codes and GST return filing are not automated. An ordinary generated PDF does not replace e-invoicing where applicable. Invoice numbers must be consecutive, unique within a financial year and at most 16 characters. The client must review the actual contract and legal treatment before issue.

Existing invoices save their own business/customer snapshots, so changing a contact or business profile does not rewrite previously saved invoices. Use the supplied PDF copies as issued records. Edits to legally issued invoices may require an appropriate credit/debit note outside this app.

## Demo

Open **Help & backups → Load fictional demo** in an empty workspace to explore. All demo names and identifiers are fictional. Never issue them as real invoices. Clear the demo only after confirming no real records are present.

## Troubleshooting

- **I see GitHub code instead of the app:** open the GitHub Pages deployment URL shown in Settings → Pages.
- **404 after deployment:** ensure `index.html` is in the selected root directory and Pages deployment succeeded.
- **The app looks unchanged after a code update:** reload the page. Back up your records before clearing any site data.
- **I cannot issue a draft:** complete business settings, then open the draft and use **Refresh business details** to copy the current profile into that draft. Confirm customer, SAC, dates and tax type too.
- **Download blocked:** use the visible Save-file link, or Print / Save PDF. Allow downloads for your own site if your browser prompts.
- **Records missing on mobile:** restore the desktop JSON backup on mobile. There is no automatic sync.
- **Different business name on an older invoice:** its supplier snapshot is intentionally preserved. Refresh the draft's business details if appropriate before issue.

## Developer checks

The package includes dependency-free Node tests:

```sh
node tests.mjs
```

The test suite checks tax arithmetic, discounts, payment status, duplicate invoice numbers, validation, HTML escaping, backup validation, storage failure handling and workspace separation. Browser checks cover invoice editing, receipts/TDS, PDF and backup export and customer/vendor forms. No test data is embedded into the initial workspace.

GST invoice field reference: https://taxinformation.cbic.gov.in/content-page/explore-rules/1000136/1000001

GitHub Pages setup reference: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
