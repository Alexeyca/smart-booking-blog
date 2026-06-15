---
layout: page
title: About GoChatTravel
permalink: /about/
description: "GoChatTravel is a chat-first travel booking platform. Book hotels, flights, tours, and trains through WhatsApp, Telegram, or Instagram. Powered by deterministic Rust engine."
---

**Book hotels, flights, tours, and trains through WhatsApp, Telegram, or Instagram — no apps, no registrations, no redirects.**

- **Chat-first booking** — search, compare, pay, and get confirmation entirely inside your messenger
- **Deterministic Rust engine** — all business logic, pricing, and fulfillment run on a modular monolith built in Rust; LLM handles only the conversational interface
- **Stripe payments** — credit card data goes directly between you and Stripe; we never see card details

## What We Do

Open WhatsApp, Telegram, Facebook Messenger, WeChat, or Instagram and start a conversation. Describe what you need — a beach resort in Bali, a boutique hotel in Tokyo, a multi-city European trip. The AI parses natural language, searches available options, and presents relevant matches.

The entire booking process happens in chat: search, compare, book, pay, receive confirmation. No redirects. No external websites. No app switching.

## Key Features

- **Multi-room bookings** — book several rooms in one reservation, each with different guest details
- **90+ languages** — chat in your native language
- **Free cancellation** — most bookings offer free cancellation, and we always warn you about any fees upfront
- **24/7 support** — human-backed assistance powered by Nuitee
- **Wholesale pricing** — competitive rates through direct hotel and distributor partnerships

## Under the Hood

GoChatTravel is powered by a deterministic booking engine built in Rust. The core architecture is a modular monolith — combining the simplicity of a single codebase with the scalability of independent modules.

The engine handles thousands of requests per second while maintaining minimal resource footprint. Every booking operation is deterministic: given the same inputs, the engine produces the same outputs. This makes the system predictable, testable, and reliable at scale.

LLM is used only for conversational interface — understanding user intent and maintaining natural dialogue. All business logic, pricing, search, and fulfillment runs on the deterministic Rust engine. No AI hallucinations in your booking.

## Who We Are

We're a team with 30+ years of experience in travel technology. We've built booking engines, worked with major OTAs, and understand the supply side inside out. GoChatTravel is our answer to a simple question: why is booking travel still so complicated in 2026?

## Try It

👉 **[gochattravel.com](https://www.gochattravel.com)** — start booking through your favorite messenger.

## This Blog

Product updates, engineering insights, travel tips, and behind-the-scenes stories from building a chat-first travel platform.

Questions or feedback? [info@gochattravel.com](mailto:info@gochattravel.com).
