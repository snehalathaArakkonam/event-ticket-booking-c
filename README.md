
<div align="center">

```
 ███████╗██╗   ██╗███████╗███╗   ██╗████████╗    ███╗   ███╗ ██████╗ ██████╗ 
 ██╔════╝██║   ██║██╔════╝████╗  ██║╚══██╔══╝    ████╗ ████║██╔════╝ ██╔══██╗
 █████╗  ██║   ██║█████╗  ██╔██╗ ██║   ██║       ██╔████╔██║██║  ███╗██████╔╝
 ██╔══╝  ╚██╗ ██╔╝██╔══╝  ██║╚██╗██║   ██║       ██║╚██╔╝██║██║   ██║██╔══██╗
 ███████╗ ╚████╔╝ ███████╗██║ ╚████║   ██║       ██║ ╚═╝ ██║╚██████╔╝██║  ██║
 ╚══════╝  ╚═══╝  ╚══════╝╚═╝  ╚═══╝  ╚═╝       ╚═╝     ╚═╝ ╚═════╝ ╚═╝  ╚═╝
                                                                               
  ████████╗██╗ ██████╗██╗  ██╗███████╗████████╗    ██████╗  ██████╗  ██████╗ 
  ╚══██╔══╝██║██╔════╝██║ ██╔╝██╔════╝╚══██╔══╝    ██╔══██╗██╔═══██╗██╔════╝ 
     ██║   ██║██║     █████╔╝ █████╗     ██║       ██████╔╝██║   ██║██║      
     ██║   ██║██║     ██╔═██╗ ██╔══╝     ██║       ██╔══██╗██║   ██║██║      
     ██║   ██║╚██████╗██║  ██╗███████╗   ██║       ██████╔╝╚██████╔╝╚██████╗ 
     ╚═╝   ╚═╝ ╚═════╝╚═╝  ╚═╝╚══════╝   ╚═╝       ╚═════╝  ╚═════╝  ╚═════╝ 
```

### **Production-Grade Event & Ticket Booking Platform — Written in Pure C**

<br>

[![Language](https://img.shields.io/badge/Language-C%20%28C99%29-00599C?style=for-the-badge&logo=c&logoColor=white)](https://en.wikipedia.org/wiki/C_(programming_language))
[![Platform](https://img.shields.io/badge/Platform-Linux%20%7C%20Windows%20%7C%20macOS-lightgrey?style=for-the-badge&logo=linux&logoColor=white)](https://github.com/snehalathaArakkonam/event-ticket-booking-c)
[![License](https://img.shields.io/badge/License-MIT-22c55e?style=for-the-badge)](./LICENSE)
[![Build](https://img.shields.io/badge/Build-GCC%20%7C%20Makefile-f97316?style=for-the-badge&logo=gnu&logoColor=white)](./Makefile)
[![Status](https://img.shields.io/badge/Status-Production%20Ready-8b5cf6?style=for-the-badge)](https://github.com/snehalathaArakkonam/event-ticket-booking-c)
[![Modules](https://img.shields.io/badge/Modules-9%20Core%20Systems-ec4899?style=for-the-badge)](https://github.com/snehalathaArakkonam/event-ticket-booking-c)

<br>

> *A complete, modular console-based Event Management System implementing real-world booking logic, dynamic memory management via linked lists, binary file persistence, tiered refund policies, and revenue analytics — all in standard C.*

<br>

---

</div>

## 📋 Table of Contents

- [Overview](#-overview)
- [System Architecture](#-system-architecture)
- [Data Structures](#-data-structures)
- [Module Breakdown](#-module-breakdown)
- [Key Algorithms](#-key-algorithms)
- [File Structure](#-file-structure)
- [Build & Run](#-build--run)
- [Test Cases](#-test-cases)
- [Sample Output](#-sample-output)
- [Concepts Demonstrated](#-concepts-demonstrated)
- [Author](#-author)

---

## 🎯 Overview

The **Event Management System** is a comprehensive, console-based application engineered in pure C (C99 standard). It simulates a production-grade ticketing platform — from event creation and seat allocation to waitlist management, cancellation refunds, guest lists, digital certificates, and revenue analytics — all backed by binary file persistence.

This project was built to demonstrate **advanced C programming proficiency** relevant to systems-level internships and fresher AI/software engineering roles.

### What This System Handles

| Capability | Implementation |
|---|---|
| Dynamic event catalog | Singly linked list with heap allocation |
| Seat selection & booking | Grid-based seat map with `char` status flags |
| Waitlist auto-enrollment | Traversal-based promotion on cancellation |
| Tiered refund calculation | Time-delta policy (80% / 50% / 20% / 0%) |
| Revenue analytics | Per-event + aggregate float accumulation |
| Guest list management | Separate linked list with confirmation state |
| Digital certificate | Formatted console output with event binding |
| Data persistence | Binary `fwrite` / `fread` across 4 `.dat` files |
| Activity logging | Timestamped `fprintf` to `event.log` |

---

## 🏗 System Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                     EVENT MANAGEMENT SYSTEM                         │
│                          event.c (main)                             │
└───────────────────────────────┬─────────────────────────────────────┘
                                │
          ┌─────────────────────┼─────────────────────┐
          │                     │                     │
          ▼                     ▼                     ▼
  ┌───────────────┐    ┌────────────────┐    ┌────────────────┐
  │ event_module  │    │ ticket_module  │    │waitlist_module │
  │  addEvent()   │    │  bookTicket()  │    │addToWaitlist() │
  │displayEvents()│    │displaySeatMap()│    │enrollWaitlist()│
  │ searchEvent() │    │  selectSeats() │    └────────────────┘
  │ updateEvent() │    └────────────────┘
  │ deleteEvent() │
  └───────────────┘
          │                     │                     │
          ▼                     ▼                     ▼
  ┌───────────────┐    ┌────────────────┐    ┌────────────────┐
  │cancellation_  │    │revenue_module  │    │ guest_module   │
  │   module      │    │revenueReport() │    │  addGuest()    │
  │cancelTicket() │    │eventAnalytics()│    │confirmGuest()  │
  │calcRefund()   │    │topByRevenue()  │    │ guestReport()  │
  └───────────────┘    └────────────────┘    └────────────────┘
          │                     │                     │
          ▼                     ▼                     ▼
  ┌───────────────┐    ┌────────────────┐    ┌────────────────┐
  │certificate_   │    │ admin_module   │    │  File Layer    │
  │   module      │    │adminDashboard()│    │ events.dat     │
  │generateCert() │    │totalRevenue()  │    │ tickets.dat    │
  └───────────────┘    └────────────────┘    │ guests.dat     │
                                             │ venue.dat      │
                                             │ event.log      │
                                             └────────────────┘
```

---

## 🧱 Data Structures

### Event Node — Singly Linked List

```c
typedef struct Event {
    int    eventID;
    char   eventName[100];
    char   eventDescription[500];
    char   eventType[50];         /* Concert | Workshop | Conference | Party | Seminar */
    char   organizer[50];
    char   email[50];
    char   phone[15];
    int    venueID;
    char   venueName[100];
    char   venueAddress[200];
    int    totalCapacity;
    int    bookedSeats;
    int    availableSeats;
    int    waitlistCount;
    int    eventDate;
    int    eventTime;
    int    duration;
    float  ticketPrice;
    float  totalRevenue;
    char   status[20];            /* Scheduled | Ongoing | Completed | Cancelled */
    char   category[30];
    long   createdDate;
    struct Event* next;
} Event;
```

### Ticket Node — Singly Linked List

```c
typedef struct Ticket {
    int    ticketID;
    int    eventID;
    int    seatNumber;
    char   seatType[20];          /* Premium | Standard | Economy */
    char   customerName[50];
    char   customerEmail[50];
    char   customerPhone[15];
    float  ticketPrice;
    float  bookingFee;            /* 10% of ticket price */
    float  totalAmount;
    char   bookingStatus[20];     /* Confirmed | Waitlist | Cancelled */
    long   bookingDate;
    int    paymentStatus;
    struct Ticket* next;
} Ticket;
```

### Seat & Venue

```c
typedef struct Seat {
    int   seatNumber;
    char  seatType[20];
    float price;
    char  status;                 /* 'A' = Available | 'B' = Booked | 'W' = Waitlist */
    int   ticketID;
} Seat;

typedef struct Venue {
    int    venueID;
    char   venueName[100];
    char   venueAddress[200];
    int    totalSeats;
    int    premiumSeats;
    int    standardSeats;
    int    economySeats;
    Seat   seats[500];
} Venue;
```

### Guest Node

```c
typedef struct Guest {
    int    guestID;
    int    eventID;
    char   name[50];
    char   email[50];
    char   phone[15];
    char   company[50];
    char   designation[50];
    int    confirmed;
    long   inviteDate;
    long   responseDate;
    struct Guest* next;
} Guest;
```

---

## 📦 Module Breakdown

### Module 1 — Event Management (`event_module.c`)

Manages the full lifecycle of events using a **singly linked list** with `malloc` / `free`.

| Function | Description |
|---|---|
| `addEvent()` | Allocates a new `Event` node, assigns auto-incremented ID, prepends to list |
| `displayAllEvents()` | Traverses linked list and prints formatted event cards |
| `searchEvent()` | Linear search by event ID or name substring |
| `updateEvent()` | Locate node by ID, modify fields in-place |
| `deleteEvent()` | Splice node from list, call `free()`, update `count` |
| `eventByType()` | Filter traversal with `strcmp` on `eventType` |
| `eventByDate()` | Filter traversal comparing `eventDate` integer |
| `upcomingEvents()` | Compare `eventDate` against `time(NULL)` |
| `eventReport()` | Aggregate stats over full list pass |

---

### Module 2 — Ticket Booking with Seat Selection (`ticket_module.c`)

```
Booking Flow:
─────────────────────────────────────────────────────────
Select Event ID  →  Display Seat Map  →  Choose Seats
       │                                      │
       ▼                                      ▼
  Validate Event                     Validate each seat
  (exists + has                      (bounds check +
   available seats)                   status == 'A')
       │                                      │
       ▼                                      ▼
  Enter Customer Details         Mark seats status = 'B'
       │                                      │
       └──────────────┬───────────────────────┘
                      ▼
              Calculate Total
              price × n + 10% booking fee
                      │
                      ▼
              Update Event counters
              bookedSeats++  availableSeats--
              totalRevenue += totalAmount
                      │
                      ▼
              generateTicket() → print receipt
```

**Seat Map Display:**

```
    MAIN STAGE
    ==========

        0   1   2   3   4   5   6   7   8   9
  0     0   0   0   X   0   0   0   0   0   0
  1     0   X   0   0   0   0   X   0   0   0
  2     0   0   0   0   0   X   0   0   0   0
  ...

  0 = Available  |  X = Booked  |  W = Waitlist
  Premium: 100   |  Standard: 300  |  Economy: 100
```

---

### Module 3 — Waitlist Management (`waitlist_module.c`)

```c
/* Add to waitlist when event is full */
void addToWaitlist(EventList* events, TicketList* tickets, int eventID);

/* Promote first waitlist entry when a seat opens */
void enrollFromWaitlist(EventList* events, TicketList* tickets, int eventID);
```

On cancellation, `cancelTicket()` calls `enrollFromWaitlist()` automatically — the **first `Waitlist` ticket for that eventID** is promoted to `Confirmed`, maintaining FIFO order.

---

### Module 4 — Cancellation & Refund (`cancellation_module.c`)

#### Refund Policy Engine

```c
float calculateRefund(float amount, int daysBefore) {
    if      (daysBefore >= 7)  return amount * 0.80f;  /* 80% refund */
    else if (daysBefore >= 3)  return amount * 0.50f;  /* 50% refund */
    else if (daysBefore >= 1)  return amount * 0.20f;  /* 20% refund */
    else                       return 0.0f;             /* No refund  */
}
```

| Days Before Event | Refund % | Policy |
|---|---|---|
| ≥ 7 days | **80%** | Early cancellation |
| 3 – 6 days | **50%** | Mid-term cancellation |
| 1 – 2 days | **20%** | Late cancellation |
| < 1 day | **0%** | No refund |

On confirmed cancellation:
- Seat status reset to `'A'`
- `seat.ticketID = -1`
- `event.bookedSeats--`, `event.availableSeats++`
- `event.totalRevenue -= ticket.totalAmount`
- Waitlist auto-enrollment triggered

---

### Module 5 — Revenue Analytics (`revenue_module.c`)

```
Revenue Calculation per Event:
────────────────────────────────────────
  baseRevenue   =  ticketPrice × bookedSeats
  bookingFees   =  baseRevenue × 0.10
  totalRevenue  =  baseRevenue + bookingFees - refunds
────────────────────────────────────────

Platform Aggregates:
  totalRevenue     = Σ event.totalRevenue
  avgRevenueEvent  = totalRevenue / totalEvents
  occupancyRate    = (bookedSeats / totalCapacity) × 100
```

Functions:
- `revenueReport()` — Per-event revenue breakdown
- `eventAnalytics()` — Status counters + aggregate figures
- `topEventsByRevenue()` — Top 5 by descending `totalRevenue`

---

### Module 6 — Guest List Management (`guest_module.c`)

| Function | Description |
|---|---|
| `addGuest()` | Allocates `Guest` node, links to event by `eventID` |
| `displayGuests()` | Lists all guests with confirmation status |
| `searchGuest()` | Name-based substring search |
| `confirmGuest()` | Sets `confirmed = 1`, records `responseDate` |
| `guestReport()` | Confirmed vs pending statistics |
| `pendingResponses()` | Filter for `confirmed == 0` |

---

### Module 7 — Digital Certificate Generation (`certificate_module.c`)

```
╔══════════════════════════════════════════════════════════╗
║           CERTIFICATE OF PARTICIPATION                   ║
╠══════════════════════════════════════════════════════════╣
║                                                          ║
║   This is to certify that                               ║
║                                                          ║
║             Amit Sharma                                  ║
║                                                          ║
║   has successfully participated in                       ║
║                                                          ║
║             Music Concert 2026                           ║
║                                                          ║
║   Event Type  :  Concert                                 ║
║   Date        :  30/06/2026                              ║
║   Venue       :  Mumbai Stadium                          ║
║   Ticket ID   :  1                                       ║
║   Issued On   :  25/06/2026                              ║
║                                                          ║
╠══════════════════════════════════════════════════════════╣
║   Organizer   :  Rahul Events                            ║
╚══════════════════════════════════════════════════════════╝
```

---

### Module 8 — Admin Dashboard (`admin_module.c`)

```
╔══════════════════════════════════════════════════════╗
║            ADMIN DASHBOARD — LIVE STATS              ║
╠══════════════════════════════════════════════════════╣
║  Total Events       :    5                           ║
║  Total Bookings     :    2,500                       ║
║  Total Revenue      :    ₹12,50,000                  ║
║  Upcoming Events    :    3                           ║
║  Completed Events   :    1                           ║
║  Avg Booking/Event  :    500                         ║
╠══════════════════════════════════════════════════════╣
║  Events by Type                                      ║
║    Concert       ——  2                               ║
║    Workshop      ——  1                               ║
║    Conference    ——  1                               ║
║    Seminar       ——  1                               ║
╚══════════════════════════════════════════════════════╝
```

---

## ⚙️ Key Algorithms

### 1. Linked List Operations — O(1) Insert, O(n) Search

```
HEAD → [Event 3] → [Event 2] → [Event 1] → NULL
         ↑
    New events prepended at head (O(1))
    Search traverses O(n)
    Delete: prev->next = target->next, free(target)
```

### 2. Seat Grid Indexing

```c
/* 2D logical grid mapped to 1D array */
int seatIndex = row * 10 + col;
Seat* seat    = &venue.seats[seatIndex];

/* Status check before marking */
if (seat->status == 'A') {
    seat->status   = 'B';
    seat->ticketID = newTicket->ticketID;
}
```

### 3. Refund Calculation

```c
/* Time-based tiered refund */
int daysBefore  = (event->eventDate - currentDate);
float refund    = calculateRefund(ticket->totalAmount, daysBefore);
```

### 4. Revenue Aggregation

```c
float totalRevenue = 0.0f;
Event* curr = events->head;
while (curr != NULL) {
    totalRevenue += curr->totalRevenue;
    curr = curr->next;
}
float avgRevenue = totalRevenue / events->count;
```

---

## 📁 File Structure

```
event-ticket-booking-c/
│
├── 📄 event.c                  ← Main entry point (800+ lines)
├── 📄 event_module.c           ← Event CRUD + linked list ops
├── 📄 ticket_module.c          ← Booking, seat map, receipt
├── 📄 waitlist_module.c        ← Waitlist add + auto-enroll
├── 📄 cancellation_module.c    ← Cancel + refund calculation
├── 📄 revenue_module.c         ← Analytics + top events
├── 📄 guest_module.c           ← Guest list management
├── 📄 certificate_module.c     ← Certificate generation
├── 📄 admin_module.c           ← Dashboard statistics
│
├── 📦 events.dat               ← Binary: Event records
├── 📦 tickets.dat              ← Binary: Ticket records
├── 📦 guests.dat               ← Binary: Guest records
├── 📦 venue.dat                ← Binary: Venue + seat data
├── 📝 event.log                ← Text: Timestamped activity log
│
├── 🔧 Makefile                 ← Build automation
├── 📄 README.md                ← This file
└── 📄 LICENSE                  ← MIT License
```

### File I/O Strategy

```c
/* Binary write — Event record persistence */
FILE* fp = fopen(EVENTS_FILE, "wb");
if (fp == NULL) {
    fprintf(stderr, "[ERROR] Cannot open events.dat\n");
    return;
}

Event* curr = events->head;
while (curr != NULL) {
    fwrite(curr, sizeof(Event), 1, fp);
    curr = curr->next;
}
fclose(fp);

/* Binary read — Restore events on startup */
FILE* fp = fopen(EVENTS_FILE, "rb");
if (fp != NULL) {
    Event temp;
    while (fread(&temp, sizeof(Event), 1, fp) == 1) {
        Event* node = malloc(sizeof(Event));
        *node = temp;
        node->next = events->head;
        events->head = node;
        events->count++;
    }
    fclose(fp);
}
```

---

## 🔧 Build & Run

### Prerequisites

- GCC compiler (`gcc --version`)
- Make utility (`make --version`)
- Works on: Linux, macOS, Windows (MinGW / WSL)

### Compile & Run

```bash
# Clone the repository
git clone https://github.com/snehalathaArakkonam/event-ticket-booking-c.git
cd event-ticket-booking-c

# Build using Makefile
make

# Run the system
./event_system

# Or compile manually
gcc -std=c99 -Wall -Wextra \
    event.c event_module.c ticket_module.c waitlist_module.c \
    cancellation_module.c revenue_module.c guest_module.c \
    certificate_module.c admin_module.c \
    -o event_system -lm

./event_system
```

### Makefile

```makefile
CC     = gcc
CFLAGS = -std=c99 -Wall -Wextra
TARGET = event_system
SRCS   = event.c event_module.c ticket_module.c waitlist_module.c \
         cancellation_module.c revenue_module.c guest_module.c   \
         certificate_module.c admin_module.c

all: $(TARGET)

$(TARGET): $(SRCS)
	$(CC) $(CFLAGS) $(SRCS) -o $(TARGET) -lm

clean:
	rm -f $(TARGET) *.dat *.log

run: all
	./$(TARGET)
```

---

## 🧪 Test Cases

### TC-01 · Create Event

```
Input:
  Event Name    : Music Concert 2026
  Type          : Concert
  Organizer     : Rahul Events
  Venue         : Mumbai Stadium
  Capacity      : 1000
  Ticket Price  : ₹500
  Date          : 30/06/2026
  Time          : 18:00

Expected Output:
  ✅ Event created successfully!
  Event ID      : 1
  Name          : Music Concert 2026
  Capacity      : 1000
  Ticket Price  : ₹500.00
```

### TC-02 · Book Ticket (3 seats)

```
Input:
  Event ID      : 1
  Seats         : 5, 10, 15
  Customer      : Amit Sharma
  Email         : amit@email.com
  Phone         : 9876543210

Calculation:
  Base Price    : ₹500 × 3 = ₹1,500
  Booking Fee   : ₹1,500 × 10% = ₹150
  Total         : ₹1,650

Expected Output:
  ✅ Ticket booked successfully!
  Ticket ID     : 1
  Seats Booked  : 3
  Total Amount  : ₹1,650.00
```

### TC-03 · Add to Waitlist

```
Precondition  : Music Concert 2026 — FULL (0 available seats)

Input:
  Event ID      : 1
  Customer      : Priya Singh
  Email         : priya@email.com

Expected Output:
  ✅ Added to waitlist!
  Ticket ID          : 2
  Waitlist Position  : 1
```

### TC-04 · Cancel Ticket + Auto Enroll from Waitlist

```
Input:
  Ticket ID     : 1 (Amit Sharma)

Days before event : 10

Refund Calculation:
  Total Paid    : ₹1,650
  Policy        : 10 days ≥ 7 → 80% refund
  Refund Amount : ₹1,320

Expected Output:
  ✅ Ticket cancelled!
  Refund Amount      : ₹1,320.00
  ✅ Waitlist auto-enrolled: Priya Singh → Confirmed
```

### TC-05 · Revenue Report

```
Expected Output:
  ════════════════════════════════════════
      REVENUE ANALYTICS
  ════════════════════════════════════════

  Event : Music Concert 2026
    Booked Seats  : 950
    Ticket Price  : ₹500.00
    Revenue       : ₹4,75,000.00

  ════════════════════════════════════════
  TOTAL REVENUE   : ₹4,75,000.00
  ════════════════════════════════════════
```

### TC-06 · Event Analytics

```
Expected Output:
  Total Events         : 5
  Scheduled            : 3
  Ongoing              : 1
  Completed            : 1
  Total Bookings       : 2,500
  Total Revenue        : ₹12,50,000.00
  Avg Revenue/Event    : ₹2,50,000.00
```

---

## 💡 Sample Output

### Main Menu

```
════════════════════════════════════════════════
          EVENT MANAGEMENT SYSTEM
       Ticket Booking & Analytics v1.0
════════════════════════════════════════════════
  1.  Event Management
  2.  Ticket Booking
  3.  Waitlist Management
  4.  Ticket Cancellation
  5.  Revenue Analytics
  6.  Guest List
  7.  Certificate Generation
  8.  Admin Dashboard
  9.  Exit
════════════════════════════════════════════════
Enter choice:
```

### Seat Map

```
════════════════════════════════════════════════
    VENUE: Mumbai Stadium
════════════════════════════════════════════════

    MAIN STAGE
    ==========

      0   1   2   3   4   5   6   7   8   9
  0   0   0   0   X   0   0   0   0   0   0
  1   0   X   0   0   0   0   X   0   0   0
  2   0   0   0   0   0   X   0   0   0   0
  3   0   0   W   0   0   0   0   0   X   0

  0 = Available  |  X = Booked  |  W = Waitlist
  Premium: 100   |  Standard: 300   |  Economy: 100
════════════════════════════════════════════════
```

---

## 🎓 Concepts Demonstrated

| Concept | Where Applied |
|---|---|
| **Singly Linked List** | `EventList`, `TicketList`, `GuestList` — dynamic node allocation/deletion |
| **Dynamic Memory** | `malloc()` on every node insert, `free()` on delete |
| **File Handling** | `fwrite` / `fread` binary I/O, `fprintf` activity logging |
| **Structs & Typedef** | `Event`, `Ticket`, `Guest`, `Seat`, `Venue` composites |
| **Sorting (Bubble Sort)** | Top-5 events sorted by `totalRevenue` descending |
| **Mathematical Algorithms** | Refund tiers (%), revenue aggregation, occupancy rate |
| **Input Validation** | Bounds check on seat numbers, NULL checks on all pointers |
| **Pointer Arithmetic** | Seat grid indexing via `row * 10 + col` |
| **Modular Programming** | 9 separate translation units with single-responsibility design |
| **Error Handling** | File open failures, NULL event/ticket lookups, invalid choices |
| **Time Functions** | `time(NULL)` for `bookingDate`, `createdDate`, log timestamps |

---

## 👩‍💻 Author

<div align="center">

**Snehalatha Arakkonam**

B.Tech Computer Science Engineering · AI & ML Specialization

[![GitHub](https://img.shields.io/badge/GitHub-snehalathaArakkonam-181717?style=for-the-badge&logo=github)](https://github.com/snehalathaArakkonam)

*Built as part of a production-quality C systems programming portfolio.*
*Demonstrates linked list design, file persistence, modular architecture, and real-world booking logic in pure C.*

</div>

---

<div align="center">

**⭐ Star this repo if it helped you understand systems programming in C**

```
  Made with ❤️ in C  |  No databases. No GUIs. No shortcuts.
```

</div>
