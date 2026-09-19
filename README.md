# MA-NGO

**From your surplus to someone's essential.**

A donor-to-NGO platform: anyone (a family with a pair of shoes, a restaurant with 80 hot meals) posts a donation, and a nearby NGO that asked for it claims it and arranges pickup. A beta volunteer flow matches volunteers to NGOs by skills, causes, availability and distance.

Clickable prototype built for a hackathon review. Single file, no build step.

## Run it
Open `index.html` in a browser, or serve the folder:

    npx serve .

Live demo (after enabling GitHub Pages): Settings, Pages, deploy from branch `main`, folder `/ (root)`.

## Demo flow (60 seconds)
1. **Donor**: choose Business or Family, pick a category, post. Food shows a live "Safe until" timer.
2. **NGO**: the post appears in the feed. Claim it and pick a pickup method within the 10-minute reservation.
3. **Volunteer (beta)**: accept the dispatch, then mark it delivered with an optional proof photo.
4. Watch the donor's status stepper and the impact counter update.

## What is real vs. sample
- Real in the prototype: the full donor, NGO and volunteer flow, safe-window timers, capacity check, category filtering from the NGO's "What we need" list, volunteer match scoring.
- Sample data: all NGOs, donors, and impact numbers are seeded for the demo.
- Assumptions to validate: safe-window hours per food type, and the CO2e estimate (about 0.4 kg food per meal, about 2.5 kg CO2e per kg).
- Not built yet: real backend, auth, push notifications, ID checks for volunteer roles involving children.

## Stack
Plain HTML and JavaScript, Tailwind via CDN, Plus Jakarta Sans, Material Symbols. State is in memory, so a refresh resets the demo.

## Roadmap
- React + Firebase (Firestore, phone auth, FCM)
- Claim transaction so only one NGO can win a donation
- Volunteer verification and safeguarding
- Donor CSR/impact certificates
