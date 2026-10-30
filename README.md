# Maryland early voting, 2026 vs. 2022 and 2024

Data, fact-check code and graphics behind Capital News Service coverage of mail-in and early in-person voting before Maryland's Nov. 3, 2026 general election.

The data comes from the Maryland State Board of Elections' daily mail-in and early voting reports for the 2022, 2024 and 2026 general elections, most of it obtained through a Maryland Public Information Act request.

**One gap in the state board's records.** The archive the board provided has no spreadsheet of the Oct. 26, 2022 mail-in report, only a PDF. That day's figures instead come from a copy of the report that Derek Willis, a data journalism professor at the University of Maryland, College Park, had previously downloaded from the State Board of Elections (`supplemental_reports/absentee_ballots_20221027.xlsx`).

## The graphics

Numbered in the order they appear in the article.

| # | Graphic | What it shows | Table in `output/` |
|---|---|---|---|
| 1 | [One Week Out: Early voting spikes in Maryland](https://dlanderm-dal.github.io/md-early-voting-2026/table_1_stacked_bars_d3.html) (D3) | Mail-in, early in-person and combined votes by party, seven days before Election Day, 2022 vs. 2026 | `voting_methods_flourish.csv`, `methods_table_factcheck.csv` |
| 2 | [Who accounts for the jump in early voting in Maryland?](https://public.flourish.studio/visualisation/30737421/) (Flourish table) | Each party's share of the change in votes from 2022 to 2026, by voting method | `methods_party_change_flourish.csv`, `methods_party_change_table.csv` |
| 3 | [Marylanders increasingly utilizing methods of voting before election day](https://public.flourish.studio/visualisation/30731131/) (Flourish line chart) | Running totals of mail-in, early in-person and combined votes from 16 to 5 days before Election Day, 2022, 2024 and 2026 | `early_voting_time_domain_graphic.csv`, `daily_wide.csv`, `mail_daily.csv` |
| 4 | [Congressional districts all see spike in early in-person voting](https://dlanderm-dal.github.io/md-early-voting-2026/section_5_districts_stacked_bars_d3.html) (D3) | Early in-person votes by party in each of Maryland's eight congressional districts, seven days out, with the 2026 candidates | `in_person_congressional_flourish.csv`, `cd_table_factcheck.csv` |

The county figures in the article's text (Montgomery County up 46%, Baltimore City down 24%, 11% more ballots statewide before in-person early voting began) compare mail-in ballots received on Oct. 26, 2022 and Oct. 21, 2026. They're built in the Rmd as `pre_in_person_early_table`.

Graphics 1 and 4 are D3 pages served by GitHub Pages and embedded in the article as iframes. Graphics 2 and 3 are published in Flourish. Graphics 1 and 4 also have Flourish versions, and their `*_flourish.csv` files are those charts' uploads.

## How the numbers are built

Everything is in **`early_voting_factcheck_self.Rmd`**, which rebuilds each graphic's numbers from the original state reports. Run its chunks in order from this folder in R or RStudio. It needs the `tidyverse`, `janitor`, `readxl` and `jsonlite` packages. It writes every table to `output/`.

Definitions and choices:

- **Mail-in** = mail-in ballots *received* by election officials, as of 6 p.m. on the report's date. Each daily report is a running total.
- **Early in-person** = votes *cast* at early voting centers. The raw files list each day's votes separately (Day1 to Day8), so the running totals are added up in the Rmd.
- **Combined** = mail-in + early in-person.
- **Other** = voters not registered as Democrats or Republicans.
- **Comparison points.** Years are lined up by days before Election Day, not by calendar date. Election Days were Nov. 8, 2022, Nov. 5, 2024 and Nov. 3, 2026.
  - "Seven days before Election Day" is Nov. 1, 2022 and Oct. 27, 2026.
  - The line chart runs from 16 days out (the earliest 2022 report in the records) to 5 days out (the last day of early voting).
- **Early voting dates.** State law sets early voting "beginning the second Thursday before a primary or general election through the Thursday before the election" ([Chapter 660, 2021](https://mgaleg.maryland.gov/2021RS/chapters_noln/Ch_660_hb0206E.pdf)). That was Oct. 27 to Nov. 3, 2022; Oct. 24 to Oct. 31, 2024; and Oct. 22 to Oct. 29, 2026.
- **Dates come from the reports.** Each mail-in report is dated from its own "As of" line, not its folder name. The 2024 and 2026 folders are named for the day the board posted the report, one day after its "As of" date.
- **Candidates.** The graphic 4 candidate lists come from the board's 2026 candidate list. They show only candidates printed on the ballot; write-in candidates are left out.

## Folders

- **`Press Reports-selected/`**: the board's daily reports from the records request, by election. The general elections (`GG22`, `PG24`, `GG26`) are used; the primary folders (`GP22`, `PP24`) aren't.
- **`direct-download/`**: 2026 reports downloaded from the board's website on Oct. 28, 2026. The records request stops at Oct. 26, 2026, so these supply Oct. 27.
- **`supplemental_reports/`**: files that fill gaps:
  - `absentee_ballots_20221027.xlsx`: the Oct. 26, 2022 mail-in report. The board's records have only a PDF for that day, so this copy comes from Derek Willis, a data journalism professor at the University of Maryland, College Park, who downloaded it from the board at the time.
  - `2026_GG_representativeincongressbydistrict_candidatelist.csv`: the board's 2026 congressional candidate list, downloaded Oct. 26, 2026.
  - `US_Congressional_Districts_2022.geojson`: Maryland iMAP's congressional district file, downloaded Oct. 26, 2026. The Rmd uses it to identify each district's incumbent.
  - `md_sbe_mail_in_receipts.xlsx`: an earlier compiled timeline of daily mail-in receipts. The Rmd doesn't use it.
- **`output/`**: the tables the Rmd writes. The `*_flourish.csv` and `early_voting_time_domain_graphic.csv` files are the exact uploads to Flourish. The other files are fact-check tables.

## Credits

- Graphics and analysis: David Landerman, Capital News Service
- Editor: Adam Marton
- Oct. 26, 2022 mail-in report: Derek Willis, University of Maryland, College Park
- Source: [Maryland State Board of Elections](https://elections.maryland.gov/press_room/index.html)
