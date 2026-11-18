# R2R Renewal Desk

Annual renewals for R2R Tutorials, on autopilot.

- **The app** (`index.html`) runs on your phone from GitHub Pages and works without a signal.
- **The autopilot** (`Code.gs`) is a free Google Apps Script in your own Google account. Every morning at 07:00 it:
  - emails each client a heads-up **14 days before** their renewal
  - emails the **invoice PDF on the renewal date**
  - keeps a **"R2R Renewals" Google Calendar** up to date
  - emails you a digest only when something needs you
- **WhatsApp reminders** are written by the app. A week after an unpaid due date, then weekly up to 3, a reminder appears on the Today screen. You tap **WhatsApp**, check the message and press Send. After reminder 3 the app tells you to call.

Your clients and receipts are kept in a Google Sheet, so every device shows the same list.

## Files

| File | Where it goes |
|---|---|
| `index.html`, `sw.js`, `manifest.webmanifest`, icons | This GitHub repository (root) |
| `Code.gs` | **Not GitHub.** Paste it into the Apps Script editor of your Google Sheet (step 1) |
| `renewals.ics` | No longer needed. Leave it or delete it |

---

## Setting it up (once, about 20 minutes)

### On your laptop: the autopilot

1. Go to **sheets.google.com** signed in as learn2earninvesting@gmail.com and create a blank sheet. Name it **R2R Renewal Desk**.
2. In the sheet, open **Extensions → Apps Script**. Delete the few lines already in the editor, paste in the whole of `Code.gs`, and press **Save** (the disk icon).
3. In the dropdown next to **Run**, choose **setup**, then press **Run**.
   Google asks for permission: **Review permissions → your account → Advanced → Go to project (unsafe) → Allow**.
   It says "unsafe" only because you wrote the script yourself and Google hasn't reviewed it. It runs only in your account.
4. Press **Deploy → New deployment**. Click the gear icon, choose **Web app**, and set:
   - Execute as: **Me**
   - Who has access: **Anyone**

   Then press **Deploy**.
5. Go back to the sheet tab and reload it. A new **R2R** menu appears. Open **R2R → Show connection link** and copy the link. Email it to yourself so you can open it on your phone.

### On your laptop: the app

6. Open **github.com/learn2earninvesting-maker/r2r-renewal-desk**.
7. Click **Add file → Upload files**. Drag in `index.html`, `sw.js`, `manifest.webmanifest` and `README.md`, then press **Commit changes**. GitHub replaces the old copies.
8. Wait about two minutes for GitHub Pages to update.

### On your phone

9. Open the Renewal Desk as you normally do. If it still looks like the old dark app, close it fully and open it again.
10. Your clients carry over from the old version on their own. Open the **☰ menu → Setup**, paste the connection link under **Connect autopilot** and tap **Connect**. Your clients copy into the Sheet.
11. Still in Setup, fill in **Invoice and payment details**, especially your **UPI ID**, and tap **Save details**.
12. Go to **Clients**. For each client, tap **Edit** and add their **email** and **WhatsApp number**. Without an email, the autopilot can't send their heads-up and invoice.
13. Tap **Send me test emails**. Four samples arrive in your inbox, marked [TEST]: heads-up, invoice, receipt and your digest. Check the wording and your payment details.
14. When you're happy, tap **Go live**. From the next morning at 07:00, emails go to clients.

Until you press Go live, the autopilot is in **test mode**. Each morning it emails *you* a list of what it would have sent, and clients get nothing.

**Google Calendar:** the renewals appear on a new calendar called **R2R Renewals**. On iPhone, add your Google account under Settings → Calendar → Accounts if it isn't already there. If you subscribed to the old `renewals.ics` feed, you can remove that subscription now.

---

## What you do from then on

| When | What |
|---|---|
| Money arrives | Open the client → **Record payment**. They get a receipt email, and their renewal moves on a year. |
| A WhatsApp reminder is due | It shows in red on **Today**. Tap **WhatsApp**, then press Send in WhatsApp. |
| After 3 reminders, still unpaid | Today shows **Call these**. Call them, then **Record payment** or **Mark lapsed**. |
| New client | **☰ → Add client**. Nothing else to do. |
| Fee changes or client leaves | **Edit** the fee, or **Mark lapsed** |
| Once a year, if you like | **Money → Export** gives you the year's receipts as a spreadsheet |

Invoice numbers run `R2R/26-27/001`, `002`… and restart each 1 April.

Clients who were **more than 14 days overdue** when the autopilot started don't get an automatic invoice. Use the WhatsApp reminders for them. The **Invoice** button on any client opens a printable copy you can share yourself.

## If something seems off

- **Setup** shows the last morning run and whether it worked. If a run fails, Google emails you.
- **R2R → Run autopilot now** in the Sheet runs the morning check straight away.
- **Wrong key / can't connect:** copy the link again from **R2R → Show connection link**. If you changed `Code.gs`, deploy again with **Deploy → Manage deployments → Edit → Version: New version**.
- **Keep the connection link private.** Anyone with it can see your client list.

## Publishing changes to the app

After editing `index.html`, bump the version at the top of `sw.js` (`r2r-desk-v2` → `r2r-desk-v3`). Otherwise phones keep showing the old copy.
