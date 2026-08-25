# 2306565 — What is a database?

A short hands-on introduction to databases and SQL for chemical engineering students,
taught on one month of real-shaped data from a boiler house.

**You do not need to install anything. Everything runs in your browser.**

---

## Start here

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ratchanon12/2306565/blob/main/boiler_intro.ipynb)

Click the badge above. The notebook opens in Google Colab.

Then, before you type anything:

> ### File → Save a copy in Drive
>
> This gives you your own copy, saved to your Google account, so the answers you write today
> are still there tomorrow. **Work in that copy, not the original.**

Run cells with the **▶** button on the left of each cell, or **Shift + Enter**.

The first cell builds the database for you. There is nothing to download and nothing to
upload.

---

## What is in this repository

| File | What it is |
|---|---|
| [`boiler_intro.ipynb`](boiler_intro.ipynb) | **The notebook you will work in.** Start here |
| [`handouts/Workbook_STUDENT.pdf`](handouts/Workbook_STUDENT.pdf) | Printable workbook: the database in full, a one-page SQL cheat sheet, and the three exercises |
| [`slides/`](slides) | The lecture slides |
| [`boilerhouse.db`](boilerhouse.db) | The database as a file. You only need this if you want to open it in DB Browser for SQLite instead of using Colab |

---

## What you will learn

Not how to memorise SQL. By the end of the session you should be able to say:

- what a **table** is, and what one row of it represents
- why data is **split across several tables** instead of kept in one big sheet
- how to **put it back together** with a `JOIN`

The whole vocabulary for the day is twelve words:

```
SELECT   FROM   WHERE   ORDER BY   LIMIT
COUNT    AVG    MIN     MAX        SUM
GROUP BY        JOIN ... ON
```

---

## The database

Five tables, one month of data (April 2026) from a boiler house with three gas-fired boilers.
It is deliberately small — you can scroll through any table and check an answer with your own
eyes.

| Table | One row is | Rows |
|---|---|---|
| `boilers` | one boiler | 3 |
| `operators` | one person | 6 |
| `readings` | one instrument reading, every 4 hours | 540 |
| `daily_logs` | one boiler on one day | 90 |
| `water_tests` | one weekly water sample | 15 |

A row in `readings` does not say *"Boiler 2"* — it says `boiler_id = 2`, and you look `2` up
in the `boilers` table. Storing a fact once and pointing at it from everywhere else is the
whole idea of a database.

---

## The three exercises

1. **Looking at the data** — `SELECT`, `WHERE`, `ORDER BY`, `LIMIT`, `COUNT`
2. **Summarising** — `AVG`, `MIN`, `MAX`, `SUM`, `GROUP BY`
3. **Joining two tables** — `JOIN ... ON`, and answering a real question

One of the three boilers is quietly wasting gas. Two queries are enough to find it, put a
number on it, and say why — which is the point of the whole session.

---

## If something goes wrong

| What you see | What to do |
|---|---|
| Colab says it disconnected | Run the first two cells again. Nothing is lost. |
| `no such table: boilers` | You have not run the first two cells yet, or the runtime restarted. Run them. |
| `no such column: B-02` | Text needs **single** quotes: `code = 'B-02'`, not `code = "B-02"`. |
| An empty result | Your `WHERE` is too strict. Take it off and look at the raw rows first. |
| You want to start a question again | Just retype the query and run the cell. You cannot damage anything. |
