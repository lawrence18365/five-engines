# Product proof report
_Generated 2026-09-11 00:05 UTC from live data — last 24h_

## Collection health
- collection runs: **180 total, 177 ok, 2 failed** (98% uptime)
- prices collected: **60,637** across **94** events
- snapshots: **465** over **108 minutes** of observation
  - DAZN Bet (altenar): 62 events, 15,795 prices
  - BetMGM (entain): 17 events, 23,696 prices
  - BetRivers (kambi): 53 events, 16,398 prices
  - NEO.bet (neo): 30 events, 2,064 prices
  - Pinnacle (pinnacle): 19 events, 2,684 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **222**
- exact markets priced by 2 or more engines: **3,909**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs neobet | 674 | 12.0% |
  | betmgm vs betrivers_on | 2,559 | 11.0% |
  | betrivers_on vs neobet | 740 | 8.2% |
  | betmgm vs dazn_bet | 1,725 | 2.8% |
  | dazn_bet vs neobet | 498 | 2.0% |
  | betrivers_on vs dazn_bet | 1,778 | 1.9% |
  | betrivers_on vs pinnacle | 850 | 1.5% |
  | betmgm vs pinnacle | 832 | 1.1% |
  | dazn_bet vs pinnacle | 720 | 0.6% |
  | neobet vs pinnacle | 280 | 0.4% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | total | 3,636 | 1.83 | 376 | 558 |
  | spread | 3,422 | 2.03 | 580 | 603 |
  | team_total | 2,658 | 1.25 | 18 | 310 |
  | moneyline | 181 | 2.03 | 30 | 64 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and so far NOT supported
- observed window: **108 minutes**, 466 snapshots
- unbiased (randomised collection order): **27 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass. Measured on that unbiased data only, the previously 'verified' relationships have not reappeared, and what remains sits at chance:

  | pair | paired moves | same direction |
  |---|---:|---:|
  | entain → altenar | 70 | 52.9% |
  | altenar → entain | 24 | 33.3% |

Nothing here is published as a signal, and nothing will be until it survives measurement on unbiased data. We are reporting a feature that did not work, because a product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **348**
- passed clean (zero warnings): **77**
- flagged or withheld: **271** (78% of everything found)
- rated high confidence: **39**
- average quoted edge, clean rows: **0.99%**
- average quoted edge, flagged rows: **4.25%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines: **2,000**
- median improvement from taking the best price: **4.9%**
- largest: **Under 8.50** — 1.82 worst vs **4.10** at BetMGM (**+125.3%**)

## Book movement (stale-line detection)
- observed window: **108 minutes**, 465 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 1206 | 408 | 798 | 66.2% |
  | Pinnacle | pinnacle | 622 | 335 | 287 | 46.1% |
  | NEO.bet | neo | 332 | 190 | 142 | 42.8% |
  | BetMGM | entain | 1600 | 978 | 622 | 38.9% |
  | DAZN Bet | altenar | 1002 | 690 | 312 | 31.1% |

## Known limits — stated, not hidden
- NFL only so far; other leagues collect but are not tuned.
- Pregame only. No in-play pricing.
- Leader/laggard needs many hours of history; it currently reports nothing rather than guessing.
- Upstream feeds are public sportsbook client APIs. They can change or close without notice; there is no SLA behind them.