

# VaultX — Client-Side Password Vault

## Overview
A fully browser-based password manager with AES-GCM encryption, PIN-based authentication, and all data stored in localStorage. Dark-mode-only security-focused design.

---

## Phase 1: Foundation & Security Layer

### Dark Theme & Design System
- Override CSS variables with the specified dark color palette (#0F1117 background, #6C63FF primary, etc.)
- Import Inter font from Google Fonts
- Set up custom card styles with subtle purple glow shadows
- Configure 12px/8px/50px border radius tokens

### Crypto Utilities
- SHA-256 PIN hashing via Web Crypto API
- PBKDF2 key derivation (100k iterations) from PIN + random salt
- AES-GCM encrypt/decrypt functions with unique IV per entry
- Secure password generator using `crypto.getRandomValues()`
- All keys held in memory only, cleared on lock

### Master PIN Lock Screen
- First-visit: "Set Your Master PIN" (4–6 digit numeric input)
- Return visits: PIN entry with 3-attempt lockout (30s countdown)
- "Forgot PIN?" option with confirmation dialog to wipe all data
- Smooth fade-in animation on successful unlock
- Auto-lock after configurable inactivity timeout (default 5 min)
- Manual lock button (top-right lock icon)

---

## Phase 2: Vault Dashboard

### Layout
- Two-column desktop layout: persistent sidebar + card grid
- Collapsible sidebar on tablet, hamburger menu on mobile
- Responsive grid: 3 cols desktop, 2 tablet, 1 mobile

### Left Sidebar
- "VaultX" logo/name at top
- Total entries count badge
- Category filters with emoji icons and count badges (All, ⭐ Favorites, 💬 Social, 💰 Finance, 💼 Work, 🛒 Shopping, 📧 Email, 🎮 Gaming, 📁 Other)

### Main Content
- Search bar (real-time filter across siteName, username, siteUrl)
- Sort options: Newest, Oldest, A–Z, Last Updated
- Entry cards with: favicon (or initial avatar), site name, username, masked password with show/hide toggle, category badge, favorite star toggle, copy/edit/delete actions, "last updated" footer
- Staggered fade-in animation on cards
- Empty states for no entries, no search results, and empty categories

### Copy Password Behavior
- Decrypt → copy to clipboard → "Copied!" tooltip
- Auto-clear clipboard after 30s with countdown toast
- Option to clear immediately

---

## Phase 3: CRUD Operations

### Add Entry (Floating "+" button → slide-up modal/drawer)
- Fields: Site Name*, Site URL, Username*, Password* (with show/hide), Notes (max 300 chars), Category dropdown with emojis, Favorite toggle
- Favicon auto-fetch via Google's favicon service
- Inline password generator panel (length slider 8–64, character type toggles, exclude ambiguous chars, live preview, regenerate, "Use This Password")
- Password strength meter (4-segment bar: Weak/Fair/Good/Strong with tips)
- Encrypt password + notes on save → toast "Entry saved 🔒"

### Edit Entry
- Same modal pre-filled with decrypted values
- Password history tracking (last 5) in collapsible section
- Old passwords masked by default, reveal on hover/click
- Toast "Entry updated ✅"

### Delete Entry
- Inline confirmation popover per card
- Card animate-out on delete → toast "Entry deleted 🗑️"
- Bulk delete mode: select toggle activates checkboxes, floating "Delete Selected (N)" bar

---

## Phase 4: Settings & Extras

### Settings Panel (gear icon, top-right)
- Change Master PIN (requires current PIN)
- Auto-lock timer selector (1 min / 5 min / 15 min / Never)
- Export vault as encrypted JSON file download
- Import vault from JSON file
- "Wipe All Data" (red, requires PIN confirmation)
- Storage stats: total entries + localStorage bytes used

### Seed Data
- After first PIN setup, offer "Load sample entries?" prompt
- 5 fake entries across different categories for immediate UI exploration

