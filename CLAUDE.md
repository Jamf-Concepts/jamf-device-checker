# App Store Stub — Agent Setup Guide

This repository is a documentation and issue-tracking hub for a Jamf Concepts app distributed via the Apple App Store. There is no source code here.

## Your Job

Populate this stub so it is ready for public use. That means filling every `[PLACEHOLDER]` token across the README, wiki pages, and issue templates using content sourced from the App Store listing and the developer-provided inputs below.

## What to Ask the Developer

Before starting, confirm you have these five values:

| Field | Example |
|---|---|
| App Store URL | `https://apps.apple.com/app/jamf-passport/id1234567890` |
| Jamf Pro required? | `yes` / `no` / `optional` |
| Jamf Pro minimum version | `11.0` (only if required) |
| Managed config keys? | `yes` / `no` |
| Managed config key details | key name, type, description, default (only if yes) |

Everything else — app name, description, platform support, OS requirements, screenshots context, version — comes from the App Store listing.

## Step-by-Step

### 1. Fetch the App Store listing
Fetch the App Store URL provided by the developer. Extract:
- App name
- Short description (for the README one-liner)
- Full description (for the problem/solution narrative)
- Platform support (iOS, iPadOS, macOS, visionOS)
- Minimum OS versions
- Current version number
- Developer name (should be Jamf)

### 2. Populate the README
Fill in `README.md`:
- `[APP NAME]` → app name from App Store
- `[APP_STORE_ID]` → the `id` portion of the App Store URL (e.g. `id1234567890`)
- One-liner under the title → short description from App Store
- **The Problem** → derive from the App Store description: what pain point does this app address?
- **How [APP NAME] Solves It** → derive from the App Store description: what does the app do and why does it matter?

### 3. Populate the wiki seed pages
The `wiki/` folder contains seed pages that must be pushed to the repo's wiki (`.wiki.git`), not served from the repo itself. Populate each file first, then push.

**wiki/Home.md**
- App name, one-liner, App Store badge link

**wiki/Overview.md**
- Key features (from App Store description)
- Use cases (infer from App Store description and target audience)
- Requirements table (platforms and OS versions from App Store listing, Jamf Pro from developer input)
- App Store link

**wiki/Getting-Started.md**
- Prerequisites based on requirements
- Installation steps: ABM/ASM volume purchase path + direct App Store path
- First-run setup (infer from App Store description; note if unclear)
- Managed configuration table (from developer input — omit section if no managed config)

**wiki/FAQ.md**
- Fill in platform compatibility and Jamf Pro answers from confirmed inputs
- Leave troubleshooting items as placeholders if specific issues aren't known

**wiki/Changelog.md**
- Seed with current App Store version and today's date
- Use "Initial release" if no prior history is available

**wiki/_Sidebar.md**
- Replace `[APP NAME]` and `[APP_STORE_ID]`

### 4. Push wiki pages
Clone the wiki repo and push the populated pages:

```bash
git clone https://github.com/Jamf-Concepts/[REPO-NAME].wiki.git
# copy populated wiki/ files in, commit, push
```

### 5. Update issue templates
Replace `[APP NAME]` and `[APP_STORE_ID]` in:
- `.github/ISSUE_TEMPLATE/config.yml`
- `.github/ISSUE_TEMPLATE/bug_report.yml`
- `.github/ISSUE_TEMPLATE/feature_request.yml`
- `.github/ISSUE_TEMPLATE/general_question.yml`

### 6. Commit and open a PR
- Commit all changes to a new branch off `develop`
- Do not push directly to `main` or `develop` — open a PR against `develop`
- PR title: `feat: initial stub population for [APP NAME]`

## Done When

- [ ] No `[PLACEHOLDER]` tokens remain in any file
- [ ] All wiki pages are pushed to `.wiki.git`
- [ ] PR is open against `develop`
