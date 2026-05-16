# Stumptown Merch Page — Deploy Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Deploy the Stumptown Disc Golf merch page to Vercel with updated branding and a live QR code.

**Architecture:** Single static `index.html` at repo root — no framework, no build step. Vercel detects and serves it automatically. Logo is a sibling `logo.png` file referenced by `<img>` tag.

**Tech Stack:** HTML/CSS, Git, GitHub CLI (`gh`), Vercel dashboard

---

## File Map

| File | Action | Purpose |
|---|---|---|
| `index.html` | Rename + modify | Main merch page (renamed from `stumptown-merch.html`) |
| `logo.png` | Add later | Real club logo (placeholder `<img>` tag added now) |

---

### Task 1: Rename file and initialize Git

**Files:**
- Rename: `stumptown-merch.html` → `index.html`

- [ ] **Step 1: Rename the file**

```powershell
Rename-Item "stumptown-merch.html" "index.html"
```

- [ ] **Step 2: Initialize git repo**

```powershell
git init
git add index.html
git commit -m "init: add merch page"
```

Expected output: `1 file changed` commit confirmation.

---

### Task 2: Update color scheme to match stumptowndiscgolf.org

**Files:**
- Modify: `index.html` (CSS variables block, lines 12–21)

- [ ] **Step 1: Replace the `:root` CSS variables block**

Find this block in `index.html`:
```css
:root {
  --navy: #1a2744;
  --navy-light: #243259;
  --teal: #2eaad1;
  --teal-light: #4bc4e8;
  --cream: #f7f4ee;
  --warm-white: #fdfcfa;
  --gold: #d4a43a;
  --text-main: #1a2744;
  --text-muted: #5a6a8a;
}
```

Replace with:
```css
:root {
  --navy: #111111;
  --navy-light: #222222;
  --teal: #01add3;
  --teal-light: #33c4e0;
  --cream: #ffffff;
  --warm-white: #f4f4f4;
  --gold: #d4a43a;
  --text-main: #111111;
  --text-muted: #555555;
}
```

- [ ] **Step 2: Open `index.html` in a browser and verify visually**

- Background should be white (not cream)
- Section label bars should be near-black (not navy)
- Accent color on prices and icons should be the brighter site teal `#01add3`
- Payment card (dark section) should read as black, not navy
- Gold deal prices should be unchanged

- [ ] **Step 3: Commit**

```powershell
git add index.html
git commit -m "style: update colors to match main site branding"
```

---

### Task 3: Replace placeholder SVG logo with real logo img tag

**Files:**
- Modify: `index.html` (header section, lines 335–346)

- [ ] **Step 1: Replace the logo-mark div**

Find this block:
```html
<div class="header">
  <div class="logo-mark">
    <svg viewBox="0 0 44 44" fill="none" xmlns="http://www.w3.org/2000/svg">
      <circle cx="22" cy="22" r="18" stroke="#2eaad1" stroke-width="2"/>
      <ellipse cx="22" cy="22" rx="10" ry="3.5" fill="#2eaad1" opacity="0.7"/>
      <circle cx="22" cy="22" r="3" fill="#2eaad1"/>
      <line x1="4" y1="22" x2="40" y2="22" stroke="#2eaad1" stroke-width="1.5" opacity="0.4"/>
    </svg>
  </div>
  <h1>Stumptown<br><span>Disc Golf</span></h1>
  <p>Club Merch &amp; Swag</p>
</div>
```

Replace with:
```html
<div class="header">
  <img src="logo.png" alt="Stumptown Disc Golf" class="logo-img">
  <p>Club Merch &amp; Swag</p>
</div>
```

- [ ] **Step 2: Replace the `.logo-mark` CSS rule with `.logo-img`**

Find and remove:
```css
.logo-mark {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 72px;
  height: 72px;
  background: var(--navy);
  border-radius: 50%;
  margin-bottom: 1rem;
}

.logo-mark svg {
  width: 44px;
  height: 44px;
}
```

Replace with:
```css
.logo-img {
  height: 100px;
  width: auto;
  margin-bottom: 1rem;
}
```

- [ ] **Step 3: Open in browser — confirm header shows broken image placeholder (expected until logo.png is added), and subtitle "Club Merch & Swag" still renders**

- [ ] **Step 4: Commit**

```powershell
git add index.html
git commit -m "feat: swap placeholder SVG for real logo img tag"
```

---

### Task 4: Push to new GitHub repo

- [ ] **Step 1: Create the GitHub repo**

```powershell
gh repo create stumptown-merch --public --source=. --remote=origin --push
```

Expected output: repo URL printed, e.g. `https://github.com/YOUR_USERNAME/stumptown-merch`

If `gh` is not authenticated, run `gh auth login` first and follow the prompts.

- [ ] **Step 2: Verify on GitHub**

Open the repo URL in your browser. Confirm `index.html` is visible in the file list.

---

### Task 5: Deploy to Vercel

- [ ] **Step 1: Go to vercel.com → Add New Project**

- Click **"Add New Project"**
- Click **"Import Git Repository"**
- Select the `stumptown-merch` repo

- [ ] **Step 2: Configure project settings**

- Framework Preset: **Other** (not Next.js)
- Root Directory: `/` (leave as default)
- Build Command: leave blank
- Output Directory: leave blank (or set to `.`)
- Click **Deploy**

- [ ] **Step 3: Note the live URL**

After deploy completes (~30 seconds), Vercel shows the URL. It will be something like:
`https://stumptown-merch.vercel.app`

Copy this URL — you'll need it for Task 6.

- [ ] **Step 4: Open the URL on your phone and verify the page loads correctly**

---

### Task 6: Generate and add the site QR code

- [ ] **Step 1: Generate the QR code**

Go to [https://www.qr-code-generator.com](https://www.qr-code-generator.com) and:
- Paste the live Vercel URL
- Select PNG format, size 500×500px minimum
- Download as `menu-qr.png`
- Drop `menu-qr.png` into the project folder alongside `index.html`

- [ ] **Step 2: Locate the existing QR section in `index.html`**

Find the block starting with:
```html
<!-- QR CODE -->
<div style="width:100%;max-width:640px;display:flex;justify-content:center;margin-bottom:1.5rem;">
  <div class="qr-card" style="max-width:260px;width:100%;">
    <div class="qr-label">PayPal</div>
```

- [ ] **Step 3: Add the Merch Menu QR card before the existing PayPal QR card**

Find the opening line of the existing QR section:
```html
<div style="width:100%;max-width:640px;display:flex;justify-content:center;margin-bottom:1.5rem;">
```

Replace that opening div and everything up to (but not including) the first `<div class="qr-card"` with:
```html
<div class="qr-section">
  <div class="qr-card">
    <div class="qr-label">Merch Menu</div>
    <div class="qr-img-wrap">
      <img src="menu-qr.png" alt="Merch Menu QR Code">
    </div>
    <div class="qr-sublabel">Scan to view this menu</div>
  </div>
```

Then at the end of the section, replace the closing `</div>` of the outer wrapper with just `</div>` closing the `.qr-section` div (the existing PayPal `.qr-card` div stays intact between them).

The existing PayPal `<img src="data:image/png;base64,...">` tag must not be touched — only the outer wrapper div is changed.

- [ ] **Step 4: Commit and push**

```powershell
git add index.html menu-qr.png
git commit -m "feat: add live menu QR code alongside PayPal QR"
git push
```

Vercel auto-deploys on push. Wait ~30 seconds then verify both QR codes display on the live URL.

---

### Task 7: Add real logo (when file is ready)

- [ ] **Step 1: Drop `logo.png` into the project folder**

File must be named `logo.png` and placed at the root (same level as `index.html`).

- [ ] **Step 2: Open in browser — logo should display in header**

- [ ] **Step 3: Adjust size if needed**

If the logo looks too large or small, update this CSS rule in `index.html`:
```css
.logo-img {
  height: 100px; /* adjust this value */
  width: auto;
  margin-bottom: 1rem;
}
```

- [ ] **Step 4: Commit and push**

```powershell
git add index.html logo.png
git commit -m "feat: add real Stumptown logo"
git push
```
