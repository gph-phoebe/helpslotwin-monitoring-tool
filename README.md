# HelpSlotWin

HelpSlotWin is a web-based slot jackpot monitor built to track visible jackpot meter values, store historical snapshots, and show changes in one simple dashboard. The point is not to act like a casino platform. It is there to help users monitor jackpot movement without checking pages manually over and over.

Live Site: [https://helpslotwinhub.com/](https://helpslotwinhub.com/)

## What It Is For

HelpSlotWin is meant to make jackpot tracking easier to follow. Instead of jumping between different pages and trying to remember which jackpot meter moved, users can view normalized data in one place and compare trends over time.

It works as a monitoring layer, not a game service. It watches supported sources, captures jackpot values, stores those readings, and shows them through a dashboard built for quick viewing.

## What the Product Does

At a basic level, HelpSlotWin does four things:

- collects jackpot values from supported pages
- normalizes the data into one format
- stores time-based snapshots
- displays the results through a searchable dashboard

This keeps the product focused. It is not trying to replace a casino lobby or become an all-in-one platform. It is a slot jackpot monitor first.

## Tech Stack

HelpSlotWin uses a practical stack built for monitoring and dashboard delivery.

The frontend uses Next.js with React and TypeScript. This keeps the interface fast, easy to navigate, and flexible enough for tables, filters, and charts.

The backend uses FastAPI in Python. That makes sense for monitoring work because Python is good for scraping, parsing, scheduling, and API delivery.

PostgreSQL handles storage for sources, jackpot readings, and historical snapshots.

Redis with a background job layer such as RQ or Celery is used for scheduled polling and queue-based processing.

Playwright is used for source extraction, especially where jackpot meters are rendered dynamically instead of appearing as clean static HTML.

## How It Works

HelpSlotWin starts from a list of supported sources. Each source includes its URL, polling interval, parsing logic, and basic validation rules.

When a scheduled worker runs, it opens the source, waits for the jackpot meter to load, extracts the visible value, and converts it into a normalized reading. Before saving, the system checks whether the value looks valid and whether the jump from the previous reading makes sense.

Once accepted, the reading is stored as a snapshot in PostgreSQL. The frontend then reads from the API instead of scraping directly, which keeps the dashboard faster and more stable.

## Why the Architecture Is Set Up This Way

The product separates monitoring from presentation on purpose. Scraping and data collection can be slow or unstable depending on the source page, so that work happens in the background.

This means the dashboard is not trying to fetch live source data every time a user opens it. Users see stored and structured data instead of waiting on real-time scraping. That makes the tool more usable and easier to scale.

It also makes HelpSlotWin easier to expand later. New sources, alerts, and additional dashboard views can be added without rebuilding the whole product.

## Final Note

HelpSlotWin is a focused web-first monitoring tool for jackpot tracking. Its main value is simple: watch jackpot meter values, keep historical records, and make those trends easier to read in one place.

The current setup uses Next.js for the dashboard, FastAPI for the backend, PostgreSQL for storage, Redis for job handling, and Playwright for browser-based extraction. That keeps the product realistic, maintainable, and ready to improve over time.)
