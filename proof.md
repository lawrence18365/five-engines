# Product proof report
_Generated 2026-09-10 23:55 UTC from live data — last 24h_

## Collection health
- collection runs: **161 total, 158 ok, 2 failed** (98% uptime)
- prices collected: **58,525** across **94** events
- snapshots: **426** over **98 minutes** of observation
  - DAZN Bet (altenar): 62 events, 15,035 prices
  - BetMGM (entain): 17 events, 22,597 prices
  - BetRivers (kambi): 53 events, 16,342 prices
  - NEO.bet (neo): 30 events, 2,008 prices
  - Pinnacle (pinnacle): 18 events, 2,543 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **222**
- exact markets priced by 2 or more engines: **3,895**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs neobet | 674 | 12.3% |
  | betmgm vs betrivers_on | 2,559 | 11.0% |
  | betrivers_on vs neobet | 740 | 8.1% |
  | betmgm vs dazn_bet | 1,725 | 2.6% |
  | betrivers_on vs dazn_bet | 1,778 | 1.9% |
  | dazn_bet vs neobet | 498 | 1.8% |
  | betrivers_on vs pinnacle | 850 | 1.5% |
  | betmgm vs pinnacle | 832 | 1.1% |
  | dazn_bet vs pinnacle | 706 | 0.4% |
  | neobet vs pinnacle | 280 | 0.4% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | total | 3,624 | 1.83 | 376 | 544 |
  | spread | 3,396 | 2.04 | 580 | 603 |
  | team_total | 2,642 | 1.25 | 18 | 310 |
  | moneyline | 176 | 2.06 | 30 | 64 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines
- observed window: **98 minutes**, 427 snapshots
- no relationship yet clears the sample and significance bar
- relationships tested: 16, rejected as noise or insufficient sample: 11

  Scored on whether the follower moves the SAME DIRECTION, against a 50% baseline with an exact binomial test, and requiring at least 20 paired moves. Counting who moved first would have given the opposite answer: Altenar reprices far more often than Kambi and a naive count credited it with 87% of all leads, but when Altenar moved first Kambi followed the same way only 40% of the time.

  **Caveat:** lead/lag is NOT published yet: every snapshot so far was collected in a FIXED book order, which makes whichever book is polled first appear to lead the others by exactly the polling gap. Collection order was randomised 16 minutes ago; results become publishable after 60 minutes of unbiased data..

## What the gate rejected
- opportunities detected: **347**
- passed clean (zero warnings): **76**
- flagged or withheld: **271** (78% of everything found)
- rated high confidence: **39**
- average quoted edge, clean rows: **1.01%**
- average quoted edge, flagged rows: **3.75%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines: **2,000**
- median improvement from taking the best price: **4.9%**
- largest: **Under 9.50** — 1.54 worst vs **3.40** at BetMGM (**+120.8%**)

## Book movement (stale-line detection)
- observed window: **98 minutes**, 426 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 1185 | 408 | 777 | 65.6% |
  | NEO.bet | neo | 314 | 158 | 156 | 49.7% |
  | Pinnacle | pinnacle | 613 | 331 | 282 | 46.0% |
  | BetMGM | entain | 1541 | 923 | 618 | 40.1% |
  | DAZN Bet | altenar | 974 | 638 | 336 | 34.5% |

## Known limits — stated, not hidden
- NFL only so far; other leagues collect but are not tuned.
- Pregame only. No in-play pricing.
- Leader/laggard needs many hours of history; it currently reports nothing rather than guessing.
- Upstream feeds are public sportsbook client APIs. They can change or close without notice; there is no SLA behind them.