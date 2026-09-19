# MA-NGO

**From your surplus to someone's essential.**

PassItOn connects anyone who has something to give (a family with a pair of outgrown school shoes, a caterer with 40 hot meals left after an event) to the NGO nearby that actually needs it, and gets it there before it goes to waste. A beta feature also matches volunteers to the NGOs that suit their skills, interests and schedule.

> Status: clickable prototype built for a hackathon review. The full flow works end to end in the browser. The backend is planned, not built (see [Prototype status](#prototype-status)).

---

## The problem

Edible food and usable goods are thrown away every day while NGOs run short of exactly those things.

- The UN Environment Programme's Food Waste Index Report 2024 estimates the world wasted about **1.05 billion tonnes of food in 2022**, while hundreds of millions of people faced hunger. It puts India's figure at roughly **78 million tonnes a year** (household level). Check the report before quoting exact numbers in a slide.
- Weddings, banquets, caterers and canteens routinely end up with large batches of cooked food nobody will eat.
- Households hold shoes, clothes and books that are still good and that shelters and schools need.

Why does it keep happening when both sides want to fix it?

1. **Cooked food has a short window.** A caterer with 40 meals at 9 PM has a few hours, not days. Finding an NGO by phone calls is too slow.
2. **Donors don't know who needs what.** A family with three pairs of size 5-7 school shoes has no idea which NGO wants them, so the shoes stay in a cupboard.
3. **NGOs can't take everything.** A shelter with limited storage and a fixed dinner service can't accept an unpredictable 100 meals, and can't easily say what it actually needs.
4. **The last mile is the real bottleneck.** Listing a donation is easy. Someone has to collect it in time.
5. **Willing volunteers can't find the right place.** People who want to help don't know which NGO needs their particular skills on their free evenings.

## How PassItOn solves it

One network with three sides: **Donors → NGOs → Volunteers.**

| Who | What they do in PassItOn |
|---|---|
| **Donor** (individual or business) | Pick a category and post in under a minute. Food shows a live "Safe until" timer. See a live radar of what nearby NGOs need and tap **Fulfill**. |
| **NGO** | Publish a "What we need" list (categories, meals, shoe sizes, diet). Get a live feed of matching donations only. Claim, choose how it will reach you, confirm receipt with a photo. |
| **Volunteer** (beta) | Build a profile (skills, causes, availability, distance). Get ranked NGO matches with reasons, offer to help for a shift, and accept pickup dispatches from NGOs. |

### The core loop

```
Donor posts  →  matching NGOs are notified  →  one NGO claims (reserved 10 min)
     →  pickup arranged (volunteer, NGO van, or donor drop-off)
     →  NGO confirms receipt with a proof photo  →  impact counter updates
```

## What makes it work

- **Safe-window timer for cooked food.** The donor gives the food type and cooked time. The app computes a "Safe until" time and shows a live countdown. Expired food can't be posted and disappears from NGO feeds. *The hours per food type are placeholder assumptions until validated with food-safety guidance.*
- **Two donation modes, one pipeline.** Cooked food is urgent: countdown, 10-minute claim reservation, red alert when the window is nearly closed. Goods (shoes, clothes, books, other) are scheduled: flexible pickup window, no clock pressure.
- **NGO "What we need" routing.** NGOs choose which categories they accept and what they need right now. Their feed only shows matching donations, and every donor sees their needs on the Give screen. This is what solves "who wants my shoes?".
- **Capacity check.** A shelter can't claim more meals than it can take tonight. Over-capacity claims are blocked.
- **Claim reservation and release.** A claimed donation is held for 10 minutes. If it isn't confirmed, or the NGO taps release, it goes back to the pool for the next NGO.
- **Three pickup options.** Volunteer dispatch (beta), the NGO collects, or the donor drops off. Volunteer dispatch is what turns the last mile from a bottleneck into a one-tap task.
- **Proof of handover.** The receiving side can attach a photo when confirming. The donor's status tracker shows it, which builds trust on both sides.
- **Live impact counter.** Items and meals given, hot meals rescued, and a weekly chart, updated as handovers are confirmed.

### Volunteer matching (beta)

Each NGO is scored 0-100 against the volunteer's profile:

| Factor | Weight |
|---|---|
| Skills overlap | 35 |
| Causes overlap | 30 |
| Weekly availability overlap | 25 |
| Distance (closer is better, within the chosen radius) | 10 |

Each match shows why it matched (shared skills, causes, shifts that fit, distance). NGOs beyond the volunteer's radius are hidden. Roles around children are flagged as needing ID checks and NGO supervision, which are not built yet.

## Who benefits

- **Donors:** an easy way to give, knowing it reaches someone who asked for it.
- **NGOs:** predictable, relevant donations, less phone-chasing, and a way to signal real needs.
- **Volunteers:** a clear place to help that fits their skills and time.
- **Communities:** less edible food wasted and more essentials in the right hands.

## SDG alignment

- **SDG 2 (Zero Hunger):** surplus meals reach people who need them.
- **SDG 12 (Responsible Consumption and Production), target 12.3:** reduces edible food waste, and gives reusable goods a second life.
- **SDG 17 (Partnerships):** connects donors, NGOs and volunteers on one network.

## Prototype status

**Working in the prototype**
- Full donor, NGO and volunteer flow with role switching
- Adaptive donation form, safe-window timers, claim reservation, capacity check
- NGO needs editor that filters the feed and updates the donor radar
- Status tracker, proof photo (real file upload, kept in memory), live impact dashboard
- Volunteer profile, match scoring, shift offers, and dispatch accept/decline

**Sample or assumed**
- All NGOs, donors, volunteers and impact numbers are seeded demo data.
- Safe-window hours per food type are placeholders.
- The CO2e figure assumes about 0.4 kg of food per meal at about 2.5 kg CO2e per kg. Replace with a cited factor before presenting it as fact.
- Distances and ETAs are static estimates.

**Not built yet**
- Backend, real accounts and login, push notifications, and real NGO verification
- Volunteer background checks and child-safeguarding rules
- Food-safety compliance checks against local regulations
- Real geolocation and routing

## Run it

No build step. Open `index.html` in a browser, or serve the folder:

```
npx serve .
```

To host it free, use GitHub Pages: Settings, Pages, deploy from branch `main`, folder `/ (root)`.

### 60-second demo
1. **Donor:** switch between Business and Family, pick a category, and post. Try food with an old cooked time to see the safe-window block.
2. **NGO:** open the feed, claim the food, choose Volunteer dispatch, and confirm.
3. **Volunteer:** accept the dispatch and mark it delivered with a photo.
4. **NGO** confirms receipt if needed, then check the donor's status tracker and the impact dashboard.
5. **Volunteer** tab: edit the profile and see the NGO match ranking change.

## Tech stack

- **Now:** a single HTML file with plain JavaScript, Tailwind via CDN, Plus Jakarta Sans and Material Symbols. State lives in memory, so a refresh resets the demo.
- **Planned production backend (Firebase):** Firestore for donations and live status, Auth with phone OTP, Cloud Storage for proof photos, FCM for volunteer pings, and a Firestore transaction so only one NGO can claim a donation.

```
index.html   the whole prototype (UI, data, logic)
README.md    this file
```

## Roadmap
1. React + Firebase (Firestore, phone auth, Storage, FCM) with security rules
2. Transactional claims and a server-side claim timeout
3. NGO verification and volunteer safeguarding
4. Real distance and routing, and radius search
5. Donor impact and CSR certificates, plus waste-pattern analytics for businesses
6. Native Android app for volunteers (background location, reliable push)

## Design
Palette and type come from a Google Stitch design pass (Plus Jakarta Sans, warm amber and olive tokens), with light and dark themes.
