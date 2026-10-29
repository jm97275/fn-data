# Auction sale archive

Source: USDA AMS Market News, livestock auction reports (MARS API), https://www.ams.usda.gov/market-news

One row per market sale, cattle class and weight bracket, collected by the
Farmer's Navigator daily-prices workflow from auctions.json. One file per
sale month (YYYY-MM.csv). Prices are $/cwt.

Columns:
- sale_date, state, slug (MARS report id), market
- class: feeder_steer, feeder_heifer or slaughter_cow
- bracket: weight in lbs (feeders); blank for slaughter cows
- head, avg, low, high: head count and average/low/high price for the bracket
  (slaughter cows: simple average of the reported cow lots; no low/high)
- receipts: total head reported for the sale
- grade_used, grade_fallback: feeder grade the prices come from; blank for
  slaughter cows and in rows captured before these fields were added
  (2026-10-19)
- method: largest_lot = captured before 2026-10-10T15:27:56Z, when each
  bracket took the single largest lot of any grade; head_weighted =
  head-weighted average of Medium and Large 1 lots (or the market's best grade
  when grade_fallback is true)
- fetched_at: first snapshot that carried these values (UTC)

Coverage: each run keeps a market's latest sale from the last 14 days, twice a
day Monday to Saturday, so a market that sells twice between runs can miss a
sale.
