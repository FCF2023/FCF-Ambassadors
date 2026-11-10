# Ambassador space and page cleanup: proposal

Prepared 10 November 2026 from a review of the live site (all 27 published pages), its plugins, and the tools Falls Church Forward already uses.

## Summary

1. **Private ambassador space:** don't build a community inside WordPress. Run the conversation as a private **groups.io** email group (free), keep the **roster and files in a restricted Google Drive folder**, and give ambassadors one password-protected **Ambassador Hub page on the FCF site** that links to both. Cost: $0. Nothing new to patch or update.
2. **Page cleanup:** the welcome and ambassador material is spread over 7 pages. It fits on **3 evergreen pages plus the seasonal Good Neighbor Day page**. Three pages retire with redirects.
3. **Fix first:** `/ambassador-finder/` is live and in the sitemap with placeholder contact details (`naudy@example.com`, `(703) 555-0187`). Set it to Draft until the map has real data.
4. Draft versions of all four pages are in [`drafts/`](drafts/), written as paste-in Custom HTML blocks like the existing pages.

---

## Part 1: A private home for ambassadors

### Recommendation

Three small pieces, each doing the one thing it is good at:

| Piece | Tool | What lives there | Who can get in | Your upkeep |
|---|---|---|---|---|
| Front door | Password-protected page on fallschurchforward.org (`/ambassador-hub/`) | Links to everything, a short how-to, good-to-know notes | Anyone with the shared password | Edit a page now and then; change the password yearly |
| Conversation | Private groups.io group (Free plan) | Ideas, questions, announcements, searchable archive | Members you approve | Invite and remove members |
| Roster and files | Google Drive folder owned by the FCF Gmail account | Roster spreadsheet with contact details, flyers, welcome-kit materials, notes | Only the people you share it with | Share and unshare the folder |

Why this shape:

- **Email reaches people.** Volunteers answer email. They rarely remember to log in to a forum. With groups.io an ambassador replies from their inbox and everything is still archived and searchable on the web.
- **The site gives it a home.** The hub page is the one bookmark a new ambassador needs, on your own domain, in your own design.
- **Contact details sit behind per-person access.** The hub page has one shared password, which is fine for a signpost. The roster is the sensitive part, so it lives in Drive where each person is invited individually and can be removed individually. If the page password leaks, nobody's phone number does.
- **You maintain almost nothing.** No member accounts, no password resets, no extra plugins.

### Why not build it inside WordPress

A real members area means user accounts plus a forum or community plugin. That brings account creation and password resets (with Wordfence login checks in the way), spam sign-ups, more plugins to update on the site that hosts everything else, notification emails that need mail-delivery setup, and cache exceptions for WP Super Cache. Personal contact details would also sit in the website database. For a group this size it is the most work for the least use.

If the shared hub password ever feels too loose, the next step up is giving ambassadors individual logins and restricting the hub page to them (the free Members plugin does this). I would wait until there is a reason.

### Options compared

| Option | Cost | Where people talk | What you maintain | Verdict |
|---|---|---|---|---|
| **groups.io Free + hub page + Drive folder** | $0 | Email, with a private web archive | Group membership, Drive sharing, one page | **Recommended** |
| Google Group + hub page + Drive folder | $0 | Email, with a plainer web archive | One list: share the Drive folder with the group address and membership covers both | Good alternative if you want a single access list from day one |
| groups.io Premium | $220/year | Email and web | One list: roster (database), files, wiki and calendar all live inside the group | Upgrade path if two lists become a chore |
| Members area inside WordPress | Free and paid plugins | A forum people must remember to visit | Accounts, resets, spam, plugin updates, mail delivery | Not recommended |
| Private channel in the existing Discord | $0 | Chat | Assign a role | Fine as an extra for quick chatter, not as the home base |

groups.io Free covers up to 100 members and includes the email group and its archive, but not files, wiki, calendar or database. That is why the roster and files go in Drive. (Plan details checked on groups.io on 10 November 2026.)

### Setup

1. **Create the group** at groups.io, for example `fcf-ambassadors`. Create it from the FCF Gmail account rather than a personal one. Settings: not listed in the public directory, archive visible to members only, new members need approval, replies go to the group. Put the hub link in the welcome message new members receive.
2. **Create the Drive folder** in FCF's Google Drive, for example "FCF Ambassadors (private)". Add a Roster spreadsheet and move in any flyers or welcome-kit files. Keep general access set to Restricted and share with each ambassador by email. Give them edit rights on the roster so each person keeps their own row current.
3. **Create the hub page** from [`drafts/ambassador-hub.html`](drafts/ambassador-hub.html). Replace the three placeholder links, set Visibility to Password protected, set the page to noindex in Yoast, and leave it out of the menus.
4. **Check it** in a private browser window: the page should ask for the password. WordPress remembers the password on a device for about ten days.
5. **Invite the current ambassadors** to the group and the folder. First message: say hello and ask everyone to add their roster row.
6. **Add a second owner** to both the group and the folder so the setup does not depend on one person.

Suggested roster columns: name, neighborhood or building, zone (matching the map), email, phone, best way to reach, languages, on the public page (yes/no), joined.

### Upkeep

- **New ambassador:** invite to the group, share the folder, they add their roster row, you add their card to the Community Ambassadors page (now the only place it appears).
- **Someone steps back:** remove from the group, unshare the folder, remove their roster row and card. Change the hub password if you have any doubt.
- **Once a year:** change the hub password and skim the roster for stale rows.

### Decisions for you

1. **groups.io or Google Groups?** I recommend groups.io: it is built for exactly this and is nicer to use. Google Groups wins on one point only, a single access list. Both are free.
2. **Should ambassadors' personal contact details ever be public?** The map is built to show each ambassador's email and phone to anyone. I recommend the public pages show first name, neighborhood and bio, with contact going through the existing form, and that direct contact details stay in the private roster.

---

## Part 2: Fewer pages

### Today: 7 pages for one topic

| Page | What it is | Problem |
|---|---|---|
| `/welcome/` | Three tiles, then a full copy of the ambassador cards and form | Duplicates the ambassadors page |
| `/tips/` | Seven tips for new residents | Reached only from a Welcome tile |
| `/community-directory/` | One Airtable embed | Thin |
| `/welcome-newsletters-blogs-forums/` | One Airtable embed | Thin, awkward address |
| `/community-ambassadors/` | Intro, nine cards, form | The real home, but duplicated |
| `/ambassador-finder/` | Intro and the map | Placeholder data, linked from nowhere, in the sitemap |
| `/good-neighbor-day/` | September campaign page | Fine; seasonal |

The duplication has already caused drift: Belén is listed under **Park Towers** on Welcome and **Virginia Village** on Community Ambassadors.

### Proposed: 3 evergreen pages, 1 seasonal, 1 private

| Page | Absorbs | Contents |
|---|---|---|
| `/welcome/` | `/tips/` | Lead, three tiles, a short "Meet your ambassador" strip, then the tips under "Start here" |
| `/community-ambassadors/` | `/ambassador-finder/` | Intro, the only copy of the cards, a slot for the map once it is real, the only copy of the form, a link to the hub |
| `/community-directory/` | `/welcome-newsletters-blogs-forums/` | Both Airtable lists under two tabs |
| `/good-neighbor-day/` | | Unchanged. Show its homepage card in late summer only |
| `/ambassador-hub/` (new, private) | | See Part 1 |

Existing addresses of the surviving pages do not change, so printed links and QR codes keep working.

### Redirects

The Redirection plugin is already installed (Tools → Redirection).

| Old address | Send to |
|---|---|
| `/tips/` | `/welcome/#start-here` |
| `/welcome-newsletters-blogs-forums/` | `/community-directory/#word-on-the-street` |
| `/ambassador-finder/` | `/community-ambassadors/#find` |

`/ambassador-map/` stays as it is. It is the map itself, which gets embedded, not a page people browse to.

### Homepage and menu

- **Homepage "Neighbors, in action":** keep the Welcome and Community Ambassadors cards. Treat Good Neighbor Day and Candidate Forum as seasonal slots rather than permanent ones.
- **Menu (optional):** none of the welcome pages are in the top menu today. A "New here?" dropdown with Welcome, Community Ambassadors and Community Directory would fix that. "Mission" could make room, since About → Vision covers the same ground.

### Fix along the way

- Confirm Belén's neighborhood (the draft uses Virginia Village, from the more recently edited page).
- "Fall Church resident" in Robin's bio (fixed in the draft).
- "Ways to be a good neigbor" heading on Good Neighbor Day.
- Two Welcome tile images are 700–830 KB PNG files. Re-saving them smaller will speed the page up.

### Also noticed elsewhere (optional, lower priority)

- `/farmers-market/` and `/farmers-market-expansion/` are two versions of the same petition. Keep one, redirect the other.
- `/fundraiser-2026/` still shows registration for an event held 27 September 2026. Turn it into a short recap or unpublish it.
- The homepage "Candidate Forum" card describes the October 2025 forum in the present tense.
- `/our-vision/` and `/who-we-are/` could be one About page. The Vision page's title is currently "Falls Church Forward".
- `/meeting-search/` and `/meeting-finder/` are two search boxes over the same meeting records. They could be one page with two modes. This needs template work, so it can wait.
- `/subscribe/` lists RSS feeds only, while "Get updates" is the email sign-up. Renaming the page "RSS feeds" avoids the mix-up.

Doing only the welcome and ambassador consolidation takes the site from 27 public pages to 24. The optional items would bring it to about 20.

---

## Draft pages

| File | Becomes |
|---|---|
| [`drafts/welcome.html`](drafts/welcome.html) | `/welcome/` |
| [`drafts/community-ambassadors.html`](drafts/community-ambassadors.html) | `/community-ambassadors/` |
| [`drafts/community-directory.html`](drafts/community-directory.html) | `/community-directory/` |
| [`drafts/ambassador-hub.html`](drafts/ambassador-hub.html) | `/ambassador-hub/` (new, password protected) |

Each file starts with a comment explaining what it replaces and how to install it. They reuse the existing copy, images, Airtable views and Tally form. They were rendered against the live theme stylesheet at desktop and phone widths, but not on the live site, so preview each one in WordPress before publishing. The hub page text is starter copy to edit.

## Suggested order

1. **Now:** set `/ambassador-finder/` to Draft. Confirm Belén's neighborhood.
2. **Pages:** paste in the three public drafts, add the three redirects, retire the old pages, check the homepage cards.
3. **Ambassador space:** create the group, the folder and roster, and the hub page, then invite people.
4. **Later:** put real data in the map and switch it on within the Community Ambassadors page. Pick off the optional items.

## Note on this repository

`index.html` here is an older version of the map than the one live at `/ambassador-map/` (the live one has the current site fonts and colors). Copy the live version back before making map changes from this repository.
