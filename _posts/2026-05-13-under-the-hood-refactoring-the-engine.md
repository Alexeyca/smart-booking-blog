---
layout: post
title: "Under the Hood — Rethinking the Cart for Chat-Based Booking"
date: 2026-05-13
description: "Our booking cart only allowed one item per vertical. Real travel means multi-city trips, multiple rooms, group bookings. Here's why we paused to refactor the core."
categories: [engineering, architecture]
tags: [refactoring, cart architecture, conversational commerce, state management, event sourcing, booking engine, chat UX, multi-city]
---

We've been building travel technology for a long time. The booking domain — hotels, flights, tours, trains — is well-understood. The supply side, the pricing models, the fulfillment pipelines — all solved problems.

What we got wrong was the cart.

## The Assumption

When we built the initial engine, we made a simplifying assumption: one cart holds one booking per vertical. One hotel. One flight. One tour. If the user picks a different hotel, it replaces the first one.

For a simple use case — "I need a hotel in Barcelona for the weekend" — this works fine.

But real travel doesn't work like that.

## How Real Travel Works

A destination wedding in Santorini. The couple books the main suite. Parents need a room on the same floor. Groomsmen book three rooms in the same hotel, different dates, each paying their own card. One conversation, one hotel, ten rooms, five different payment methods.

A business traveler books a multi-city itinerary: London → Berlin → Paris. Three hotels, three train segments, all in one conversation. They need to modify the Berlin leg without touching the rest.

A group of four friends plans a weekend together. They share the same hotel, but each pays for their own room. Different names, different payment details, one conversation.

None of these scenarios fit the "one item per vertical" model.

![Chat cart interface showing multiple booking options](https://www.gochattravel.com/assets/images/white-label/white-label-chatcart.png.jpg)

## What Broke

The cart couldn't represent:

- **Multiple hotels in one trip** — adding a second hotel replaced the first. No way to hold both
- **Multi-room bookings with different guests** — one offer, multiple rooms, each with its own guest details and payment
- **Multi-city itineraries** — three hotels across three cities, all part of one trip, each independently modifiable
- **Split payments** — same booking, different people paying for different parts
- **Parallel exploration** — user wants to compare two hotels side by side before deciding, not replace one with the other

Each of these is a standard travel booking scenario. Each one required the cart to hold multiple items of the same vertical simultaneously. Our cart couldn't.

Patching it meant adding special-case logic for every combination: multi-hotel, multi-flight, multi-room, split-pay, multi-city. The state machine grew exponentially. Each new scenario doubled the edge cases.

## The Decision

We could have kept patching. Add flags, add arrays, add special handlers. Ship features one by one.

But we've built systems like this before. The "one item" assumption is load-bearing — it shapes the entire data model, the state machine, the fulfillment pipeline. You can't patch it. You have to redesign.

So we paused new vertical development and started refactoring the cart from the ground up.

## What We're Building

**Unlimited Cart Items**
The cart no longer assumes one item per vertical. A single conversation can hold three hotels, two flights, and a tour — all coexisting, all independently modifiable.

**Item Grouping**
Cart items can be grouped into trips. All items in a trip share context (dates, destination) but remain independently bookable. User can confirm the hotel without confirming the flight.

**Per-Item Guest and Payment**
Each cart item carries its own guest details and payment information. Same hotel, two rooms, different guests, different cards — no problem.

**Event-Sourced State**
Every cart mutation is an event. Add a hotel — event. Remove it — event. Change dates — event. This means full history, full recoverability, and the ability to branch (what if we change the Berlin leg?).

**Parallel Exploration**
Users can hold multiple options for the same leg of a trip without committing. Compare two hotels side by side, then confirm one. The other drops out cleanly.

## Why This Matters

The cart is the heart of any booking system. If the cart can't represent real travel scenarios, the system fails — not because the supply side is broken, but because the data model can't express what the user needs.

For chat-based booking, this is even more critical. The conversation is the interface to the cart. If the cart model is too rigid, the conversation becomes a frustrating game of "the bot replaced my hotel again."

## What This Means for Users

Hotel booking continues as normal. The refactor is happening under the hood.

When it ships, the cart will support everything real travel requires: multiple rooms, multi-city trips, group bookings with split payments, parallel exploration. All within the same conversation.

## Lessons Learned

1. **Don't assume simplicity.** "One item per vertical" felt like a reasonable starting point. It wasn't. Real travel is multi-everything.
2. **The cart model is the product.** Not the AI, not the chat interface. The cart. That's where the complexity lives and where the user experience is won or lost.
3. **Refactor before it hurts.** Every week we spent patching the old cart made the redesign harder. We caught it early.
4. **Event sourcing fits booking.** Travel plans change constantly. An event-sourced cart makes mutations cheap, reversible, and auditable.

## What's Next

We'll share more as the new cart architecture ships. And once it's solid, the next booking verticals roll out fast.

Stay tuned.
