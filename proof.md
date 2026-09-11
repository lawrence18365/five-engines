# Product proof report
_Generated 2026-09-11 00:37 UTC from live data — last 24h_

## Collection health
- collection runs: **222 total, 219 ok, 2 failed** (99% uptime)
- prices collected: **67,042** across **95** events
- snapshots: **551** over **139 minutes** of observation
  - DAZN Bet (altenar): 63 events, 17,293 prices
  - BetMGM (entain): 17 events, 26,821 prices
  - BetRivers (kambi): 53 events, 17,354 prices
  - NEO.bet (neo): 30 events, 2,113 prices
  - Pinnacle (pinnacle): 27 events, 3,461 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **222**
- exact markets priced by 2 or more engines: **3,993**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs neobet | 674 | 12.5% |
  | betmgm vs betrivers_on | 2,559 | 10.4% |
  | betrivers_on vs neobet | 740 | 8.2% |
  | betmgm vs dazn_bet | 1,725 | 2.6% |
  | betrivers_on vs dazn_bet | 1,778 | 2.1% |
  | dazn_bet vs neobet | 498 | 1.8% |
  | betrivers_on vs pinnacle | 874 | 1.7% |
  | betmgm vs pinnacle | 832 | 0.8% |
  | dazn_bet vs pinnacle | 790 | 0.6% |
  | neobet vs pinnacle | 280 | 0.4% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | total | 3,806 | 1.81 | 376 | 616 |
  | spread | 3,648 | 1.97 | 580 | 613 |
  | team_total | 2,794 | 1.24 | 18 | 308 |
  | moneyline | 213 | 1.91 | 30 | 72 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and so far NOT supported
- observed window: **140 minutes**, 554 snapshots
- unbiased (randomised collection order): **58 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass. Measured on that unbiased data only, the previously 'verified' relationships have not reappeared, and what remains sits at chance:

  | pair | paired moves | same direction |
  |---|---:|---:|
  | pinnacle → entain | 70 | 65.7% |
  | entain → altenar | 325 | 53.8% |
  | entain → pinnacle | 76 | 50.0% |
  | pinnacle → altenar | 16 | 50.0% |
  | altenar → entain | 341 | 45.5% |
  | altenar → pinnacle | 20 | 20.0% |

Nothing here is published as a signal, and nothing will be until it survives measurement on unbiased data. We are reporting a feature that did not work, because a product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **344**
- passed clean (zero warnings): **71**
- flagged or withheld: **273** (79% of everything found)
- rated high confidence: **41**
- average quoted edge, clean rows: **1.07%**
- average quoted edge, flagged rows: **3.71%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **5 minutes** of the others: **1,953**
- best price vs the **median** price: **2.00%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.76%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **Baltimore Ravens -14.00** — 4.00 worst vs **5.40** at BetRivers (**+35.0%**)

## Book movement (stale-line detection)
- observed window: **139 minutes**, 551 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 1402 | 603 | 799 | 57.0% |
  | NEO.bet | neo | 401 | 193 | 208 | 51.9% |
  | Pinnacle | pinnacle | 731 | 367 | 364 | 49.8% |
  | BetMGM | entain | 1782 | 1019 | 763 | 42.8% |
  | DAZN Bet | altenar | 1281 | 953 | 328 | 25.6% |

## Known limits — stated, not hidden
- NFL only so far; other leagues collect but are not tuned.
- Pregame only. No in-play pricing.
- Leader/laggard needs many hours of history; it currently reports nothing rather than guessing.
- Upstream feeds are public sportsbook client APIs. They can change or close without notice; there is no SLA behind them.