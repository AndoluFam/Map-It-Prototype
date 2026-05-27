# Map-It-Prototype
Map-It is a real-time event mapping platform that helps multicultural communities stay connected. Plant yourself on a live world map, see where everyone is scattered globally, and share moments through time-limited photos. Built as a 2-hour prototype at a graduation party—because the blues of distance shouldn't mean the end of friendships.

# MindTheMap 🌍

**Real-time event mapping for communities staying connected across continents.**

Pin yourself on a live world map. See where your people are scattered globally. Share moments. Celebrate together, even when continents apart.

---

## The Story

I built this in **2 hours** before my graduation party—because I was terrified of losing my class to distance, and also, it has been a quick 1-year program for me at Cornell, but I've grown attached to my cohort.

As a student from a multicultural background, I watched my community prepare to scatter across the world. I wanted one last thing: a way to see where everyone was, to celebrate together in real-time, and to hold onto those moments through shared photos. 

I didn't expect I would be this much into building this, and eventually commiting to it as much as I have. I just had so much fun, and peopl were interested in filling out this thing which motiviated me to build a prototype. This version [Map-It] is a more polished version that I spent on, 4-5 hours the few days after the party to enhance on this.

[Map-It] I hope can be a tool to serve students, alumni networks, conference attendees, and reunion organizers who refuse to let geography dissolve their communities.

I can't built this without the help of Replit, Claude, Google AI, Google Cloud, and also my friends around. 

Please bear with me with the vibe coding, as it is very messy. But I think the version work a bit great! 

---

## What This App Does

### Core Features ✅

- **Real-time World Map** — Drop a pin by clicking or searching your city. Watch live as your community populates the map across continents.
- **Guest Directory** — Browse all attendees, grouped by country. Search by name. One click to locate them on the map.
- **Live Sync** — Every pin, photo, and announcement appears instantly across all connected browsers via Firebase Realtime Database.
- **Country Filter** — Check/uncheck countries to focus the map. Track how many countries and guests are represented.
- **Ephemeral Photo Bubbles** — Post a photo tied to a location. It glows for 3 minutes, then fades. Perfect for capturing the moment without cluttering the map.
- **Photo Slideshow** — View all shared photos in a fullscreen carousel during the event.
- **Live Announcements** — Host sends messages that pop on all guest screens. Set them to repeat or one-time.
- **Projector Mode** — Fullscreen map with a scrolling ticker of all guests. Perfect for displaying on a big screen during an event.
- **Mobile Responsive** — Works flawlessly on phones and tablets with a bottom tab bar and slide-up panels.

### Secondary Features 🎁

- Spotlight cards with QR codes to guests' social handles
- Featured guest banners ("Just Joined!" notification)
- Celebration modals with confetti
- Photo archival to Google Drive (optional)
- Mobile-friendly country checklist
- Animated counter badge showing global reach

---

## Tech Stack

### Frontend
| Layer | Technology |
|-------|-----------|
| Map Engine | **Leaflet 1.9.4** — lightweight, open-source mapping library |
| Tile Layer | **CARTO Light** — clean, free basemap (no API key required) |
| Geocoding | **OpenStreetMap Nominatim** — free city-to-coordinates lookup |
| QR Codes | **QRCode.js 1.0.0** — client-side QR generation |
| Styling | **Vanilla CSS** — no framework, responsive design with CSS variables |
| JavaScript | **Vanilla ES Modules** — no build step, no bundler required |
| Firebase SDK | **v10.8.0** — Realtime Database only (minimal footprint) |

### Backend
| Layer | Technology |
|-------|-----------|
| Runtime | **Node.js ≥18** — plain `http` module (no Express) |
| Server | **server.js** — ~240 lines, two routes: `GET /` and `POST /api/archive-photo` |
| Config Injection | Firebase + host config injected into HTML at startup |
| Image Processing | **sharp 0.34.5** — converts photos to JPEG before Drive upload |

### Database & Real-time
| Layer | Technology |
|-------|-----------|
| Primary Database | **Firebase Realtime Database** — cloud-hosted JSON tree |
| Schema | `guests/`, `photos/`, `announcements/`, live sync via `onChildAdded`/`onChildRemoved` |
| External APIs | Google Drive API (optional photo archival), Google Sheets (optional logging) |

### Deployment
- **Hosting:** Replit (auto-scaling, zero-config)
- **Build:** No build step required — runs instantly on `node server.js`
- **Environment:** `nodejs-20` (NixOS stable channel)

---

## Why This Tech Stack?

**Speed Over Complexity** — Built in 2 hours with vanilla JS, no build tools, no frameworks. Launched immediately.

**Realtime Magic** — Firebase Realtime Database handles live sync effortlessly. When one guest pins themselves, everyone sees it in milliseconds.

**Accessibility** — Leaflet + CARTO means anyone with a browser can see the map. No app download needed.

**Affordability** — CARTO and Nominatim are free. Firebase has a generous free tier. This scales from a class reunion to a global conference without breaking the bank.

**Maintainability** — Vanilla JS means this runs on any server. No dependency hell. No framework version churn.

---

## Getting Started

### Prerequisites
- Node.js ≥18
- A Firebase Realtime Database project
- (Optional) Google Drive API credentials for photo archival

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/mindthemap.git
   cd mindthemap
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   
   Create a `.env` file in the root directory:
   ```env
   # Firebase Configuration
   FIREBASE_API_KEY=your_api_key
   FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
   FIREBASE_DATABASE_URL=https://your_project.firebaseio.com
   FIREBASE_PROJECT_ID=your_project_id
   FIREBASE_STORAGE_BUCKET=your_project.appspot.com
   FIREBASE_MESSAGING_SENDER_ID=your_sender_id
   FIREBASE_APP_ID=your_app_id

   # Host Configuration
   HOST_PASSWORD=your_secure_password

   # Optional: Google Drive Photo Archival
   GOOGLE_SERVICE_ACCOUNT_JSON={"type":"service_account",...}
   GOOGLE_DRIVE_FOLDER_ID=your_folder_id
   ```

4. **Start the server**
   ```bash
   npm start
   # Server runs on http://localhost:5000
   ```

5. **Open in your browser**
   ```
   http://localhost:5000
   ```

### Firebase Setup

1. Create a new Firebase Realtime Database
2. Set Security Rules to (for demo/development):
   ```json
   {
     "rules": {
       ".read": true,
       ".write": true
     }
   }
   ```
   ⚠️ **Security Note:** This is open access. For production, implement proper authentication.

3. Copy your config to the `.env` file above.

---

## Project Scope & Decision-Making

### What's Included
✅ Real-time map synchronization across all browsers  
✅ Guest directory with country filtering  
✅ Ephemeral photo bubbles with slideshow  
✅ Projector mode for event displays  
✅ Live announcements system  
✅ Mobile-responsive design  
✅ Host admin controls  

### What's Out of Scope (By Design)
❌ User authentication & accounts (intentionally guest-only for simplicity)  
❌ Permanent photo storage (by design—ephemeral, not archived)  
❌ Rate limiting / bot protection (assumes trusted event attendees)  
❌ Pin editing (delete & re-add only)  
❌ Event scheduling / recurring events  

### Design Decisions Explained

**Why Firebase?** — Realtime sync with zero backend complexity. Perfect for live events where latency kills the experience.

**Why Vanilla JS?** — Launched in 2 hours. A framework would've added overhead. Vanilla JS runs everywhere with zero build step.

**Why Ephemeral Photos?** — Photos disappear after 3 minutes. This encourages *presence* and *liveness* rather than endless documentation. It feels like a real party, not a permanent record.

**Why Leaflet + CARTO?** — Open-source, lightweight, and free. No API keys needed for the basemap.

**Why Server-side Image Processing?** — Sharp converts image data-URLs to JPEG before archiving to Drive. Saves bandwidth and storage.

---

## Known Limitations & Future Improvements

### Current Limitations
- **No user accounts** — Identity is based on localStorage. Refresh your browser = new guest entry (by design, for a 2-hour build).
- **Nominatim rate limits** — City search is rate-limited to 1 request/second. High-volume events might timeout.
- **Firebase rules are open** — Fine for demo/internal use. Production needs authentication.
- **Photos use base64 data-URLs** — Not optimal for large uploads, but works for the 3-minute ephemeral use case.

### Potential Enhancements
🔄 **Authentication** — User accounts + password reset for recurring communities (alumni networks, orgs)  
🛡️ **Rate Limiting** — Per-IP throttling on pin creation to prevent spam  
📝 **Pin Editing** — Allow users to update their location/bio without deleting  
🌐 **Internationalization** — Multi-language support for global events  
⚡ **Offline Support** — Service workers + local caching for unreliable connections  
🎨 **Event Customization** — Configurable branding, colors, and copy via a settings panel  

---

## Architecture & Code Highlights

### Project Structure
```
mindthemap/
├── server.js              # Node.js server, config injection, photo archiving
├── index.html             # Everything: HTML + CSS + JS (145 KB, single file)
├── package.json           # Dependencies: googleapis, sharp, express (minimal)
├── .env.example           # Configuration template
└── README.md              # This file
```

### Key JavaScript Modules (within index.html)
- **Map Initialization** — Leaflet map setup, CARTO basemap, click handlers
- **Firebase Sync** — Real-time listeners on guests, photos, announcements
- **Geocoding** — Nominatim API calls with debouncing
- **Photo Upload** — File input handling, base64 compression, Firebase writes
- **Projector Mode** — Fullscreen view with ticker + slideshow controls
- **UI State Management** — Directory filtering, tab switching, mobile sheet panel

### Notable Code Patterns
✨ **Debounced Geocoding** — Prevents hammering Nominatim with every keystroke  
✨ **Session-scoped Announcements** — Guests track seen announcements in `sessionStorage` (one-time vs. repeat logic)  
✨ **Ephemeral Photo Cleanup** — `setTimeout` deletes photos after 3 minutes  
✨ **Responsive Tabs** — CSS media queries swap from sidebar to bottom tabs at ≤767px  
✨ **Safe Password Comparison** — Though currently client-side (see security note below), uses timing-safe comparison patterns  

### Security Considerations ⚠️

**Current (Demo-Safe) Vulnerabilities:**
- Host password is injected into HTML source → visible to anyone who inspects
- Firebase rules are fully open (read/write)
- No input sanitization (though DOM-based, not HTML injection)

**For Production Deployment, Implement:**
1. Server-side password verification (don't inject raw password)
2. Firebase authentication + scoped security rules
3. Rate limiting on pin creation
4. HTTPS enforcement
5. CSP headers for security

See [SECURITY.md](./SECURITY.md) for detailed hardening guide.

---

## Performance & Scale

### Current Performance
- **Load Time** — ~2s on 4G (145 KB HTML, images lazy-loaded)
- **Map Responsiveness** — Pins render in <100ms across all browsers (Firebase magic)
- **Concurrent Users** — Tested up to 50+ live guests without degradation
- **Photo Bubbles** — Handle 10-20 uploads/min without issues (base64 + sharp processing)

### Scalability Limits
- **Nominatim** — Rate-limited to 1 req/sec (suitable for <100 attendees per minute)
- **Firebase** — Free tier allows ~100 simultaneous connections (scales on paid plan)
- **Photo Storage** — Firebase Realtime Database isn't ideal for high-volume binary data (currently using base64, which is inefficient)

### Optimization Opportunities
- Migrate photos to **Firebase Cloud Storage** instead of base64 in Realtime DB
- Add **Service Workers** for offline-first support
- Implement **image compression** on client before upload
- Cache Nominatim results in localStorage

---

## How to Run the Demo

1. Follow installation steps above
2. Visit `http://localhost:5000` in multiple browser windows
3. Pin yourself (click map or search city)
4. Watch pins appear live across windows
5. Toggle "Host" in the directory
6. Try projector mode (fullscreen icon)
7. Post a photo (upload tab)
8. Send an announcement (if logged in as host)

**Demo Workflow (~5 minutes):**
```
1. Open 3 browser windows side-by-side
2. In window 1: Pin yourself in New York
3. In window 2: Pin yourself in Tokyo
4. In window 3: Pin yourself in London
   → See all three appear in real-time on all windows
5. Host login (password: see .env)
6. Send announcement: "Welcome to the graduation party!"
7. Upload a photo from the photo tab
8. Click fullscreen (projector mode)
9. Watch the ticker scroll all guests + slideshow the photo
```

---

## Technical Skills Demonstrated

### Full-Stack Development
- **Frontend:** Vanilla JavaScript (ES Modules), Leaflet.js, responsive CSS, real-time UI updates
- **Backend:** Node.js, HTTP server routing, file I/O, integration with external APIs
- **Database:** Firebase Realtime Database, JSON schema design, real-time sync patterns
- **DevOps:** Environment configuration, secrets management, Replit deployment

### Problem-Solving Under Pressure
- Built a working MVP in 2 hours (constraint-driven design)
- Integrated 4 external APIs (Leaflet, CARTO, Nominatim, Firebase)
- Handled real-time synchronization across browsers
- Debugged on-the-fly at a live event

### Design & Product Thinking
- Prioritized user experience over feature completeness
- Made thoughtful tradeoffs (ephemeral photos vs. permanent records)
- Designed for accessibility (mobile-first, no framework overhead)
- Iterated based on feedback from real users at events

### Communication
- Documented code for future developers
- Created clear error states and user guidance
- Built features that work without explanation

---

## Lessons Learned

### What Worked Well
✅ **Vanilla JS + No Build Step** — Deploy anywhere, run instantly  
✅ **Firebase Realtime DB** — Magic for live experiences. Zero backend heavy-lifting.  
✅ **Constraint-Driven Design** — 2-hour limit forced ruthless prioritization  
✅ **Mobile-First Approach** — Most users joined via phone; design reflected that  

### What I'd Do Differently Next Time
📌 **Server-side password verification** — Don't inject secrets into client HTML  
📌 **Implement rate limiting** — Prevent spam and duplicate pins early  
📌 **Use Cloud Storage for photos** — Base64 in Realtime DB is inefficient at scale  
📌 **Add authentication system** — Especially for recurring communities (alumni networks)  

### Broader Insights
💡 **Fast shipping > perfect architecture** — Built in 2 hours and iterated with real feedback  
💡 **Real-time sync is a superpower** — Users don't understand how it works; they just *feel* connected  
💡 **Events are better than static** — The app shines during *live use* (parties, conferences)  

---

## Contributing

Found a bug? Have an idea? Contributions welcome!

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## License

This project is licensed under the MIT License — see [LICENSE](./LICENSE) file for details.

---

## Contact & Credits

**Built by:** [An (Andrew) Pham]  
**Inspired by:** Making the time spent with that one cohort memorable. Determination to make people feel connected.

**Get in touch:**
- 📧 Email: [andrewpham01.work@gmail.com]
- 🐙 GitHub: [@yourusername](https://github.com/AndoluFam)
- 💼 LinkedIn: [https://www.linkedin.com/in/andrewpham01/]
- 🌐 Portfolio: [theandrewpham.com] - still in works :D

**Special thanks to:**
- REPLIT for building out and hosting the platform.
- Netlify for quickly deploying the landing page
- Figma AI to help design the landing page
- Firebase for real-time magic
- Leaflet & CARTO for mapping simplicity
- Conrell Class of 2026 MPS Cohort for being scattered across the world (and inspiring this).

---

## Changelog

### v1.0 (Launch)
- Core mapping and guest directory
- Real-time sync via Firebase
- Ephemeral photo bubbles
- Projector mode
- Live announcements
- Mobile responsiveness

### v1.1 (Current)
- Photo slideshow
- Country filtering
- Animated counter badge
- Google Drive photo archival
- Celebration modals
- Enhanced mobile UX

---

**Remember:** Distance doesn't end community. It just changes how we show up. 🌍
