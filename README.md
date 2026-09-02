# 2306565 — What is a database?

A short hands-on introduction to databases and SQL for chemical engineering students,
taught on three months of real-shaped data from a boiler house.

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
| [`handouts/Boilerhouse_SQL_reference.pdf`](handouts/Boilerhouse_SQL_reference.pdf) | **Print this and keep it beside you.** One page: every table and column, and the SQL you need |
| [`slides/`](slides) | The lecture slides |
| [`boilerhouse.db`](boilerhouse.db) | The database as a file. You only need this if you want to open it in DB Browser for SQLite instead of using Colab |

---

## What you will learn

Not how to memorise SQL. By the end of the session you should be able to say:

- what a **table** is, and what one row of it represents
- why data is **split across several tables** instead of kept in one big sheet
- how to **put it back together** with a `JOIN`

- how to ask whether something is **getting worse**, not just whether it is bad
- how to back a finding with **two independent measurements** instead of one

The vocabulary for the day:

```
SELECT   FROM   WHERE   AND / OR   ORDER BY   LIMIT   DISTINCT
COUNT    AVG    MIN     MAX        SUM
GROUP BY        HAVING             JOIN ... ON
substr(ts, 1, 7)     a sub-query in brackets
```

Every exercise marks itself. Write your query inside `check("2.2", q("""..."""))` and it will
tell you whether the answer is right; `hint("2.2")` gives a nudge and `solution("2.2")` gives
a worked answer once you have tried.

---

## The database

Seven tables, three months of data (February to April 2026) from a boiler house with four
gas-fired boilers. It is still small enough to scroll through and check an answer with your own
eyes — and big enough to hide things.

| Table | One row is | Rows |
|---|---|---|
| `boilers` | one boiler — tag, maker, rating, year | 4 |
| `operators` | one person on the shift roster | 6 |
| `readings` | one instrument reading, every 4 hours | 1,866 |
| `daily_logs` | one boiler on one day | 311 |
| `water_tests` | one weekly water sample | 45 |
| `maintenance_events` | one job done on one boiler | 14 |
| `fuel_prices` | what gas cost in one month | 3 |

Hidden in there, for you to find: a boiler that is slowly fouling, another that had the same
problem and was cured, three days when a boiler was off line, a thermocouple that spent a day
reading zero, one impossible 511 °C spike, and a maintenance log that explains all of it.

A row in `readings` never names a boiler — it says `boiler_id = 2`. That id is **not** the tag
painted on the machine: `boiler_id = 2` is tag `B-2103` (the South watertube), not `B-2102`.
The only way to know which boiler a row belongs to is to look the id up in `boilers` with a
`JOIN`. Storing a fact once and pointing at it from everywhere else is the whole idea of a
database — and guessing the machine from its id is the habit this notebook is built to break.

---

## The five exercises

1. **Reading the data** — `SELECT`, `WHERE`, `AND`/`OR`, `ORDER BY`, `LIMIT`, `COUNT`, `DISTINCT`
2. **Summarising** — `AVG`, `MIN`, `MAX`, `SUM`, `GROUP BY`, `HAVING`
3. **Joining tables** — `JOIN ... ON`, two joins at once, load as a share of rating, and the
   maintenance log
4. **Investigating** — month by month with `substr`, sub-queries, counting only the rows that
   matter, and the missing days
5. **The case, and the money** — joining on a month you cut out yourself, and what the waste cost

29 tasks in all. Exercises 1–3 give you a query with blanks to fill in, Exercise 4 gives you
less, and Exercise 5 gives you almost nothing. A final "take it further" list has no answers.

One of the four boilers is quietly wasting gas, and it is getting worse every month. The stack
thermocouple and the gas meter are different instruments on different tables; the maintenance log
is fourteen rows of somebody's typing. By the end of the session you will have made all three
agree, and put a price on it.

---

## If something goes wrong

| What you see | What to do |
|---|---|
| Colab says it disconnected | Run the first two cells again. Nothing is lost. |
| `no such table: boilers` | You have not run the first two cells yet, or the runtime restarted. Run them. |
| `no such column: B-2103` | Text needs **single** quotes: `code = 'B-2103'`, not `code = "B-2103"`. |
| `[2.2] not there yet` | Your query ran, but the answer is not the expected one. Try `hint("2.2")`. |
| Percentages all come out `0` | Integer division. Write `100.0 * ...`, not `100 * ...`. |
| An empty result | Your `WHERE` is too strict. Take it off and look at the raw rows first. |
| You want to start a question again | Just retype the query and run the cell. You cannot damage anything. |
