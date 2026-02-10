# Duplicate Payment Detection using n8n & Google Sheets

This project implements an automated workflow using **n8n** and **Google Sheets**
to detect **duplicate payments / invoices** in real time.

Whenever a new row is added to the Google Sheet, the workflow checks whether the
`invoice_no` already exists. If a duplicate is found, the payment status is
automatically marked as **DUPLICATE**.

---

## 🚀 Features

- 🔄 Triggered automatically when a new row is added to Google Sheets
- 🔍 Checks for duplicate `invoice_no`
- 🏷️ Updates payment status (`DUPLICATE` / `NEW`)
- ⚙️ Built using **n8n (no-code / low-code)**
- 📊 Uses Google Sheets as the data source

---

## 🛠️ Tech Stack

- **n8n** – Workflow Automation
- **Google Sheets** – Data storage
- **Google Sheets Trigger & Actions**
- **IF node** – Conditional logic
- **Edit Fields** – Data preparation

---

## 📂 Google Sheet Structure

| payment_id | vendor | invoice_no | amount | payment_date | status |
|------------|--------|------------|--------|---------------|--------|
| 100        | Amazon | 200        | 1000   | 10-02-2026    | DUPLICATE |
| 101        | Amazon | 200        | 1000   | 10-02-2026    | DUPLICATE |
| 102        | Jio    | 201        | 2000   | 11-02-2026    | NEW |

---

## 🔁 Workflow Steps

1. **Google Sheets Trigger**
   - Trigger: *On Row Added*
   - Monitors the `Payments_Data` spreadsheet

2. **Get Row(s)**
   - Fetches rows matching the same `invoice_no`

3. **IF Node**
   - Condition:
     ```text
     {{ $json.invoice_no }} 
     is equal to 
     {{ $('Google Sheets Trigger').item.json.invoice_no }}
     ```

4. **Edit Fields**
   - Sets:
     - `status = DUPLICATE` (if true)
     - `status = NEW` (if false)

5. **Update Row**
   - Updates the matching row in Google Sheets
   - Writes the `status` value

---

## ✅ Use Cases

- Payment reconciliation
- Invoice validation
- Finance automation
- Preventing double payments
- No-code automation demos

---

## 📌 How to Use

1. Import the workflow JSON into n8n
2. Connect your Google account credentials
3. Select your Google Sheet and worksheet
4. Add a new row to the sheet
5. Watch the `status` column update automatically 🎉

---
