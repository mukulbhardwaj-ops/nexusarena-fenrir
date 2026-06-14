# WD-001: NexusArena - Online Gaming Website

**Category:** Web Development

---

## Context

NexusArena is a web-based competitive esports tournament management platform being built for amateur and semi-professional gaming communities across India and Southeast Asia. The platform allows players to register accounts, join or create tournaments across five game titles, track live bracket progressions, and follow per-title leaderboards. The immediate use case is MVP validation - NexusArena Pvt. Ltd. needs a publicly deployed, fully functional platform to demonstrate to early adopters and community managers before a wider marketing launch.

This milestone covers the complete frontend and backend of the NexusArena platform as a deployable MVP. It does not include a native mobile application, live video streaming, payment gateway integration, in-platform chat, or third-party game API connections for automatic result verification.

---

## Project Information

| Field | Details |
|---|---|
| Project ID | WD-001 |
| Category | Web Development |
| Project Type | Competitive Esports Tournament Management Web Platform |
| Client / Brand | NexusArena Pvt. Ltd. |
| Platform / Medium | React.js frontend, Node.js + Express.js backend, MongoDB database, deployed on Vercel or Railway or equivalent public URL |
| Deliverable Type | Deployed public URL + GitHub repository link + source code ZIP + README.md |
| Primary Goal | Build a fully functional competitive esports tournament platform where players can register, join tournaments, track live brackets, and follow leaderboards across five supported game titles |

---

## Main Goal

Build and deploy a complete web platform named NexusArena that supports the following three core workflows:

1. Player registration, login, and profile management
2. Tournament discovery, registration, creation, bracket generation, and result management
3. Leaderboard tracking per game title with automatic rank updates within 5 minutes of result finalisation

---

## About NexusArena Pvt. Ltd.

NexusArena Pvt. Ltd. is a fictional startup focused on building community-driven esports infrastructure for casual and semi-professional gamers. The company has no existing platform, no brand assets, and no backend infrastructure. This project is the first build from scratch.

**Brand tone:** Competitive, clean, community-focused
**Brand line:** `Compete. Rise. Dominate.`

---

## Supported Game Titles

The platform must support exactly the following five game titles at launch. No titles may be added or removed.

1. Valorant
2. FIFA
3. Chess
4. Call of Duty
5. Clash Royale

Each game title requires:
- A dedicated leaderboard page accessible from main navigation
- A filterable tournament section
- A game title label on all tournament cards and detail pages

---

## User Roles

The platform must implement exactly three user roles.

| Role | Assignment | Core Permissions |
|---|---|---|
| Player | Default on registration | Browse, search, join, and withdraw from tournaments; view brackets and leaderboards |
| Organiser | Any verified player who creates a tournament | Inherits Player permissions; create, edit, cancel own tournaments; trigger bracket generation; submit match results; declare final winner |
| Admin | Assigned manually - not self-registerable | View, suspend, delete any user; view and remove any tournament; view platform-wide statistics |

**Role constraints:**
- Unverified accounts cannot join or create tournaments
- Admin accounts cannot participate in tournaments
- Organiser permissions apply only to tournaments that user created

---

## Requirements

The freelancer will build a fully functional web platform covering user authentication, tournament management, bracket generation, leaderboards, notifications, and an admin panel.

### User Authentication and Account Management

1. User registration form must collect username, email address, and password. All three fields are mandatory.
2. Email verification must be triggered on account creation. Unverified accounts cannot join or create tournaments.
3. Login must use email and password. JWT-based session management is required. Tokens stored in HTTP-only cookies with 7-day expiry.
4. Password reset must be delivered via email link. The reset link must expire after 24 hours.
5. User profile page must display username, avatar, list of game titles followed, tournaments joined, win count, loss count, and current leaderboard rank per game title.
6. Avatar upload must accept PNG and JPG formats only. Maximum file size is 2 MB. Files exceeding 2 MB or in wrong format must be rejected with an error message.

### Field Validation Rules

| Field | Rule |
|---|---|
| Username | 3-20 characters; alphanumeric and underscores only; must be unique |
| Email | Standard email format; must be unique across all users |
| Password | Minimum 8 characters; at least one uppercase, one lowercase, one number |
| Tournament Name | Maximum 60 characters; no HTML tags permitted |
| Slot Limit | Integer only; minimum 4, maximum 128 |
| Rules Text | Plain text only; maximum 1000 characters |
| Prize Pool | Numeric only; greater than zero if entered; optional field |
| Avatar | PNG or JPG format only; maximum file size 2 MB |

### Tournament Discovery and Browsing

1. Homepage must display three sections: Featured Tournaments (maximum 3 cards), Recently Added Tournaments (maximum 6 cards), and Active Tournaments (maximum 6 cards).
2. Tournament filter must support filtering by game title (dropdown with all five supported titles), status (open, ongoing, completed), and format (single elimination, double elimination, round robin).
3. Tournament search must return results matching the tournament name string. Partial matches must be supported.
4. Individual tournament detail page must display: game title, tournament name, format, prize pool (if set), registration deadline, start date, total slot count, current registration count, rules text, and the bracket diagram.

### Tournament Registration

1. A Register button must appear on the tournament detail page for any open tournament the logged-in player has not yet joined.
2. Registration must close automatically when the slot count is reached or the registration deadline passes. The Register button must be replaced with a Closed label in both cases.
3. A confirmation email must be sent to the player within 5 minutes of successful registration.
4. A Withdraw button must appear on the tournament detail page for any open tournament the logged-in player has already joined. Withdrawal is permitted only before the registration deadline. After the deadline the Withdraw button must not appear.

### Tournament Creation and Management

1. Any registered and verified user may create a tournament by completing a form with the following mandatory fields: game title (one of the five supported titles), tournament name (maximum 60 characters), format (single elimination, double elimination, or round robin), slot limit (minimum 4, maximum 128), registration deadline (date and time picker), start date (must be after registration deadline), and rules (plain text, maximum 1000 characters).
2. Prize pool is an optional field. If entered, it must accept only a numeric value greater than zero.
3. Organisers may edit tournament name, rules, and prize pool before the registration deadline. Game title, format, and slot limit cannot be edited after creation.
4. Organisers may cancel a tournament before its start date. Cancellation must trigger an email notification to all registered players.
5. Organisers may manually trigger bracket generation after the registration deadline closes. Bracket generation is not automatic.
6. Organisers submit match results by selecting the winner on the bracket diagram. Only the organiser of a tournament may submit results for that tournament.
7. Organisers declare the final winner from the bracket final match result screen.

### Bracket System

1. Single elimination brackets must be generated from the registered player list on organiser trigger. Players are eliminated after one loss.
2. Double elimination brackets must be generated with a winners bracket and a losers bracket. Players are eliminated after two losses.
3. Round robin brackets must pair every registered player against every other registered player once. Final ranking by total wins then total games played.
4. If the registered player count is not a power of 2 for single or double elimination formats, byes must be assigned randomly to fill the bracket.
5. The bracket diagram must display as an interactive visual tree on the tournament detail page showing all rounds.
6. The bracket diagram must update within 30 seconds of a match result being submitted by the organiser.

### Leaderboards

1. Each of the five supported game titles must have a dedicated leaderboard page accessible from the main navigation.
2. Leaderboard entries must be ranked by total tournament wins descending. Ties are broken by total matches played descending.
3. Each leaderboard row must display: rank number, player avatar, username, total wins, and total matches played.
4. Leaderboard data must update within 5 minutes of a tournament result being finalised by the organiser.
5. Leaderboard must display a minimum of 50 rows per page with pagination for additional entries.

### Notifications

1. Email notifications must be sent for the following events: registration confirmation, tournament start (sent at start date), match result submission (sent to both players in the match), and tournament completion (sent to all registered players).
2. An in-platform notification bell icon must display the count of unread notifications as a badge.
3. A notification history page must list all past notifications for the logged-in user in reverse chronological order.

### Email Notification Events

All emails must be sent within 5 minutes of the triggering event.

| Event | Trigger | Recipients | Required Content |
|---|---|---|---|
| Registration Confirmation | Player registers for a tournament | Registering player | Tournament name, start date, organiser name |
| Tournament Start | Start date is reached | All registered players | Tournament name, bracket link |
| Match Result Submitted | Organiser submits a match result | Both players in the match | Tournament name, round, result per player |
| Tournament Completion | Organiser declares final winner | All registered players | Tournament name, winner username, final bracket link |
| Tournament Cancellation | Organiser cancels before start date | All registered players | Tournament name, cancellation reason if provided |

### Admin Panel

1. The admin panel must be accessible only to users with the admin role. Non-admin users attempting to access admin routes must be redirected to the homepage.
2. Admins must be able to view a table of all registered user accounts with columns for username, email, registration date, and account status.
3. Admins must be able to suspend or delete any user account from the user table.
4. Admins must be able to view and remove any tournament from a tournament management table.
5. The admin dashboard must display the following platform statistics: total registered users, total tournaments created, and total matches completed as integer values.

### Admin Dashboard Statistics Definitions

| Statistic | Definition |
|---|---|
| Total Registered Users | Count of all user accounts regardless of verification status |
| Total Tournaments Created | Count of all tournament records regardless of status (open, ongoing, completed, cancelled) |
| Total Matches Completed | Count of all bracket matches that have had a result submitted by an organiser |

---

## Visual and Technical Specs

### Responsive Breakpoints

- **Desktop:** 1920 x 1080 px
- **Tablet:** 768 x 1024 px
- **Mobile:** 375 x 812 px
- **Horizontal scrolling:** Not permitted on any supported screen size

### Browser Support

| Browser | Version |
|---|---|
| Chrome | Latest |
| Firefox | Latest |
| Edge | Latest |
| Safari | Latest |

---

## Technical Requirements

- **Frontend Framework:** React.js v18 or later
- **Backend Framework:** Node.js with Express.js
- **Database:** MongoDB with Mongoose ODM
- **Authentication:** JWT tokens in HTTP-only cookies; 7-day expiry
- **Email Delivery:** Any free-tier transactional email service (Nodemailer + Gmail SMTP, SendGrid free tier, Mailgun sandbox, or equivalent)
- **Platform / Target:** Desktop and mobile responsive web browser
- **Deployment:** Publicly accessible URL; accepted hosts: Vercel, Netlify, Railway, Render, or equivalent free-tier service
- **Code quality:** All source functions carry inline comments explaining their purpose; files organised into sensibly named folders

### Not Allowed

- Native mobile applications (iOS or Android)
- Live video streaming of matches
- In-platform chat or messaging between users
- Payment gateway integration
- Third-party game API integration for automatic result verification
- Multi-language support
- Paid plugins or paid third-party services

---

## Deliverables

| # | Item | Format | Notes |
|---|---|---|---|
| 1 | Deployed platform public URL | URL | Must be live and accessible at time of submission. Must load the NexusArena homepage without errors. |
| 2 | GitHub repository link | URL | Repository must be public. Must contain complete source code. |
| 3 | Source code ZIP | .zip | Complete frontend and backend source code. Must not exceed 500 MB. |
| 4 | README.md | .md | Must include: project title, tech stack, local setup instructions, environment variable list, and deployed URL. |

### File Naming Convention

All delivered files must follow this exact pattern:
nexusarena_[item-name]_v1.[ext]

**Example:** nexusarena_source_v1.zip

Rules:
- Lowercase and hyphen-separated
- No spaces
- No alternate naming structures

### Required Folder Structure
nexusarena/

frontend/

src/

components/

pages/

utils/

public/

package.json

backend/

routes/

controllers/

models/

middleware/

server.js

package.json

README.md

---

## Scope Boundaries

### DO
- Build all features listed in the Requirements section
- Use free and open-source packages and libraries
- Use placeholder game title logos or icons where needed
- Deploy to a free-tier hosting service

### DO NOT
- Build a native mobile app
- Integrate live video streaming
- Integrate a payment gateway
- Use paid plugins or paid third-party APIs
- Add game titles beyond the five specified
- Build multi-language support

---

## Developer's Choices

| Decision | Accepted Options |
|---|---|
| Frontend component library | Material UI, Chakra UI, Tailwind CSS, or plain CSS |
| Email delivery service | Nodemailer + Gmail SMTP, SendGrid free tier, Mailgun sandbox, or equivalent free tier |
| Hosting platform | Vercel, Netlify, Railway, Render, or equivalent free-tier service |
| Bracket diagram library | Any open-source bracket visualization library |

---

## Quality Control / Pre-Submission Checklist

Before submitting, confirm all of the following:

1. [ ] The deployed URL loads without errors on Chrome latest.
2. [ ] User registration, email verification, login, and password reset all function correctly.
3. [ ] Tournament creation, registration, withdrawal, and cancellation all function correctly.
4. [ ] Bracket generation works for all three formats: single elimination, double elimination, round robin.
5. [ ] Leaderboard pages exist for all five game titles and update within 5 minutes of result finalisation.
6. [ ] Admin panel is inaccessible to non-admin users.
7. [ ] All pages are responsive at 1920 x 1080, 768 x 1024, and 375 x 812 without horizontal scrolling.
8. [ ] README.md contains project title, tech stack, setup instructions, environment variable list, and deployed URL.
9. [ ] Source code is organised per the required folder structure.
10. [ ] No console errors appear on the homepage, tournament list page, or leaderboard pages.

---

## Acceptance Checklist

1. [ ] Deployed public URL is live and loads the NexusArena homepage without errors in Chrome latest.
2. [ ] GitHub repository is public and contains complete source code.
3. [ ] User can register, verify email, log in, and reset password end-to-end.
4. [ ] User profile page displays username, avatar, tournaments joined, win count, loss count, and rank per game title.
5. [ ] Avatar upload rejects files larger than 2 MB with an error message.
6. [ ] Avatar upload rejects files that are not PNG or JPG with an error message.
7. [ ] Homepage displays Featured (max 3), Recently Added (max 6), and Active (max 6) tournament sections.
8. [ ] Tournament filter works by game title, status, and format.
9. [ ] Tournament detail page displays all required fields including bracket diagram.
10. [ ] Tournament registration closes automatically at slot limit and at registration deadline with Closed label.
11. [ ] Bracket generates correctly for single elimination, double elimination, and round robin formats.
12. [ ] Byes are assigned when registered player count is not a power of 2 for elimination formats.
13. [ ] Bracket diagram updates within 30 seconds of match result submission.
14. [ ] Five dedicated leaderboard pages exist and are accessible from main navigation.
15. [ ] Leaderboard updates within 5 minutes of tournament result finalisation.
16. [ ] Admin panel is accessible only to admin role users.
17. [ ] Admin dashboard displays total users, total tournaments, and total matches completed as integers.
18. [ ] All pages render without horizontal scrolling at 375 x 812 screen width.
19. [ ] README.md contains project title, tech stack, setup instructions, environment variables, and deployed URL.
20. [ ] Source code folder structure matches the required layout exactly.

---

## Evaluation Criteria

The project will be evaluated against the following points:

- **User authentication:** Registration, email verification, login, and password reset all function correctly end-to-end
- **Tournament lifecycle:** Creation, registration, bracket generation, result submission, and winner declaration complete without errors
- **Bracket correctness:** Single elimination, double elimination, and round robin all generate correctly with byes where required
- **Leaderboard accuracy:** Rankings update within 5 minutes of result finalisation across all five game titles
- **Responsive design:** No horizontal scrolling at 375 x 812, 768 x 1024, and 1920 x 1080 viewports
- **Admin panel security:** Non-admin users cannot access admin routes under any circumstances
- **Code quality:** All functions carry inline comments and folder structure matches the required layout exactly
- **Deployment:** Public URL is live and loads without errors at time of submission

---

## Delivery Terms

- **Revisions included:** 1 round of minor revisions
- **Allowed revision types:** Bug fixes for features listed in the Requirements section, UI layout corrections, broken link fixes
- **What does not count as a revision:** Addition of new features not listed in Requirements, change of tech stack, redesign of the bracket system
- **Delivery method:** Submit the deployed public URL, public GitHub repository link, and source code ZIP via the submission form

---

## Final Goal

The completed NexusArena platform is a publicly accessible, fully functional esports tournament management website where players can register accounts, join and create tournaments across five supported game titles, track live bracket progressions, and compete for positions on per-title leaderboards. The platform handles the full tournament lifecycle from creation through bracket generation to result finalisation, sends email notifications at all key events, and provides administrators with a management panel for user and tournament oversight. A first-time visitor arriving at the deployed URL must be able to register an account, browse open tournaments, and join a tournament without any guidance beyond the platform interface itself.
