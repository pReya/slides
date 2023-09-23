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
- Use a custom room type – not visible in regular clients (separate apps for separate things)
- Calendar Events map nicely on to messages
- Users are users

---

### Let's not reinvent the wheel

- 🛳️ Replace CalDAV with Matrix for sync/federation <!-- .element: class="fragment" -->
- 📦 Replace iCal with JSCalendar for sanity <!-- .element: class="fragment" -->

Note:
- Use matrix for transport instead of CalDAV
- Let's not invent a new calender event format: JSCalendar (unfortunate naming)
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
- Custom event type (which could also be sent into regular rooms like original MSC)
- Light wrapper around JSCalendar events

---

### Building a Matrix calendar client
Matrix client boilerplate  
*(e.g. Hydrogen or Element)*  
➕ <br/>
Calendar UI library  
*(e.g. FullCalendar)*

Note:
- Now how do we use this message format? We need a client
- Existing clients don't speak matrix -> Need to build a new client
- Again: Don't reinvent the wheel: Use FullCalendar

---

### Challenges for building a Matrix Calendar Client

- 🧮 Efficiently transform stream of events into state
- 🥷 Handle conflicts (e.g. Editing at the same time)
- 💅 Make it nice (UI/UX)

Note:
- Stream of calendar events needs to be transformed into a consistent, queryable "UI state"
- Performance problems, when calendars become large (maybe send intermittent full state as message or file attachment)
- Prevent/avoid conflicts between users

---

### Bridging Matrix to CalDav

- 🤬 Don't force people to use a new tool <!-- .element: class="fragment" -->
- 🔮 Eventually calendar apps could integrate Matrix themselves <!-- .element: class="fragment" -->
- 🌉 Until then: bridging allows compatibility with existing calendar clients <!-- .element: class="fragment" -->


Note:
- Must have becaus of native system calendar apps most people use

---

### Bridge Details

- Optional Bot bridge usable through Calendar client
- Bot user is invited to bridged calendars
- CalDAV username is Matrix ID, Password will be generated by Bot (No Matrix credentials given to bot)
- Possibly: Allow to send invites to Matrix IDs

Note: 
- CalDav server use Matrix id as username, but own passwords
- Bridge bot user will automatically be added to matrix room

---

### There's an MSC for that?!

- Timeline aggregation logic can't be moved to the server due to encryption
- No server changes necessary, everything is client-side logic
- Maybe message event format could be defined in the standard


Note: 

---

### 💸 We're looking for funding 💸
Please give us your money
<br/><br/>

### Feedback / Discussion / Follow
*#matrixcalendar:bitbetter.de*

Note: 
- Gib money
- Join room
