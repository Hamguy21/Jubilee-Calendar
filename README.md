# 📅 Jubilee Calendar

> A reformed calendar system with 13 equal months, a dedicated intercalary month, and year-cycle rules anchored to Year 0.

---

## Overview

The Jubilee Calendar is a proposed reform of the Gregorian calendar that addresses its irregular month lengths, misaligned week cycles, and accumulated drift. Every year is structured identically — same month lengths, same weekday alignment — with a small set of special days handling the astronomical remainder.

---

## Gregorian vs Jubilee

| Aspect                           | Gregorian Calendar                         | Jubilee Calendar                                           |
|----------------------------------|--------------------------------------------|------------------------------------------------------------|
| Months per standard year         | 12                                         | 13                                                         |
| Month lengths                    | Irregular: 28, 29, 30, or 31 days          | Regular: 28 days each                                      |
| Weeks per month                  | Varies by month and year                   | Exactly 4 every month                                      |
| Weekday alignment year to year   | Shifts annually                            | Fixed for all standard months                              |
| Ordinary year length             | 365 days                                   | 365 days                                                   |
| Leap / correction method         | Leap day added to February in leap years   | Reset Day added after December 28; skipped every 128 years |
| Extra month                      | None                                       | Jubilee month of 7 days every 28 years                     |
| Long-year length                 | 366 days in leap years                     | 372 days in Jubilee years                                  |
| Days outside weekday cycle       | None                                       | Reset Day, plus Jubilee days after year-end                |
| Internal structure               | Astronomically inherited historical system | Deliberately regularized reform system                     |
| Conversion basis in this project | Native civil calendar                      | Exact epoch-based mapping to Gregorian via day offsets     |

---

## Structure

### The Year

| Component                 | Count          | Days                        |
|---------------------------|----------------|-----------------------------|
| Standard months           | 13             | 28 each                     |
| Reset Day                 | 1              | 1 (omitted every 128 years) |
| Jubilee Month             | every 28 years | 7 days                      |
| **Total (standard year)** |                | **365**                     |
| **Total (Jubilee year)**  |                | **372**                     |

### The Months

The calendar inserts **Sol** between June and July, splitting the Gregorian second half of the year into more equal segments.

> **Note:** This mapping is for conceptual familiarity only. The Jubilee Calendar is independent of the Gregorian system and uses its own epoch (Year 0).

| # | Name         | Notes                       |
|---|--------------|-----------------------------|
| 1 | January      |                             |
| 2 | February     |                             |
| 3 | March        |                             |
| 4 | April        |                             |
| 5 | May          |                             |
| 6 | June         |                             |
| 7 | **Sol**      | Intercalary month (new)     |
| 8 | July         |                             |
| 9 | August       |                             |
| 10 | September   |                             |
| 11 | October     |                             |
| 12 | November    |                             |
| 13 | December    | Followed by Reset Day       |
| 14 | **Jubilee** | Jubilee years only — 7 days |

Every month has exactly **28 days**, forming exactly **4 complete weeks**. This means every month starts on the same weekday every year.

---

## Special Days

### Reset Day

Reset Day falls after December 28th and serves as the calendar's New Year marker. It sits outside the normal month/week structure — it is not assigned a weekday.

- Occurs every year; it is **skipped** only in years divisible by **128** (see `Reset Skipped` in [Cycle Rules](#cycle-rules-year-0-anchor))
- Observed as **World Reset Day**, a global civic holiday
- When skipped (every 128th year), the calendar absorbs the correction silently

### Jubilee Month

Every **28 years**, a 7-day month called **Jubilee** is appended after December's Reset Day. These years are called **Jubilee Years**.

- Jubilee years: any year where `year % 28 === 0`
- The Jubilee month contains its own dedicated festivals (see [Holidays](#holidays))
- Jubilee years are visually marked throughout the calendar interface

---

## Cycle Rules (Year 0 Anchor)

All cycle calculations are anchored to **Year 0**.

```
Jubilee Year  →  year % 28 === 0
Reset Skipped →  year % 128 === 0
```

These two rules are the complete ruleset. There are no secondary correction cycles.

---

## Holidays

The calendar includes a built-in holiday set. Any date originally falling on day 29, 30, or 31 of a Gregorian month is moved forward to the following month.

| Month     | Day | Holiday                        |
|-----------|-----|--------------------------------|
| January   | 1   | New Year's Day                 |
| February  | 14  | Valentine's Day                |
| March     | 8   | International Women's Day      |
| March     | 17  | St. Patrick's Day              |
| March     | 20  | Spring Equinox                 |
| April     | 1   | April Fools' Day               |
| April     | 22  | Earth Day                      |
| May       | 1   | International Workers' Day     |
| June      | 5   | World Environment Day          |
| June      | 21  | Summer Solstice                |
| July      | 4   | Independence Day               |
| August    | 15  | Assumption Day                 |
| September | 22  | Autumn Equinox                 |
| October   | 24  | United Nations Day             |
| November  | 11  | Veterans Day / Armistice Day   |
| December  | 21  | Winter Solstice                |
| December  | 25  | Christmas Day                  |
| December  | 26  | Boxing Day                     |
| December  | 29  | **World Reset Day / New Year** |
| Jubilee   | 1   | Jubilee Festival               |
| Jubilee   | 7   | Jubilee Closure                |

> **Shifting example:** New Year's Day is Gregorian Jan 1, which is within the 28-day limit, so it stays. A holiday originally on "March 31" would shift to April 3 (31 − 28 = day 3 of the next month).

---

## Navigation

The calendar interface has three zoom levels:

| Level      | Shows                              | Navigate                      |
|------------|------------------------------------|-------------------------------|
| **Month**  | Individual days in a 7-column grid | ← / → moves month by month    |
| **Year**   | All months as cards                | ← / → moves year by year      |
| **Decade** | 12 years as cards                  | ← / → moves by 12-year blocks |

Click the title label to zoom out one level. Click **Now** to return to the current date.

---

## Visual Legend

| Color          | Meaning                         |
|----------------|---------------------------------|
| 🟡 Gold        | Holiday                        |
| 🔴 Red (ember) | Reset Day                      |
| 🔵 Ice blue    | Today                          |
| 🟣 Violet      | Jubilee month / year           |
| 🔴 Red tag     | No Reset year (128-year cycle) |

---

## Epoch Converter

The calendar includes a built-in holiday set. Any date originally falling on day 29, 30, or 31 of a Gregorian month is moved forward to the following month.
`jubilee-converter.html` translates dates between the Gregorian and Jubilee systems in both directions.

### Gregorian → Jubilee

Enter a Gregorian year, month, and day. The converter reduces that date to an exact absolute day offset from the shared epoch, then resolves the corresponding Jubilee year, month, and day — including Reset Day and the Jubilee month where applicable.

- Day out of range for the given month
- Jubilee month entered for a non-Jubilee year
- Reset Day entered for a 128-year skip year
- Leap year February overflow

### Conversion Method

All conversions use an **exact epoch-based day-offset** approach anchored to a shared epoch: `Jubilee Day 0 = Gregorian January 1, 2000 CE`. Every date is first reduced to an absolute integer day count from that anchor, and then resolved into the target calendar. This handles multi-year transitions, leap years, and BC dates exactly — no proportional approximation.

**Absolute day (from epoch)** means the number of days between the input date and the shared anchor date.

- `0` means the epoch day itself: Gregorian January 1, 2000 CE
- positive values mean days after the epoch
- negative values mean days before the epoch

This gives both calendars one shared timeline. The converter first turns the input into that timeline position, then reconstructs the matching date in the other calendar.

**DOY position in year** means **Day Of Year**: the date's 1-based position within its own year.

- DOY `1` = the first day of the year
- DOY `32` = the 32nd day of the year
- DOY `365` or `366` = the last Gregorian day of the year, depending on leap year

In other words, `daysToYearStart(year)` tells you where the year begins on the absolute timeline, and `DOY(date)` tells you how far into that year the date sits.

```
Step 1 — abs = daysToYearStart(input_year) + DOY(input_date) − 1
Step 2 — find output year y such that yearStart(y) ≤ abs < yearStart(y+1)
Step 3 — output_DOY = abs − yearStart(y) + 1, then resolve month and day
```

Example:

- Gregorian March 1, 2000 CE has `daysToYearStart(2000) = 0`
- Its Gregorian DOY is `61` because 2000 is a leap year
- So its absolute day is `0 + 61 − 1 = 60`

That means March 1, 2000 CE is the 60th day after the epoch day.

### BC Year Support

BC years are supported using **astronomical year numbering** throughout:

| Historical | Astronomical |
|------------|--------------|
| 1 BC       | year 0       |
| 2 BC       | year -1      |
| 45 BC      | year -44     |


Enter a negative number in the Year field to use a BC date. The proleptic Gregorian leap rule (`y%4==0 && y%100!=0 || y%400==0`) extends correctly into negative years with no special cases.

### Validation
The converter catches and reports specific, context-aware errors:

- Day out of range, with the correct maximum stated (e.g. `February 29 does not exist in 1900 CE — not a Gregorian leap year. Next leap year: 1904 CE`)
- Jubilee month entered for a non-Jubilee year, with the next Jubilee year shown
- Reset Day entered for a 128-year skip year, with the next valid Reset Day shown
- Day > 28 in a standard Jubilee month, with a hint about Reset Day if December was selected

### DOY Math Panel

Clicking **Show Math** after a conversion reveals the full workings:

- Input and output dates side by side
- Input and output DOY with year totals
- Absolute day offset from epoch
- Percentage position within the year (input vs output)
- The three-step formula with actual values substituted in
- Epoch anchor and BC rule reference

---

## Implementation

The project consists of two self-contained HTML files with no build step or external dependencies beyond Google Fonts.

```
jubilee-calendar.html
├── Starfield animation (Canvas)
├── Calendar logic (vanilla JS)
│   ├── isJubileeYear(y)   →  y % 28 === 0
│   ├── isResetSkipped(y)  →  y % 128 === 0
│   └── getHoliday(m, d)   →  string | null
└── UI (CSS + HTML)
    ├── Month view
    ├── Year view
    └── Decade view

jubilee-converter.html
├── Starfield animation (Canvas, shared pattern)
├── Epoch arithmetic (vanilla JS)
│   ├── gregLeapsBelow(y)              →  leap count below year y (handles BC)
│   ├── gregDaysToYearStart(y)         →  days from epoch to year y start
│   ├── jubDaysToYearStart(y)          →  days from epoch to Jubilee year y start
│   ├── gregToAbsolute(y, m0, d)       →  absolute day offset
│   ├── jubToAbsolute(y, m0, d)        →  absolute day offset
│   ├── absoluteToGreg(abs)            →  exact Gregorian resolution via bounded year-start search
│   └── absoluteToJub(abs)             →  exact Jubilee resolution via bounded year-start search
├── Validation (vanilla JS)
│   ├── validateGreg(y, m0, d)         →  null | error string
│   └── validateJub(y, m0, d)          →  null | error string
└── UI (CSS + HTML)
    ├── Direction toggle (Gregorian ↔ Jubilee)
    ├── Dynamic input fields (BC hint included)
    ├── Result card with contextual notes
    ├── Math workings panel (toggle)
    └── Month quick-reference table
```

To run: open either file in any modern browser. No build step required.

---

## Design

The interface uses a **Void Observatory** aesthetic:

- **[Cinzel](https://fonts.google.com/specimen/Cinzel)** — serif display font for titles and month names
- **[JetBrains Mono](https://fonts.google.com/specimen/JetBrains+Mono)** — monospaced font for dates and metadata
- Animated star field background
- Dark void palette with precise accent glows per date type

---

## License

This project is released for open use. The calendar system itself is a design proposal — not an official standard.
