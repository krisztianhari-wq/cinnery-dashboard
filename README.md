# Cinnery Counter

Trading overview for the Cinnery bakery (Zwanestraat 29, Groningen).
One static page, no build step, no framework — open `index.html` or the published page.

- **Day** — revenue, orders, average basket and rolls sold, hour-by-hour split between
  in-store (Lightspeed POS) and pickup pre-orders (Order Anywhere), the pickup queue,
  fulfilment times, payment split, product mix with sell-out times, last 14 days.
- **Month** — the same totals for a month, day-by-day chart, weekday pattern and a
  month-by-month comparison against the previous year.
- **Year** — year to date, month by month, quarters, and the year-on-year change.

While a month or year is still running it is compared with the same stretch of the
earlier period, not the whole of it.

Three languages — English, Dutch, Hungarian — from the switcher in the header. English
is the default; the choice is remembered in the browser. All copy lives in the `I18N`
object at the top of the script, where the English string is its own key.

Figures are generated demo data until Lightspeed is connected; the page says so while
that is the case. Real days go into the `LIVE_DAYS` object at the top of the script,
keyed by ISO date — a day listed there replaces the demo day.

Built by sadrobot.
