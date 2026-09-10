# Product proof report
_Generated 2026-09-10 23:31 UTC from live data — last 24h_

## Collection health
- collection runs: **119 total, 116 ok, 2 failed** (97% uptime)
- prices collected: **52,708** across **93** events
- snapshots: **337** over **74 minutes** of observation
  - DAZN Bet (altenar): 61 events, 13,502 prices
  - BetMGM (entain): 17 events, 19,537 prices
  - BetRivers (kambi): 50 events, 15,394 prices
  - NEO.bet (neo): 30 events, 1,834 prices
  - Pinnacle (pinnacle): 18 events, 2,441 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **218**
- exact markets priced by 2 or more engines: **3,885**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs neobet | 666 | 11.9% |
  | betmgm vs betrivers_on | 2,553 | 10.4% |
  | betrivers_on vs neobet | 734 | 8.7% |
  | betmgm vs dazn_bet | 1,721 | 3.0% |
  | betrivers_on vs dazn_bet | 1,772 | 2.0% |
  | betrivers_on vs pinnacle | 850 | 1.5% |
  | dazn_bet vs neobet | 494 | 1.4% |
  | betmgm vs pinnacle | 832 | 1.0% |
  | dazn_bet vs pinnacle | 706 | 0.8% |
  | neobet vs pinnacle | 276 | 0.4% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | total | 3,610 | 1.82 | 376 | 540 |
  | spread | 3,390 | 2.04 | 578 | 603 |
  | team_total | 2,638 | 1.25 | 18 | 310 |
  | moneyline | 170 | 2.09 | 30 | 64 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines
- observed window: **74 minutes**, 337 snapshots
- **verified:** pinnacle -> entain (78.9% same direction over 57 moves, p=1e-05, ~85s lag)
- **verified:** kambi -> altenar (77.3% same direction over 44 moves, p=0.00019, ~514s lag)
- relationships tested: 13, rejected as noise or insufficient sample: 11

  Scored on whether the follower moves the SAME DIRECTION, against a 50% baseline with an exact binomial test, and requiring at least 20 paired moves. Counting who moved first would have given the opposite answer: Altenar reprices far more often than Kambi and a naive count credited it with 87% of all leads, but when Altenar moved first Kambi followed the same way only 40% of the time.

  **Caveat:** only 74 minutes of history exists - lead/lag relationships need hours before they are dependable.

## What the gate rejected
- opportunities detected: **345**
- passed clean (zero warnings): **81**
- flagged or withheld: **264** (77% of everything found)
- rated high confidence: **42**
- average quoted edge, clean rows: **0.92%**
- average quoted edge, flagged rows: **2.66%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines: **2,000**
- median improvement from taking the best price: **4.8%**
- largest: **Under 6.50** — 1.70 worst vs **2.64** at Pinnacle (**+55.3%**)

## Book movement (stale-line detection)
- observed window: **74 minutes**, 337 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | NEO.bet | neo | 197 | 60 | 137 | 69.5% |
  | BetRivers | kambi | 858 | 263 | 595 | 69.3% |
  | BetMGM | entain | 981 | 389 | 592 | 60.3% |
  | Pinnacle | pinnacle | 502 | 330 | 172 | 34.3% |
  | DAZN Bet | altenar | 685 | 473 | 212 | 30.9% |

## Known limits — stated, not hidden
- NFL only so far; other leagues collect but are not tuned.
- Pregame only. No in-play pricing.
- Leader/laggard needs many hours of history; it currently reports nothing rather than guessing.
- Upstream feeds are public sportsbook client APIs. They can change or close without notice; there is no SLA behind them.