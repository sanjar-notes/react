# 43. Mocking HTTP Requests
Created Mon Sep 30, 2024 at 6:36 PM

## Situation
Making real network calls during tests is:
1. Slow
2. Expensive
3. Unreliable - state may change too much.

## Fix
Mocking HTTP calls will make them faster, inexpensive and reliable.

Real APIs are used only for e2e or some important integration tests. Unit tests are almost always mocked.

## How
[MSW](https://mswjs.io/) is the easiest way to set up HTTP mocking without writing server code.