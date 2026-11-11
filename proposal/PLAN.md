# FCF website: welcome and ambassador page consolidation

First prepared 10 November 2026. Updated 11 November 2026: decisions recorded and the page changes applied to the live site.

## Status

| Item | Decision | Status |
|---|---|---|
| Welcome, ambassadors and directory pages | Consolidate, with redirects. Belén is in Virginia Village. | **Live** 11 Nov. Checked at desktop and phone widths. |
| Ambassador space (hub page, groups.io) | On hold pending discussion | Nothing installed. Notes kept in section 7. |
| Ambassador map | Keep off the site until ready. Remove the GitHub copy. | Finder page in Draft. `index.html` deleted on this branch; still on GitHub Pages until merged. |
| Subscribe page | Rename to RSS Feeds | **Live** 11 Nov. |
| "New here?" menu | Try it | Preview built (section 3). Can go live from the WordPress menu once the Mission question is settled. |
| `/farmers-market/` | Fold into `/farmers-market-expansion/` | **Live** 11 Nov. |
| Meeting Finder | Roll into Meeting Search | Needs a decision and a theme edit (section 6). |

What was applied on 11 November, through the WordPress REST API with an Administrator application password:

- Content replaced on `/welcome/`, `/community-ambassadors/` and `/community-directory/`.
- `/subscribe/` retitled "RSS Feeds".
- Four redirects added in Redirection (group "Redirections", 301).
- Four pages set to Draft: Local Tips, Newsletters/Blogs/Forums, Find Your Ambassador, Farmers Market.

To undo any page, open it in WordPress and use Revisions, or set a Draft page back to Published and delete its redirect under Tools → Redirection. The site now has 23 published pages, down from 27.

---

## 1. Welcome and ambassador pages

Seven pages become three evergreen pages plus the seasonal Good Neighbor Day page.

| Page | Absorbs | Contents |
|---|---|---|
| `/welcome/` | `/tips/` | Lead, three tiles, a short "Meet your ambassador" strip, then the tips under "Start here" |
| `/community-ambassadors/` | `/ambassador-finder/` | Intro, the only copy of the cards, a switched-off slot for the map, the only copy of the form |
| `/community-directory/` | `/welcome-newsletters-blogs-forums/` | Both Airtable lists under two tabs |
| `/good-neighbor-day/` | | Unchanged |

Surviving pages keep their addresses, so printed links and QR codes keep working.

### Redirects

| Old address | Send to |
|---|---|
| `/tips/` | `/welcome/#start-here` |
| `/welcome-newsletters-blogs-forums/` | `/community-directory/#word-on-the-street` |
| `/ambassador-finder/` | `/community-ambassadors/#find` |
| `/farmers-market/` | `/farmers-market-expansion/` |

The four old pages are in Draft, not Trash, so they can be brought back. All four redirects were checked with and without the trailing slash, and the retired pages are gone from the sitemap.

### Links checked

All 27 pages and 57 posts were scanned for links to the retiring addresses. The only ones are on `/welcome/` and `/tips/` themselves, and the new Welcome page fixes them. Nothing else on the site needs editing.

### Small fixes included

- Belén: Virginia Village (the old Welcome page said Park Towers).
- "Fall Church resident" in Robin's bio.
- Still open: "Ways to be a good neigbor" heading on Good Neighbor Day, and two Welcome tile images that are 700–830 KB.

---

## 2. Ambassador map

- **`/ambassador-finder/`** is in Draft and redirects to the ambassadors page. It is not linked from the homepage or the menu.
- **The GitHub copy** (`index.html` in this repository) had the same zones, contacts and code as the live map, with older colors and fonts. It is deleted on this branch. It was also being served publicly by GitHub Pages at `fcf2023.github.io/FCF-Ambassadors/`, placeholder contacts included. That copy goes away when this branch is merged to `main`. Turning off Pages in the repository settings is the cleaner finish.
- **The live map** is a plain file on the server at `/ambassador-map/`, not a WordPress page. Putting the Finder page in Draft unlinks it, but anyone with the address can still open it and see the placeholder contacts. To take it fully offline, move the `ambassador-map` folder out of `~/fallschurchforward.org` (FileZilla or a DreamHost session). When it is ready, it can be switched on inside the Community Ambassadors page: the draft has a marked slot for it.

---

## 3. "New here?" menu

Previews, rendered with the live theme stylesheet:

- Desktop: [`previews/new-here-desktop.png`](previews/new-here-desktop.png)
- Desktop after scrolling: [`previews/new-here-desktop-scrolled.png`](previews/new-here-desktop-scrolled.png)
- Phone menu: [`previews/new-here-mobile.png`](previews/new-here-mobile.png)

What the test showed:

- **It has to take Mission's place.** Added as a ninth item, the menu wraps onto two lines at every desktop width. Swapped for Mission, it fits. The homepage keeps its mission section, About → Vision covers the same ground, and the footer link to Mission stays.
- **Move the hamburger breakpoint from 1080px to 1140px.** Today's menu wraps between 1081 and 1119px wide. With "New here?" it wraps between 1081 and about 1138px. This rule removes the wrap entirely (tested: phone-style menu up to 1140px, one line from 1141px). It can be pasted into Appearance → Customize → Additional CSS, so no theme file needs editing:

  ```css
  @media (max-width:1140px){
    .nav .navlink, .nav .has-dropdown{display:none}
    .hdr-cta{display:none}
    .menu-btn{display:block}
  }
  ```
- **It is a menu change, not a theme edit.** The header is an ordinary WordPress menu ("Primary Menu 20260803", Appearance → Menus). About is a parent item with four children, and "New here?" would be built the same way: a parent linking to `/welcome/` with three children. It takes a minute to add and a minute to undo.
- **Mission could move instead of going.** Making it the first item under About keeps it reachable from the header.

For reference, this is the markup the theme produces for a dropdown, which is what the previews were built from:

```html
<!-- desktop, in place of the Mission link -->
<div class="has-dropdown"><a class="navlink" href="/welcome/" aria-haspopup="true">New here?[same chevron svg as About]</a>
  <div class="dropdown" role="menu">
    <a role="menuitem" href="/welcome/">Welcome guide</a>
    <a role="menuitem" href="/community-ambassadors/">Community Ambassadors</a>
    <a role="menuitem" href="/community-directory/">Community Directory</a>
  </div>
</div>

<!-- phone menu, in place of the Mission link -->
<div class="mm-group"><span class="mm-group-label">New here?</span>
  <a href="/welcome/">Welcome guide [arrow]</a>
  <a href="/community-ambassadors/">Community Ambassadors [arrow]</a>
  <a href="/community-directory/">Community Directory [arrow]</a>
</div>
```


---

## 4. Subscribe page

Retitle the page from "Subscribe" to "RSS Feeds". The address `/subscribe/` and the footer's "RSS" link stay as they are.

---

## 5. Farmers market

`/farmers-market/` was the older copy. Its sign-up area still showed the placeholder text "[ Sign-up form goes here — reconnect with your WordPress form ]", and its share buttons already point at `/farmers-market-expansion/`. There is nothing on it to carry over. It is now in Draft and redirects to `/farmers-market-expansion/`. The petition page and its Apps Script endpoint were not touched.

---

## 6. Meeting Finder into Meeting Search

No page or post links to Meeting Finder, and it is `noindex`, so there are no links to update.

It is not quite the same search with fewer options. Both use the same index and the same precision rules, but they answer differently. Tested with "Founders Row":

| | Meeting Search | Meeting Finder |
|---|---|---|
| Options | Civic body, date range, summaries / agendas, optional transcripts, sort by relevance / newest / oldest | Search box only |
| What it lists | One row per document, 20 per page | One row per meeting, the whole list on one page, grouped by year |
| "Founders Row" | 136 results (349 with transcripts on) | 222 meetings: 134 discussed it, 88 mentioned it in passing |
| Extras | | Links to the City video and official minutes on each row |

So retiring Finder outright loses three things: one row per meeting, the whole list at once, and the discussed / in passing split.

**Recommended:** add a fourth view to Meeting Search, "Every meeting, by year", beside Relevance / Newest / Oldest. It would call the Finder's existing code (`inc/fcf-ask-enumerate.php`) and respect Search's civic-body and date filters, which Finder cannot do today. Then send `/meeting-finder/` to Meeting Search and put the Finder page in Draft. This is a theme edit for a DreamHost session.

**Quick alternative:** redirect `/meeting-finder/` to Meeting Search with transcripts on and newest first, and accept losing those three things. This can be done at once with the other redirects.

---

## 7. Ambassador space (on hold)

Nothing here is installed, and no page links to a hub. These notes are kept for the discussion.

**Recommendation:** don't build a community inside WordPress. Use three small pieces:

| Piece | Tool | What lives there | Who can get in |
|---|---|---|---|
| Front door | Password-protected page on fallschurchforward.org | Links to everything, a short how-to | Anyone with the shared password |
| Conversation | Private groups.io group (Free plan) | Ideas, questions, announcements, searchable archive | Members you approve |
| Roster and files | Google Drive folder owned by the FCF account | Roster with contact details, flyers, notes | Only the people you share it with |

| Option | Cost | Where people talk | What you maintain | Verdict |
|---|---|---|---|---|
| groups.io Free + hub page + Drive folder | $0 | Email, with a private web archive | Group membership, Drive sharing, one page | Recommended |
| Google Group + hub page + Drive folder | $0 | Email, with a plainer web archive | One list: share the Drive folder with the group address | Good alternative |
| groups.io Premium | $220/year | Email and web | One list: roster, files, wiki and calendar inside the group | Upgrade path |
| Members area inside WordPress | Free and paid plugins | A forum people must remember to visit | Accounts, resets, spam, plugin updates, mail delivery | Not recommended |
| Private channel in the existing Discord | $0 | Chat | Assign a role | Extra, not home base |

groups.io Free covers up to 100 members and includes the email group and its archive, but not files, wiki, calendar or database (checked on groups.io, 10 November 2026). A draft hub page is in [`drafts/ambassador-hub.html`](drafts/ambassador-hub.html), marked on hold.

Open question for the discussion: should ambassadors' email and phone ever be public? The map is built to show them. The suggestion is to keep them in a private roster and route contact through the existing form.

---

## Files

| File | Becomes |
|---|---|
| [`drafts/welcome.html`](drafts/welcome.html) | `/welcome/` |
| [`drafts/community-ambassadors.html`](drafts/community-ambassadors.html) | `/community-ambassadors/` |
| [`drafts/community-directory.html`](drafts/community-directory.html) | `/community-directory/` |
| [`drafts/ambassador-hub.html`](drafts/ambassador-hub.html) | On hold |
| [`previews/`](previews/) | "New here?" menu previews |

The three public drafts reuse the existing copy, images, Airtable views and Tally form. They were rendered against the live theme stylesheet at desktop and phone widths.
