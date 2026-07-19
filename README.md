# R2R Renewal Desk

Annual renewal ledger and invoice generator for R2R Tutorials. Runs entirely in the
browser — no server, no database, no accounts. Installs to a phone home screen and
works without a signal.

## Files

| File | Purpose |
|---|---|
| `index.html` | The whole app — UI, logic, invoice template |
| `manifest.webmanifest` | Name, icons, colours for the installed app |
| `sw.js` | Service worker; makes it work offline |
| `icon-192.png`, `icon-512.png`, `icon-maskable-512.png`, `apple-touch-icon.png` | Icons |

## Putting it on GitHub Pages

1. Create a repository, e.g. `r2r-renewal-desk`.
2. Upload all the files above to the repository root (not inside a folder).
3. **Settings → Pages → Build and deployment → Source: Deploy from a branch**,
   branch `main`, folder `/ (root)`. Save.
4. Wait a minute or two, then open
   `https://learn2earninvesting-maker.github.io/r2r-renewal-desk/`.

GitHub Pages serves over HTTPS, which is what the service worker, install prompt and
contacts picker all require. It will not install from a `file://` path.

## Installing on your phone

- **Android / Chrome** — open the URL, then **Setup → Add to home screen**, or use the
  browser's Install app menu item.
- **iPhone** — open the URL **in Safari** (Chrome on iOS cannot install web apps),
  tap Share, then Add to Home Screen.

## First run

Open **Setup** and fill in your UPI and bank details, phone and address. Everything on
the invoice comes from there.

## Where the data lives

In the browser's local storage on that one device. Nothing is uploaded anywhere.

That means: clearing site data wipes it, and a second device starts empty. Use
**Setup → Export backup** after each round of collections, and **Import backup** to move
to a new phone.

## Publishing changes

Browsers cache the app aggressively once the service worker is installed. After editing
`index.html`, bump the version in `sw.js`:

```js
const CACHE = 'r2r-desk-v2';   // was v1
```

Without that, phones keep serving the old copy.

## Calendar

The app does not sync with your calendar. **Setup → Export all renewals** produces a
`.ics` file; opening it adds a yearly repeating reminder per client, alerting 7 days
ahead and again on the day. Re-export after changing fees or dates — entries carry a
stable ID per client, so they update rather than duplicate. Deleting a client here does
not remove their calendar entry; do that in the calendar app.

## Keeping the calendar in sync (subscribed feed)

`renewals.ics` in this repo is a live calendar feed. Subscribe once per device and it
re-reads the file on its own — adding, editing or removing a client eventually reaches
every calendar without touching them individually.

Feed URL:

```
https://learn2earninvesting-maker.github.io/r2r-renewal-desk/renewals.ics
```

**Subscribe (once per device)**

- iPhone: Settings → Apps → Calendar → Accounts → Add Account → Other →
  Add Subscribed Calendar → paste the URL.
- Google Calendar: on desktop, Other calendars → **+** → From URL → paste.
  It will not accept a URL added from the mobile app.

**Update it (whenever clients change)**

1. In the app: Setup → **Download renewals.ics**.
2. Upload that file to the repo root, replacing the existing one.
3. Done. Subscribers refresh on their own.

Notes:

- Yearly repetition is built into each entry, so nothing needs doing at year end.
- Google refreshes subscribed URLs on its own schedule, often 12–24 hours, and cannot be
  forced. Irrelevant for annual renewals with a 7-day advance alert.
- Subscribed calendars are read-only on the device. Record payments in the app, not the
  calendar.
- Do not also import the one-off export onto a device that subscribes to the feed, or
  every renewal shows twice.
