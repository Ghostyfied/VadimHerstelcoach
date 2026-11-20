# Herstelcoach – Product definition (V1)

Status: draft, based on the concept file `Herstelcoach-concept-v0.2.html` and the
answers Vadim gave to the product questions. This document records **what** the
product is and **what is in and out of V1**. Technical and design decisions come
later, in separate documents.

Last updated: 2026-11-20

---

## 1. What we are building

A coaching application for a small team of practitioners (physio, strength
trainer, technique analyst) and their athlete clients. Clients buy a guidance
trajectory with a custom duration. The team builds the training plan, the client
trains and logs, the team follows up, adjusts and communicates, all inside one
application that works on phone and on PC.

- **Owner**: Vadim's team. Scope and priorities are decided by the team.
- **V1 users**: one organisation, at most 3 practitioners, about 10 clients.
- **Long term**: sell the product to other practices. V1 is therefore built
  around an *organisation* as the unit of isolation from day one, even though
  only one organisation exists at launch.
- **Languages**: Dutch and English, both required in V1.
- The name "Fysiofabriek" from the concept is dropped. Brand colours are placeholders.

## 2. Product goals

1. Keep athletes training between sessions with a clear plan and frictionless logging.
2. Give practitioners a triage overview of all clients: what is new, who needs attention, mark as handled.
3. Close the feedback loop fast: client logs or films, practitioner reviews, adjusts the schema, client sees the change at once.
4. Make progress visible to both sides: per exercise and toward a phased main goal.
5. One safe, structured channel for chat, session reports and internal team notes (no WhatsApp).
6. Work as a team: shared exercise library inside the organisation, several practitioners per client.
7. Handle the business side: intake questionnaire before sign-up, trajectories with packages or custom pricing.

## 3. Decision log

Questions asked before planning, with the answers and what they mean for scope.

| # | Topic | Answer | Implication |
|---|-------|--------|-------------|
| 1 | Who is it for | Own team only for now (max 3 practitioners); later other practices | Organisation model from the start; single tenant at launch |
| 2 | Who decides | The team | No external stakeholder sign-off |
| 3 | Ownership | Own product | Own branding, no partner constraints |
| 4 | Scale | 3 practitioners, 10 clients | Small scale; no scaling work needed in V1 |
| 5 | Trajectory duration | Custom | Trajectory = start date + end date (or weeks), not fixed packages only |
| 6 | Billing | In the app: pre-arranged packages and custom ones with custom pricing | New feature versus the concept; see open question A |
| 7 | Onboarding | Always an intake; a questionnaire before sign-up | New feature: intake questionnaire flow precedes account creation |
| 8 | Client types | V1: athletes who want to get better or stronger. Team: technique analyst, strength trainer, physio | "Fysio" becomes "practitioner" with a role label; rehab-specific wording is secondary |
| 9 | Practitioner usage | Throughout the day | In-app inbox and badges are central |
| 10 | Attention triggers | Defaults are fine: no log for X days, more pain reported | Keep as in concept; more triggers later |
| 11 | Client freedom | None in V1 | Client cannot plan extra trainings, swap exercises, change weights or book appointments |
| 12 | Logging | Every field optional except "done"; "done" logs the prescribed defaults | One-tap training completion; detailed fields are optional |
| 13 | Execution video | Optional upload field, not required | Keep video upload, keep it optional |
| 14 | Goals authoring | Practitioner input plus templates | Goal and phase templates are a feature |
| 15 | Sub-goal completion | Practitioner confirms each one | The app may *propose* a sub-goal as reached from logs; nothing ticks automatically |
| 16 | Client visibility | Never other clients' data; otherwise everything except internal notes | Internal notes and internal reports hidden from client; all else visible |
| 17 | Chat | Yes; clients can always message; no response-time promises | Chat stays; consultation hours and auto-reply are not needed (see open question C) |
| 18 | Chat after trajectory | Allowed | Chat access is not tied to trajectory status |
| 19 | Push notifications | Not in V1 | In-app notifications only; see open question B for reminders |
| 20 | Several practitioners per client | Sometimes; organisations as the sharding unit | Treatment team per client within an organisation |
| 21 | Colleague visibility | Only shared clients | A practitioner sees a client only when in that client's treatment team |
| 22 | Library visibility | All libraries within the organisation | Organisation-wide library; personal "mine" view is a filter |
| 23 | Practice-system integration | Not relevant | Out of scope |
| 24 | Client self-booking | No | Out of scope; see open question D for the agenda |
| 25 | Existing videos | None | Library starts empty; exercises without video are the normal case |
| 26 | Languages | Dutch and English | Interface and content in both languages |
| 27 | Medical data | Later | Deferred |
| 28 | Retention and deletion | Later | Deferred; design so it can be added |
| 29 | Professional obligations | None | No regulatory record-keeping requirements in V1 |
| 30 | Success criteria | Works smoothly, no odd user paths, no major bugs, several feedback rounds done, no foreseeable resource problems | Quality and stability over feature count |
| 31 | First users | Internal clients | Pilot with internal clients |
| 32 | Drop or missing | N/A | – |

## 4. V1 scope

### In scope

**Organisation and accounts**
- Organisation with practitioners (role label: physio, strength trainer, technique analyst) and clients.
- Intake questionnaire that a prospective client fills in before an account is created.
- Trajectories per client with a custom duration and a package or custom price.
- Billing configuration: pre-arranged packages and custom pricing.

**Practitioner side**
- Client list with filters: all, open items, needs attention; badges that stay until marked handled.
- Client overview: signals (inactive, more pain), activity feed, session reports (to client or internal).
- Schema editor: training days, blocks, exercises, sets, reps or seconds, weight. Changes are visible to the client at once.
- Goals: main goal, phases, sub-goals; templates plus manual input; the app proposes, the practitioner confirms.
- Progress per exercise with effort and pain; chart and table view.
- Review of client execution videos with written feedback.
- Chat per client with quick replies and an inactivity reminder message.
- Treatment team per client; internal notes and internal reports hidden from the client.
- Exercise library: organisation-wide, with "mine", favourites, copy-and-adapt, optional video, both languages.
- Settings: inactivity threshold.

**Client side**
- Today screen: today's training in at most two taps.
- Training flow: instructions and optional video; "done" with defaults, optional sets, effort, pain, note and video upload.
- Agenda view of planned training days and appointments set by the practitioner (read only).
- Chat with the treatment team.
- Progress per exercise and toward the current phase; trajectory status (week x of y).
- Readable session reports; language choice.

### Out of scope for V1
- Client self-planning of extra trainings, swapping exercises, changing weights.
- Client self-booking of appointments.
- Practice-system integration.
- Push notifications.
- Consultation hours with auto-reply (to confirm, see C).
- Multi-organisation administration and selling to other practices.
- Data retention and deletion policies (to be defined later).
- Rehab-specific goal wording and templates.

## 5. Open questions from the answers

These came out of the answers and need a decision before the implementation plan is final.

- **A. Billing depth.** Does "billing in the app" mean recording what a client owes and has paid, or also collecting payment online? If online, which provider (?) and are recurring charges needed?
- **B. Reminders without push.** Client reminders on training days (concept US-27/28) assumed push notifications. Without push: drop reminders for V1, or send email (?)
- **C. Consultation hours.** With "no promises on response times", should the practitioner's online hours and the auto-reply be dropped entirely, or kept as information only?
- **D. Agenda.** With no practice system and no client booking, is an agenda still needed? Proposal: a simple list of appointments created by the practitioner that the client sees in their agenda.
- **E. Intake questionnaire.** Who defines the questions, is one fixed questionnaire enough for V1, and does the team review it before creating the account?
- **F. English content.** Interface in both languages is clear. Do exercise instructions and goal templates also need both languages from day one, or Dutch first?
- **G. Practitioner roles.** Do the three roles need different permissions, or is the role only a label?
- **H. Trajectory end.** What does the client see after the trajectory ends: read-only history, a renewal prompt, nothing?

## 6. Next steps

1. Decide the open questions A to H.
2. Write the implementation plan: platform choice, architecture, data model, milestones.
3. Define the pilot with internal clients and the feedback rounds.
