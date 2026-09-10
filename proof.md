# Product proof report
_Generated 2026-09-10 23:40 UTC from live data — last 24h_

## Collection health
- collection runs: **136 total, 133 ok, 2 failed** (98% uptime)
- prices collected: **55,222** across **93** events
- snapshots: **375** over **83 minutes** of observation
  - DAZN Bet (altenar): 61 events, 14,163 prices
  - BetMGM (entain): 17 events, 20,574 prices
  - BetRivers (kambi): 52 events, 16,062 prices
  - NEO.bet (neo): 30 events, 1,912 prices
  - Pinnacle (pinnacle): 18 events, 2,511 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **222**
- exact markets priced by 2 or more engines: **3,891**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs neobet | 672 | 11.5% |
  | betmgm vs betrivers_on | 2,557 | 11.2% |
  | betrivers_on vs neobet | 740 | 8.5% |
  | betmgm vs dazn_bet | 1,725 | 2.9% |
  | betrivers_on vs dazn_bet | 1,776 | 2.1% |
  | dazn_bet vs neobet | 498 | 1.6% |
  | betrivers_on vs pinnacle | 850 | 1.5% |
  | betmgm vs pinnacle | 832 | 1.2% |
  | dazn_bet vs pinnacle | 706 | 0.7% |
  | neobet vs pinnacle | 280 | 0.4% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | total | 3,616 | 1.83 | 376 | 542 |
  | spread | 3,394 | 2.04 | 580 | 605 |
  | team_total | 2,640 | 1.25 | 18 | 308 |
  | moneyline | 174 | 2.07 | 30 | 64 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines
- observed window: **83 minutes**, 376 snapshots
- no relationship yet clears the sample and significance bar
- relationships tested: 16, rejected as noise or insufficient sample: 10

  Scored on whether the follower moves the SAME DIRECTION, against a 50% baseline with an exact binomial test, and requiring at least 20 paired moves. Counting who moved first would have given the opposite answer: Altenar reprices far more often than Kambi and a naive count credited it with 87% of all leads, but when Altenar moved first Kambi followed the same way only 40% of the time.

  **Caveat:** lead/lag is NOT published yet: every snapshot so far was collected in a FIXED book order, which makes whichever book is polled first appear to lead the others by exactly the polling gap. Collection order was randomised 1 minutes ago; results become publishable after 60 minutes of unbiased data..

## What the gate rejected
- opportunities detected: **342**
- passed clean (zero warnings): **79**
- flagged or withheld: **263** (77% of everything found)
- rated high confidence: **43**
- average quoted edge, clean rows: **1.00%**
- average quoted edge, flagged rows: **2.96%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines: **2,000**
- median improvement from taking the best price: **4.9%**
- largest: **Under 8.50** — 1.82 worst vs **2.90** at BetMGM (**+59.3%**)

## Book movement (stale-line detection)
- observed window: **83 minutes**, 375 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 1042 | 408 | 634 | 60.8% |
  | NEO.bet | neo | 243 | 97 | 146 | 60.1% |
  | BetMGM | entain | 1289 | 673 | 616 | 47.8% |
  | Pinnacle | pinnacle | 552 | 331 | 221 | 40.0% |
  | DAZN Bet | altenar | 823 | 504 | 319 | 38.8% |

## Known limits — stated, not hidden
- NFL only so far; other leagues collect but are not tuned.
- Pregame only. No in-play pricing.
- Leader/laggard needs many hours of history; it currently reports nothing rather than guessing.
- Upstream feeds are public sportsbook client APIs. They can change or close without notice; there is no SLA behind them.