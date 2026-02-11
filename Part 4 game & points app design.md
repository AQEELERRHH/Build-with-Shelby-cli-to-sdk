# Part 4: Building a Game & Points App with Shelby

## Overview

In this part of the Shelby learning series, we build a **simple game-like application** where users earn **points, levels, and leaderboard rankings** based on file uploads and downloads powered by Shelby.

Instead of treating files as passive data, this project demonstrates how **file actions themselves can become gameplay mechanics**.

This part builds directly on:

* **Part 1:** Shelby CLI basics
* **Part 2:** Shelby SDK basics (Node.js)
* **Part 3:** Simple app for uploading and downloading files

---

## What This Part Demonstrates

By the end of this part, you will understand how to:

* Use Shelby as a **core file layer** for interactive applications
* Turn uploads and downloads into **user actions**
* Track user progress using points and levels
* Build a simple **leaderboard system**
* Design game logic *around* Shelby without modifying Shelby itself

This is a learning-focused demo not a production game.

---

## Why a Game Makes Sense for Shelby

Many applications rely on files:

* Images
* Documents
* Media assets
* User-generated content

Shelby provides decentralized, censorship-resistant storage for these files. In this project, we take that one step further by **reacting to file activity**:

* Uploading a file earns points
* Downloading a file unlocks progress
* Reaching milestones advances levels

> Shelby handles the storage layer. The game logic simply responds to what users do with files.

This separation is intentional and important.

---

## Core Game Concept: Upload Quest

Users progress through levels by completing file-related tasks.

### Example Rules

| Action             | Reward     |
| ------------------ | ---------- |
| Upload an image    | +10 points |
| Upload a text file | +5 points  |
| Upload a document  | +15 points |
| Download any file  | +3 points  |

### Level Thresholds

| Level   | Requirement |
| ------- | ----------- |
| Level 1 | Default     |
| Level 2 | 30 points   |
| Level 3 | 70 points   |
| Level 4 | 120 points  |

These values are intentionally simple and can be adjusted easily.

---

## User Identity Model

Each user is identified by a **wallet address**.

* No blockchain transactions are required
* The wallet is used purely as a unique identifier

Example player record:

```json
{
  "wallet": "0xABC123...",
  "points": 45,
  "level": 2,
  "uploads": 4
}
```

This keeps the app lightweight while still being Web3-native.

---

## How Shelby Is Used

Shelby is used for exactly two things:

1. **Uploading files** via the Shelby SDK
2. **Downloading files** via the Shelby SDK

The app then:

* Inspects the file type
* Awards points
* Updates player state

> Shelby is not responsible for points, levels, or leaderboards.
> It simply provides the decentralized file infrastructure.

This keeps responsibilities clean and modular.

---

## Application Flow

A typical user session looks like this:

1. User starts the app
2. User enters their wallet address
3. User uploads a file using Shelby
4. App determines file type
5. App awards points
6. App checks for level upgrades
7. Leaderboard is updated
8. User can download files to earn bonus points

Each step is intentionally explicit and beginner-friendly.

---

## Leaderboard System

The leaderboard is calculated by:

* Storing player data locally in a JSON file
* Sorting players by total points
* Displaying top players

Example leaderboard logic:

```text
1. 0xAAA... — 120 points
2. 0xBBB... — 95 points
3. 0xCCC... — 70 points
```

This approach avoids databases and keeps the demo easy to understand.

---

## Repository Structure

```text
part-4-game-app/
├── app.js            # Main application entry
├── gameLogic.js      # Points, levels, and rules
├── players.json      # Stored player data
├── README.md         # This file
└── .env              # Shelby config
```

Each file has a single responsibility to reduce confusion.

---

## Why This Is Useful Beyond a Game

This pattern can be reused for:

* Hackathon challenges
* Developer onboarding quests
* Learning platforms
* Storage-based reward systems
* Community engagement tools

The same logic applies anywhere file interaction matters.

---

## Limitations & Scope

This project intentionally does **not** include:

* Smart contracts
* Real tokens or payments
* Production authentication
* Security hardening

It is meant as an **educational reference implementation**.

---

## Summary

In this part, you learned how to:

* Build an interactive application on top of Shelby
* Treat files as gameplay actions
* Design a points and progression system
* Add competition through leaderboards

Shelby remains the decentralized storage backbone, while your app defines how users interact with it.

---

## What’s Next

Possible extensions include:

* Web UI
* Wallet signature login
* Database-backed leaderboards
* NFT or onchain rewards

But even in its current form, this project demonstrates a **creative and practical Shelby use case**.
