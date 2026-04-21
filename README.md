# ✅ Bus Ticket Booking System — Pre-Viva Checklist

> **📋 How to use this file:** Print this, or keep it open on your phone. Start working through it **the day before** your viva. Check off each item — if any fails, fix it before the viva starts.

> **Total time estimate:** 2 hours the night before + 30 minutes morning of.

---

# 🌙 The Night Before

## 🔧 Technical Sanity Checks

- [ ] **Backend builds clean** — `cd backend && ./mvnw.cmd clean package -DskipTests` → `BUILD SUCCESS`
- [ ] **Frontend builds clean** — `cd frontend && ./mvnw.cmd clean package -DskipTests` → `BUILD SUCCESS`
- [ ] **All 314 tests pass** — `./mvnw.cmd test` → `Tests run: 314, Failures: 0`
- [ ] **MySQL is running** — Windows Services → `MySQL80` → status: Running
- [ ] **Database has seed data** — `SELECT COUNT(*) FROM trip;` returns > 0
- [ ] **Backend runs** — `./mvnw.cmd spring-boot:run` → `Started BusTicketBookingSystemApplication`
- [ ] **Frontend runs** — `./mvnw.cmd spring-boot:run` → `Started BusFrontendApplication` on 8081
- [ ] **Login works** — http://localhost:8081 → login with `admin` / `admin1234` → lands on home
- [ ] **End-to-end booking flow works** — book 2 seats → pay → download PDF (try this flow at least twice)
- [ ] **SonarQube runs** — `cd <sonarqube>/bin/windows-x86-64 && StartSonar.bat` → http://localhost:9000 loads
- [ ] **SonarQube dashboard is green** — Quality Gate: Passed

## 🗂️ File Organization

- [ ] **Desktop folder is tidy** — all `Bus-Ticket-*.md` files in one place
- [ ] **Screenshots captured** (10 total):
  - [ ] Homepage
  - [ ] Trip list
  - [ ] Seat selection grid
  - [ ] Payment checkout
  - [ ] Success + PDF ticket
  - [ ] Member Explorer
  - [ ] Team page
  - [ ] SonarQube dashboard (green gate)
  - [ ] Terminal showing `Tests run: 314, Failures: 0`
  - [ ] IntelliJ class diagram (one module)
- [ ] **Screenshots are in a folder** — `C:\Users\Sarthak\OneDrive\Desktop\viva-screenshots\`

## 🎤 Presentation Prep

- [ ] **Slides built** — 20 slides in PowerPoint / Gamma / Google Slides
- [ ] **Slides practiced at least 2x out loud** — aim for 10 minutes total
- [ ] **Elevator pitch memorized** (the 30-second version from presentation content file)
- [ ] **Opening line memorized** — "Good morning, today I'll walk you through..."
- [ ] **Closing line memorized** — "Thank you, happy to take questions"
- [ ] **Postman collection imported** from `Bus-Ticket-API.postman_collection.json`
- [ ] **Postman: tested that `GET /api/trips` returns 200**

## 🧠 Concept Refresh

Read these sections once each:
- [ ] `final-sonarqube.md` — Section 3 (the 6 rounds)
- [ ] `Bus-Ticket-Security-Fixes-Guide.md` — what Round 4 did and why
- [ ] `Bus-Ticket-Class-Diagrams.md` — the two sequence diagrams (booking flow, security flow)

## ❓ Pre-Prepared Q&A Run-Through

Say the answer out loud for each:
- [ ] "What's the difference between your frontend and backend?"
- [ ] "Why did you use HTTP Basic and not JWT?"
- [ ] "How do you prevent two users booking the same seat?"
- [ ] "What's cognitive complexity and how did you reduce it?"
- [ ] "Why did you mark that CSRF hotspot as Safe?"
- [ ] "Show me your most complex method and explain it."
- [ ] "Why two `SecurityFilterChain` beans?"
- [ ] "What does `@AutoConfigureMockMvc(addFilters = false)` do?"
- [ ] "How would you make this production-ready?"
- [ ] "What did you learn doing this project?"

---

# ☀️ Morning Of — 30 Minutes Before Viva

## 💻 Laptop Setup

- [ ] **Laptop plugged in** (don't trust battery)
- [ ] **HDMI/projector cable tested** (if presenting on projector)
- [ ] **Close all unnecessary apps** — only keep what you need open
- [ ] **Disable notifications** — Windows Focus Assist → On
- [ ] **Silence phone** — airplane mode or silent
- [ ] **Browser tabs set up** (in this order):
  1. http://localhost:8081 (frontend)
  2. http://localhost:8080/swagger-ui.html (if configured)
  3. http://localhost:9000 (SonarQube — logged in)
  4. Your GitHub repos (backend + frontend READMEs visible)
- [ ] **Terminal 1:** backend running
- [ ] **Terminal 2:** frontend running
- [ ] **IntelliJ open** with backend project loaded
- [ ] **Postman open** with collection ready
- [ ] **PowerPoint/Gamma deck open** in presentation mode (press F5 to test)
- [ ] **File Explorer open** at `C:\Users\Sarthak\OneDrive\Desktop\` (all your .md files visible)

## 🔄 Run a Sanity Check (5 min)

- [ ] Open http://localhost:8081 → login → book a seat → pay → download PDF (full cycle)
- [ ] If the full cycle works **in order**, you're ready
- [ ] If anything fails, **don't panic** — jump to Recovery Plan in `Bus-Ticket-Demo-Walkthrough.md`

## 🎯 Mental Prep

- [ ] Deep breath. You built this. You know it better than anyone in the room.
- [ ] Remember: **examiners want you to pass**. They're on your side.
- [ ] If you don't know an answer → say "I'm not 100% sure, but my best guess is X" → they respect honesty more than bluffing

---

# 🎬 During the Viva

## Opening (first 30 seconds)

1. Stand confident. Don't fidget.
2. Greet: "Good morning, sir/ma'am."
3. Start with the elevator pitch (30 sec).
4. "I'll walk you through the project in about 10 minutes, then demo it, then take questions."

## Presenting

- ✅ **Look at examiners, not slides** (glance at slides briefly)
- ✅ **Speak at medium pace** — don't rush
- ✅ **Use hand gestures** when explaining architecture
- ✅ **Point to specific things on screen** ("This arrow represents...")
- ❌ Don't read bullets verbatim
- ❌ Don't say "um", "like", "so basically" too often
- ❌ Don't apologize ("sorry, I didn't prepare this well") — ever

## If You Get Stuck

- **On a code question:** open the file in IntelliJ → read it silently for 3 seconds → then explain
- **On a concept:** "Let me think for a second" → pause → answer
- **On something you don't know:** "That's a great question. I believe it's X, but I'd want to verify in the code — can I show you after?"

## During Demo

- Follow `Bus-Ticket-Demo-Walkthrough.md` top to bottom
- If something breaks → **jump to Recovery Plan** in that file
- Worst case: show pre-recorded screenshots/video — "Let me show you what it looks like in action"

---

# 🏁 After the Viva

- [ ] **Thank the examiners** ("Thank you for your time")
- [ ] **Note any questions you struggled with** → add to your knowledge base
- [ ] **Stop the apps** — Ctrl+C in terminals (so they don't leak resources)
- [ ] **Push your latest code** to GitHub (final commit)
- [ ] **Backup the database** — `mysqldump -u root -p busticketbooking > backup.sql`
- [ ] **Save all artifacts** — PPTs, PDFs, screenshots → one ZIP for portfolio

---

# 🆘 Emergency Contacts / Resources

**If your laptop fails mid-viva:**
- GitHub URLs (bookmarked in your phone):
  - `https://github.com/sarthakpawar0912/bus-ticket-booking-system`
  - `https://github.com/sarthakpawar0912/bus-ticket-frontend`
- Examiner can see the code on their laptop via GitHub

**If you blank on a concept:**
- Mentally reference: "what did I write in the SonarQube guide for that?"
- Most concepts are covered in `final-sonarqube.md` viva questions (Q1-Q270)

---

# 🎖️ Final Reminder

You built a **full-stack distributed Spring Boot system** with:
- 9,300 lines of code
- 89 Java files
- 47 Thymeleaf templates
- 314 passing tests
- SonarQube Quality Gate passed
- 6 rounds of code quality iteration
- Round 4 security hardening
- Proper architecture, design patterns, and testing

**You know this project inside out. The examiner does not.** You have the home advantage.

**Go crush it. 🚀**
