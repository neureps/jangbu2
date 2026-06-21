---
name: jangbu-design-system
description: Design system, constraints, and tech approach for the jangbu.html Korean corporate double-entry bookkeeping web app
metadata:
  type: project
---

`jangbu.html` is a single-file Korean corporate double-entry bookkeeping (복식부기) web app at `/Users/cypark/jangbu/jangbu.html`.

**Hard constraints (do not violate):**
- Must remain a SINGLE HTML file. No external CSS/JS files, no CDNs/webfonts/image URLs. Must work offline by double-clicking.
- System font stack only (Pretendard/Apple SD Gothic Neo/Malgun Gothic for Korean).
- Never change JS logic. JS depends on these ids: `date type subWrap subLabel sub payWrap pay amount memo vat preview addBtn formHint view exportBtn clearBtn`. And these classes (some injected via innerHTML into #view/#preview): `tab(.active,data-view) del(data-id) muted ln deb cre pill num empty cal-list cal-item(.soon,.upcoming) cal-dday cal-body cal-date cal-note acct-head summary box k v balance-ok balance-bad`. JS also injects inline styles referencing CSS vars `--bad --ok --ink` and hex `#b45309`.
- CSS-only improvements; minimal HTML wrapper additions allowed but keep all ids/classes/data-attrs.

**Design system (light theme, Korean fintech/accounting SaaS feel — Toss/Douzone/BankSalad):**
- Tokens in `:root`: bg `#f4f6f9` w/ radial gradient, card `#fff`, line `#e6e9ef`. Ink `#1a2233`, sub `#6b7480`.
- Accounting state colors: 차변(debit) blue `--debit:#1f6fdb`, 대변(credit) red `--credit:#d6442a`, accent `#2563eb`, ok `#15a34a`, warn `#b45309`, bad `#dc2626`.
- Radius scale 8/12/16px; layered soft shadows (--sh-sm/--sh/--sh-lg).
- Numbers use tabular-nums + font-feature "tnum" everywhere (.num, amounts, D-day, summary .v).
- Tabs are a segmented control inside a tinted track. Buttons have gradient + shadow. Calendar items have a colored left accent bar via ::before (soon=red, upcoming=amber).

**Why:** User wants trustworthy, professional, modern look with strong accounting-data readability.
**How to apply:** Reuse these tokens and the debit-blue/credit-red convention for any future edits. Verify ids/classes above are untouched after any change.
