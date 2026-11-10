# 🚨 Sentinel Response

> **A public-first emergency response and disaster management platform for fast reporting, location-aware coordination, and incident visibility.**

![Project](https://img.shields.io/badge/project-hackathon-blue.svg)
![Frontend](https://img.shields.io/badge/frontend-HTML%20%7C%20CSS%20%7C%20JavaScript-orange.svg)
![Maps](https://img.shields.io/badge/maps-Leaflet%20%7C%20OpenStreetMap-2E9F6B.svg)
![Storage](https://img.shields.io/badge/storage-browser%20localStorage-purple.svg)
![Status](https://img.shields.io/badge/status-prototype-brightgreen.svg)

---

## 📌 Problem Statement

During fires, road accidents, floods, medical emergencies, and building collapses, reporting is often slowed by fragmented communication, missing location information, and unclear prioritization. Responders need a common operating picture that can accept a report quickly, identify where help is needed, and make the most urgent incidents visible first.

Many emergency tools also assume that the person reporting already has an account or understands a complex workflow. That creates friction at the exact moment when every second matters.

**Sentinel Response** addresses this problem with a browser-based, public-first workflow:

1. Anyone can open the site and submit an incident without signing in.
2. A reporter can capture their current location with one tap.
3. An SOS action creates a critical report immediately and can optionally collect more details afterward.
4. Every report receives a unique name for identification and follow-up.
5. Priority is calculated automatically from the category, description, and reported impact.
6. Coordinators can review incidents, teams, locations, routes, and response analytics in one interface.

> **Prototype note:** this hackathon version persists data in the browser's `localStorage`. It demonstrates the user experience and coordination logic; a production deployment should connect the report action to a secured backend and official emergency-response workflows.

---

## 🚀 Features

| Feature | User Flow | Implementation | Status |
|---|---|---|---|
| **Public incident reporting** | Open the site and report without an account or login. | Modal-based reporting form with local browser persistence. | **Complete** |
| **One-tap SOS** | Tap SOS to create an emergency report immediately. | Captures browser coordinates when permitted, reverse-geocodes the location, and asks whether details should be added. | **Complete** |
| **One-click location capture** | Choose “Use my current location” in a report. | Browser Geolocation API plus OpenStreetMap Nominatim reverse geocoding. | **Complete** |
| **Automatic priority calculation** | Describe what happened and enter the affected-person count. | Rule-based scoring maps emergency keywords, category, and impact to Critical, High, Medium, or Low. | **Complete** |
| **Unique report names** | Identify a report during coordination or follow-up. | Timestamp and random suffix naming such as `RPT-20261110-154500-AB12` or `SOS-RPT-...`. | **Complete** |
| **Incident lifecycle tracking** | Review reported, assigned, in-progress, and resolved incidents. | Filterable incident table with status and team assignment fields. | **Complete** |
| **Response team readiness** | See available responders and their current zones. | Team readiness cards, capacity bars, and availability indicators. | **Complete** |
| **Live location map** | View incidents, available teams, the reporter position, and route line. | Leaflet map with OpenStreetMap tiles and geolocation-aware markers. | **Complete** |
| **Analytics dashboard** | Understand volume, critical reports, teams, and categories. | Summary metrics, activity chart, category donut, and readiness view. | **Complete** |
| **Responsive public UI** | Report from desktop or mobile. | Consistent cards, controls, spacing, and mobile wrapping rules. | **Complete** |

---

## 🏗️ Tech Stack

### Frontend Client

| Component | Role | Technical Rationale |
|---|---|---|
| **HTML5** | Semantic application structure and accessible form controls. | Runs directly in a browser with no build step. |
| **CSS3** | Responsive layout, design tokens, cards, tables, badges, and modal styling. | Keeps the hackathon prototype lightweight and easy to deploy. |
| **Vanilla JavaScript** | Incident state, rendering, filters, forms, SOS flow, and priority rules. | Avoids framework overhead while keeping the demo portable. |
| **Leaflet 1.9.4** | Interactive map, markers, popups, and route visualization. | Small, well-known mapping library with OpenStreetMap support. |

### Browser Services & External APIs

| Service | Role | Notes |
|---|---|---|
| **Geolocation API** | Reads the user's current latitude and longitude after permission. | Requires HTTPS or a trusted local development origin. |
| **OpenStreetMap tiles** | Displays the interactive map. | Attribution is included in the map UI. |
| **Nominatim** | Converts coordinates into a readable address. | Requests may fail gracefully; coordinates remain available. |
| **localStorage** | Stores incident reports in the current browser. | Suitable for a demo, not shared multi-user production storage. |

---

## 📂 Project Structure

```text
sentinel-emergency-response/
├── index.html       # Application shell, views, navigation, and report modal
├── styles.css       # Design system, responsive layout, cards, tables, and map UI
├── app.js           # State, rendering, geolocation, SOS, priority rules, and events
└── README.md        # Project documentation
```

---

## ⚙️ Installation & Setup

### Prerequisites

- A modern browser such as Chrome, Edge, Firefox, or Safari.
- A local static web server for reliable geolocation permissions.
- Internet access for Leaflet, OpenStreetMap tiles, and address lookup.

### Step 1: Clone the Repository

```bash
git clone https://github.com/turtel2025/bug-free-funicular.git
cd bug-free-funicular
```

### Step 2: Run the Static Application

The project has no package installation step. Serve the folder with any static server.

**Python:**

```bash
python -m http.server 5500
```

Then open:

```text
http://localhost:5500
```

**VS Code Live Server:**

1. Open the cloned folder in VS Code.
2. Install or enable Live Server.
3. Open `index.html` with **Open with Live Server**.

> Opening the file directly with `file://` can restrict geolocation in some browsers. Use a local server when testing location capture.

### Step 3: Test Public Reporting

1. Select **Report incident**.
2. Enter what happened and choose a category.
3. Use **Use my current location** or enter a location manually.
4. Add the number of people affected.
5. Confirm that **Calculated priority** updates automatically.
6. Send the report and note its unique report name.

### Step 4: Test SOS

1. Select **SOS**.
2. Allow location access if prompted.
3. Confirm the generated report name.
4. Choose whether to add details after the emergency report is created.

---

## 🧠 How It Works

Sentinel Response is organized around a short public-to-coordination flow:

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                         SENTINEL RESPONSE FLOW                              │
├─────────────────────────────────────────────────────────────────────────────┤
│  1. PUBLIC REPORTING                                                        │
│     Visitor opens the site ➜ chooses Report incident or SOS                 │
├─────────────────────────────────────────────────────────────────────────────┤
│  2. LOCATION CONTEXT                                                        │
│     Browser coordinates ➜ optional reverse geocoding ➜ map-ready position   │
├─────────────────────────────────────────────────────────────────────────────┤
│  3. AUTOMATIC PRIORITIZATION                                                │
│     Category + description + affected people ➜ calculated priority           │
├─────────────────────────────────────────────────────────────────────────────┤
│  4. IDENTIFICATION & STORAGE                                                │
│     Unique report name ➜ browser localStorage ➜ incident table and dashboard │
├─────────────────────────────────────────────────────────────────────────────┤
│  5. COORDINATION                                                            │
│     Incident markers + team markers ➜ selected incident ➜ route visualization│
└─────────────────────────────────────────────────────────────────────────────┘
```

### 1. Public Report and SOS Pipeline

The regular report flow opens a form for incident details. The SOS flow skips the form and immediately creates a Critical emergency report with the current position when available. After the report is saved, the reporter can optionally add more context without delaying the initial alert.

Both flows use the same report model, so SOS and regular reports appear consistently in the dashboard, incident table, and map.

### 2. Location Pipeline

1. The browser requests permission through `navigator.geolocation`.
2. Latitude and longitude are stored on the report.
3. Sentinel requests a readable address from Nominatim when possible.
4. If address lookup fails, the exact coordinates remain visible as the fallback.
5. The live map centers on the reporter and draws a visual line to selected incident markers.

### 3. Automatic Priority Pipeline

Priority is never typed by the reporter. `calculateSeverity()` evaluates:

- Emergency terms such as `SOS`, `trapped`, `collapse`, `unconscious`, `explosion`, or `large fire`.
- Incident category such as fire, medical emergency, accident, flood, or rescue.
- The number of people affected.

The result is shown as a read-only calculated badge and is recalculated when the report is created or edited.

| Priority | Example triggers |
|---|---|
| **Critical** | SOS, life-threatening language, collapse, explosion, large impact, or 10+ people affected |
| **High** | Fire, accident, collision, medical emergency, injury, flood, rescue, or 5+ people affected |
| **Medium** | Road, traffic, smoke, power, water, damage, or 2+ people affected |
| **Low** | No high-risk keyword and fewer than 2 people affected |

### 4. Report Identification

Each report receives a generated name using a prefix, UTC date/time, and a random suffix. This avoids relying only on a row number and gives responders a compact identifier to communicate over radio, phone, or chat.

Examples:

```text
RPT-20261110-154500-AB12
SOS-RPT-20261110-154503-7XQK
```

### 5. Dashboard and Map Rendering

The browser keeps one incident collection and derives every surface from it:

- Overview metrics count active and critical incidents.
- Priority incidents are sorted by calculated severity.
- The incident table supports report-name, title, category, and location search.
- Team cards show readiness and available capacity.
- The live map renders active incident and available-team markers.

---

## 📈 Scalability

The current version is intentionally a small hackathon prototype. Its client-side separation provides a clear path to a production architecture:

1. **API-backed report storage:** replace `localStorage` with authenticated or public-safe API endpoints and a shared database.
2. **Real team coordination:** move team status and assignment state to a server so all dispatchers see the same updates.
3. **Realtime updates:** use WebSockets or Server-Sent Events to stream newly created reports and status changes.
4. **Geospatial queries:** store coordinates in a spatial database to find the nearest suitable team rather than using demo offsets.
5. **Queue-based SOS handling:** send SOS reports through a durable queue with retry and acknowledgement semantics.
6. **Rate limiting and abuse protection:** protect public endpoints from spam while keeping emergency reporting accessible.

---

## 💡 Feasibility

- **Low deployment cost:** the current static app can be hosted by GitHub Pages, Netlify, Vercel, or any ordinary web server.
- **Fast public access:** there is no account creation or login gate for reporting.
- **Graceful degradation:** manual location entry works when permission is denied, and coordinates remain available when reverse geocoding fails.
- **Incremental backend path:** the report object already contains the fields needed for an API model: name, category, severity, location, coordinates, impact, status, team, and description.
- **Demo-ready UX:** seeded incidents and response teams make the dashboard understandable immediately during a hackathon presentation.

---

## 🌟 Novelty & Comparative Analysis

### Competitive Matrix

| Capability | Sentinel Response | Generic Contact Form | Manual Phone/Chat Coordination | Full Dispatch Suite |
|---|---|---|---|---|
| No-login public reporting | ✅ | ✅ | ✅ | ⚠️ Often account-based |
| One-tap SOS | ✅ | ❌ | ⚠️ Depends on operator | ✅ |
| Automatic location capture | ✅ | ❌ | ⚠️ Caller must describe it | ✅ |
| Automatic priority | ✅ Rule-based | ❌ | ❌ Manual judgement | ✅ |
| Unique report identity | ✅ | ⚠️ Often absent | ❌ | ✅ |
| Live map and team visibility | ✅ Prototype | ❌ | ❌ | ✅ |
| Setup complexity | 🚀 Static web app | 🚀 Low | 🚀 Low | ⏳ High |

### Core Innovation: Public-First Emergency Context

Sentinel Response combines the lowest-friction reporting experience with the context a coordinator needs: a unique report name, location coordinates, automatic priority, affected-person count, and a map view. The SOS path deliberately separates **speed of initial reporting** from **optional detail collection**, so a reporter is not forced to complete a long form before help can be coordinated.

---

## 🔧 Feature Depth & Edge-Case Engineering

### 1. Robust Edge-Case Handling

- **Location permission denied:** the reporter can enter an address manually.
- **Geolocation unavailable:** SOS still creates a report and marks the location for follow-up.
- **Reverse-geocoding failure:** latitude and longitude remain stored and displayed.
- **Repeated report names:** the timestamp plus random suffix makes collisions highly unlikely.
- **Long addresses and titles:** cards and table cells use truncation and responsive wrapping.
- **Small screens:** action buttons wrap, map details move below the map, and tables remain horizontally scrollable.
- **Existing stored reports:** older demo records receive stable display names and their priority is recalculated when loaded.

### 2. Standardized Report Schema

```json
{
  "id": "INC-1731253500000",
  "reportName": "SOS-RPT-20261110-154503-7XQK",
  "title": "SOS emergency request",
  "category": "Other Emergency",
  "severity": "Critical",
  "location": "Captured address or coordinates",
  "latitude": 12.845,
  "longitude": 80.012,
  "affected": 10,
  "status": "Reported",
  "team": "Unassigned",
  "time": "Just now",
  "description": "Emergency report sent using the SOS button."
}
```

### 3. Production Hardening Required

Before real emergency use, the prototype must add:

- A backend with durable, shared storage.
- Server-side severity and validation so client code cannot be trusted.
- Secure operator authentication and role-based permissions.
- Official emergency service integrations and escalation rules.
- Abuse prevention, audit logs, encryption, and monitoring.
- Clear local emergency-number guidance and an operational support process.

---

## ⚠️ Ethical Use & Operational Disclaimer

Sentinel Response is a hackathon prototype and is not a replacement for calling local emergency services. In a real emergency, contact the appropriate official emergency number first.

The current client-side storage is not a reliable dispatch system: reports are only stored in the browser that created them and are not automatically delivered to responders. Do not use this prototype to transmit sensitive medical, personal, or confidential information.

---

## 📜 License

This hackathon project does not currently declare a formal open-source license. All rights remain with the project authors unless a license is added to the repository.

---

## 🧩 Author & Team

Built for **Code Clash 2026 — Emergency Response & Disaster Management Platform**.

Repository: [turtel2025/bug-free-funicular](https://github.com/turtel2025/bug-free-funicular)

