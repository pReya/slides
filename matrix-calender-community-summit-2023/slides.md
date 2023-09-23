---
title: "Calendars over Matrix"
---

# Calendars over Matrix <br/> 🗓️

> Matrix Community Summit</br>
> Berlin – 23.9.2023

Note:
- Photos are okay
- This is a suggestion – we didn't build anything yet
- Want your feedback. Right now or later.

---

### We? Who?
<div style="display: flex; width: 100%; margin-bottom: 40px; font-size: 2.5rem;">
  <div style="flex: 1; display: flex; flex-direction: column; align-items: center;">
    <img style="border-radius: 9999px; width: 200px; display: block;" src="images/fabi.png" />
    <strong>Fabian</strong><br/>
    <span style="font-size: 2rem; font-weight: 200;">Fullstack Developer<br/>@fabian:bitbetter.de</span>
  </div>
  <div style="flex: 1; display: flex; flex-direction: column; align-items: center;">
    <img style="border-radius: 9999px; width: 200px; display: block;" src="images/moritz.jpg" />
    <strong>Moritz</strong><br/>
    <span style="font-size: 2rem; font-weight: 200;">Fullstack Developer<br/>
    @moritz:bitbetter.de</span>
  </div>
</div>

- 📚 Met 2014 at university in Hamburg
- 💼 Started a company together: [bitbetter GmbH](https://bitbetter.de/)

Note:

---

### 🏛️ Prior Work

- [Old MSC](https://github.com/matrix-org/matrix-spec-proposals/pull/1116) for "Calendar events in rooms"

Note:
- Different use case: Mostly about displaying individual upcoming events in a room
- Not for whole calendars, no big overlap

---

### 🏋️ Motivation
# Shared calendars suck!
*Partially due to:*  
CalDAV for transport/sync  
iCal as content representation

Note:
- Not talking about calendar invites
- Because users all need an account on the same server or SaaS product
- Sharing within your company/Exchange, within Google, within your Nextcloud is fine
- Matrix could solve this problem and give us:
  - Federation
  - Encryption
  - User management
  - Hosting calendars on homeservers

---

### We want to do 3 things

1. 💬 Define a message format for calendar events in Matrix <!-- .element: class="fragment" -->
2. 📲 Build a Matrix calendar client as MVP <!-- .element: class="fragment" -->
3. 🌉 Build a Matrix <-> CalDAV bridge for existing calendar apps <!-- .element: class="fragment" -->

Note:


---

#### Mapping calendars onto the Matrix protocol

<table>
  <thead>
    <tr>
      <th>Calendar</th>
      <th>Matrix</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Calendar</td>
      <td>Room</td>
    </tr>
    <tr>
      <td>Event</td>
      <td>Message</td>
    </tr>
    <tr>
      <td>User</td>
      <td>User</td>
    </tr>
  </tbody>
</table>

Note:
- Calendar maps nicely onto a room (arbitrary amount of people can join, user privileges)
- Events map nicely to messages
- Users are users

---

### Let's not reinvent the wheel

- Replace CalDAV with Matrix for federation <!-- .element: class="fragment" -->
- Replace iCal with JSCalendar for sanity <!-- .element: class="fragment" -->

Note:
- Unfortunate naming: Will mostly find JS calendar libs
- JSCalendar is a better replacement for iCal (JSON based, fixes some stuff that makes iCal ugly)
- JSCalendar is a Proposed IETF standard(RFC 8984)
- Invented by Fastmail, to be used in JMAP

---

### Example Matrix event
```json
{
  "type": "m.calendar.event",
  // Payload is standard JSCalender event
  "content": {
    "@type"   : "Event",
    "uid"     : "a8df6573-0474-496d-8496-033ad45d7fea",
    "updated" : "2023-09-22T18:23:04Z",
    "title"   : "Matrix Community Summit Talk",
    "start"   : "2023-09-23T17:00:00",
    "timeZone": "Europe/Berlin",
    "duration": "PT1H"
  }
  // Possibly some custom fields for efficient aggregation
}
```

Note:


---

### Moral dilemma
- Why not reverse engineer the client? <!-- .element: class="fragment" -->
  - We ❤️ Threema and Open Source
  - Making money with OSS is hard
  - <span style="text-decoration:underline">Our</span> bridge uses <span style="text-decoration:underline">their</span> infrastructure
  - Bridge allows automation -> possibly heavier usage than App
- "Client mode": We rip them off <!-- .element: class="fragment" -->
- "Gateway mode": They rip us off <!-- .element: class="fragment" -->

---

### How do we solve it?
- Talked to 👨🏻‍💼 Threema CEO about it <!-- .element: class="fragment" -->
  - Understood our problem 👊
  - Don't hate our project 🥳
  - Gave us credits for testing 🙏
- They will think about solutions <!-- .element: class="fragment" -->
  - <span style="text-decoration:underline">Maybe</span> change their pricing model
- No promises though – nothing might happen <!-- .element: class="fragment" -->
<div class="fragment" style="font-weight: 700; display: flex; justify-content: center;">=> How do we proceed?</div>

Note:
- Discussion/input afterwards appreciated
- Would like to find middle ground
- Plan for the future:
  - Gateway API for now
  - Wait for a) Threema b) Matrix SDK Maturity
  - Implement "client" solution later

---

### Implementation Phase
- Multiple SDKs/Languages on both sides of the bridge
- Official Threema Gateway SDKs not very active, but functioning
- 🦀 Rust seemed to be the most future-proof choice

Note:
- Exploration/Evaluation of SDKs took a long time
- Problem: We've never written any Rust -> started to learn

---
### Problems #1

![](images/support.png)<!-- .element height="500px" -->


---

### Problems #1
- 🤡 Threema Gateway product does not support group chats
  - But it actually does – it's just not documented
  - We implemented group logic ourselves (planning to upstream to `threema-gateway-rs`)

Note:
- Asked Threema support for Group chats -> Nope
- Threema employee gave us a hint
- Receive a message for group meta data
- Group text messages are just single messages

---

### Problems #2
- `matrix-rust-sdk` is still missing some features/buggy
  - Application Services Crate
    - E2EE is not stable
    - Can't set display names for virtual users
    - Initial state / sync is not supported, yet
    - For now: We're pausing App Service functionality

Note:
- Currently it's a bridge bot
- Would like to convert it to App Service and use Puppeteering

---

### Thanks!
- Follow us:
  - Matrix: [#threema-bridge:matrix.org](https://matrix.to/#/#threema-bridge:matrix.org)
  - GitHub: [github.com/bitbetterde/Threematrix](https://github.com/bitbetterde/Threematrix)
  - Mastodon: [@threematrix@mastodon.social](https://mastodon.social/@threematrix)


Note:
