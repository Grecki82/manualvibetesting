# BookNow — Capstone Requirements

**Project:** BookNow — Hotel Room Booking (web app)
**Used in:** the Capstone Project. This is the spec you verify the app against.
**App:** `capstone/booknow-broken/` (buggy) and `capstone/booknow-fixed/` (clean).

> This is your independent project. Explore the app, design test cases from this spec, and
> report the bugs you find. The bug count is **not disclosed** here — finding them is the job.
> A known-bugs answer key exists, but open it **only after** you finish.

---

## 1. In Scope

### 1.1 Login
- Users sign in with an email and a password.
- The password field must **mask input** (`type="password"`).
- Both fields are required — an empty submission is rejected with a visible error.
- Valid credentials: **guest@booknow.com / stay2026**.
- Wrong credentials show a visible error (`#login-error`) and stay on the login page.
- A successful sign-in navigates to the Rooms page.
- The **navbar is hidden** on the login page and appears only after authentication.
- There is an **auth guard**: Rooms, Booking, and Confirmation are not reachable without
  logging in first.

### 1.2 Rooms
- A grid of rooms; each card shows: name, description, image (valid `src`, with descriptive
  `alt` text), nightly price after discount, a discount badge, an **Available** badge, and a
  Book action.
- Rooms and pricing: Deluxe $129 (20% off), Superior $89 (10% off), Family Suite $199
  (15% off), Penthouse $299 (5% off).
- **Discount math:** discounted price = `price × (1 − discount / 100)`. Example: Deluxe at
  $129 with 20% off = **$103.20**.
- Long descriptions must **clamp within the card** (no overflow that breaks the grid).
- The **Available** badge must render in **green**.

### 1.3 Booking
- Selecting a room opens the booking form for that room.
- Fields: First/Last Name, Email, Phone, Check-in date, Check-out date, Guests.
- **All fields required** — an empty or malformed submission is rejected.
- **Email** must be a valid format (`/^[^\s@]+@[^\s@]+\.[^\s@]+$/`).
- **Phone** must contain only digits and phone punctuation (no letters).
- **Check-out date must be after the check-in date.**
- **Guests must be at least 1** (no zero or negative).
- **Nights = days between check-in and check-out**, and the **total updates when the dates
  change**. Total = discounted nightly price × nights.

### 1.4 Confirmation
- On a successful booking, the confirmation page shows:
  - a **booking summary** (room, dates, guest name, number of guests, nights, total), and
  - a **booking reference number** (e.g. `BKN-` + a 6-digit number).

### 1.5 General
- The browser tab **title** must read a real name (e.g. "BookNow — Hotel Room Booking"),
  not "Untitled".

---

## 2. Out of Scope
- Real payment processing, live availability/inventory, user registration and password reset,
  account/profile pages, email confirmations, multi-currency, and search/filtering.

## 3. Technical Context
- Static web app: `index.html`, `style.css`, `app.js`. Open `index.html` directly in a
  browser — no server needed. Data and auth are in-app/mocked.
- Credentials hardcoded: guest@booknow.com / stay2026.

## 4. Your Task (Capstone)
1. Explore BookNow and compare it against this spec.
2. Design test cases (positive, negative, edge) with your test-case-design skill.
3. Execute them against the broken app; write professional bug reports for what you find.
4. Verify each fix against the fixed app.
5. **Only after you finish**, compare your findings to `resources/known-bugs-booknow.md`.
