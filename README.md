# Azure DevOps Test Case Creator

A Windows desktop app for **bulk‑creating, editing, and managing Test Cases in Azure DevOps** (dev.azure.com), linked to a Product Backlog Item (PBI). It fills a gap in Azure DevOps: there's no built‑in way to add many Test Cases at once — each one normally has to be added by hand from a PBI's *Add Test* button.

> This repository hosts the **installer and automatic updates only**. The application source code lives in a separate private repository.

## Download & install

1. Open the [**latest release**](../../releases/latest) and download `AzureDevOpsTestCaseCreator-win-Setup.exe`.
2. Run it. It installs per‑user (no administrator rights needed) and adds a Start‑menu shortcut.
3. The installer isn't code‑signed yet, so Windows SmartScreen may warn you — choose **More info → Run anyway**.

After the first install the app **updates itself**: on launch it checks here for a newer version and, if one exists, downloads a small delta and restarts into it.

## What it does

- **Sign in with Microsoft** — uses your existing Microsoft account via interactive sign‑in (MSAL). No Personal Access Token or app registration required, and your token is never written to disk. Your organisation and project are discovered automatically.
- **Pick a PBI** — a searchable picker with live work‑item search and your recent PBIs.
- **Manual Entry** — build a Test Case with a title, steps (action + expected result), tags, module, preconditions, and automation status. Save reusable form templates.
- **Import from Excel / CSV** — download a template, fill it in, and bulk‑import dozens of cases at once with a live preview.
- **Edit existing Test Cases** — load the cases already linked to a PBI; search, filter, edit individually or in bulk (tags, automation status, assignee), rename with regex/literal Power Rename, and export to Excel.
- **Bulk‑update round‑trip** — export existing cases to Excel (each row carries its work‑item ID), change them in the spreadsheet, and re‑import to update the originals — matched by ID, so no duplicates are created.
- **Test Plan integration** — automatically creates the requirement‑based Test Suite for the PBI, so your cases show up in the board's test count just like the manual *Add Test* flow does.
- **Review before anything is written** — a confirmation screen lists exactly what will be created or updated before any change reaches Azure DevOps.
- **Comfortable to use** — dark / light themes and crisp high‑DPI scaling across monitors.

## Safety by design

The app is deliberately conservative with your Azure DevOps data:

- It **never deletes** anything and never modifies the PBI itself — it only creates Test Cases and links them, or updates the specific fields you changed.
- Every batch is shown on a **Review & Confirm** screen before a single write call is made.
- Requests are **rate‑limited** to stay within Azure DevOps limits and honour throttling.
- Your sign‑in token is held **in memory only** — never saved to disk and never logged.

## Requirements

- Windows 10 or 11.
- An Azure DevOps (dev.azure.com) account with permission to create Test Cases in your project.

## Updates

Every release is published here and the installed app keeps itself up to date automatically using [Velopack](https://velopack.io). You can also re‑download the latest `Setup.exe` from the Releases page at any time.
