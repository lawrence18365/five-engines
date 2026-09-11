# Product proof report
_Generated 2026-09-11 21:47 UTC from live data — last 24h_

## Collection health
- collection runs: **1711 total, 1488 ok, 214 failed** (87% uptime)
- prices collected: **361,218** across **260** events
- snapshots: **6051** over **1410 minutes** of observation
  - DAZN Bet (altenar): 236 events, 106,427 prices
  - BetMGM (entain): 84 events, 120,546 prices
  - bwin (entain): 14 events, 19,561 prices
  - BetRivers (kambi): 179 events, 88,016 prices
  - NEO.bet (neo): 43 events, 6,292 prices
  - Pinnacle (pinnacle): 151 events, 20,464 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **266**
- exact markets priced by 2 or more engines: **14,517**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,330 | 92.9% |
  | betrivers_on vs bwin | 2,326 | 12.7% |
  | betrivers_on vs neobet | 760 | 11.7% |
  | betmgm vs betrivers_on | 7,446 | 10.3% |
  | betmgm vs neobet | 693 | 10.1% |
  | bwin vs neobet | 643 | 9.8% |
  | dazn_bet vs neobet | 712 | 2.2% |
  | bwin vs dazn_bet | 1,932 | 2.1% |
  | betmgm vs dazn_bet | 6,211 | 1.7% |
  | betrivers_on vs dazn_bet | 6,886 | 1.7% |
  | betrivers_on vs pinnacle | 3,718 | 1.4% |
  | betmgm vs pinnacle | 2,386 | 0.8% |
  | bwin vs pinnacle | 776 | 0.8% |
  | dazn_bet vs pinnacle | 2,466 | 0.5% |
  | neobet vs pinnacle | 304 | 0.3% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | spread | 13,207 | 1.88 | 1,165 | 2,750 |
  | total | 13,018 | 1.85 | 1,130 | 2,573 |
  | team_total | 4,302 | 1.34 | 78 | 702 |
  | moneyline | 937 | 1.82 | 114 | 349 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **1411 minutes**, 6053 snapshots
- unbiased (randomised collection order): **1330 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | pinnacle → neo | 30 | 96.7% | polling artifact |
  | kambi → neo | 68 | 95.6% | polling artifact |
  | neo → entain | 79 | 86.1% | polling artifact |
  | entain → pinnacle | 390 | 73.6% | polling artifact |
  | altenar → pinnacle | 287 | 70.0% | polling artifact |
  | neo → kambi | 83 | 69.9% | polling artifact |
  | altenar → neo | 116 | 69.8% | polling artifact |
  | pinnacle → entain | 439 | 68.1% | polling artifact |
  | altenar → entain | 895 | 65.9% | polling artifact |
  | pinnacle → altenar | 125 | 64.8% | weak |
  | entain → neo | 63 | 63.5% | weak |
  | kambi → entain | 279 | 62.7% | polling artifact |
  | entain → altenar | 965 | 61.8% | polling artifact |
  | altenar → kambi | 301 | 57.8% | polling artifact |
  | kambi → pinnacle | 737 | 57.0% | polling artifact |
  | pinnacle → kambi | 462 | 56.7% | polling artifact |
  | neo → pinnacle | 18 | 55.6% | polling artifact |
  | kambi → altenar | 355 | 49.9% | noise |
  | entain → kambi | 503 | 48.9% | polling artifact |
  | neo → altenar | 45 | 44.4% | polling artifact |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **1,137**
- passed clean (zero warnings): **85**
- flagged or withheld: **1,052** (93% of everything found)
- rated high confidence: **8**
- average quoted edge, clean rows: **1.64%**
- average quoted edge, flagged rows: **1.46%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **5,140**
- best price vs the **median** price: **1.82%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.44%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **Bowling Green ** — 21.00 worst vs **29.00** at BetMGM (**+38.1%**)

## Book movement (stale-line detection)
- observed window: **1410 minutes**, 6052 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 9872 | 6432 | 3440 | 34.8% |
  | Pinnacle | pinnacle | 5419 | 3704 | 1715 | 31.6% |
  | BetMGM | entain | 9534 | 6673 | 2861 | 30.0% |
  | bwin | entain | 4369 | 3156 | 1213 | 27.8% |
  | DAZN Bet | altenar | 8395 | 6092 | 2303 | 27.4% |
  | NEO.bet | neo | 1337 | 1191 | 146 | 10.9% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **1,965**
- graded against a closing line so far: **10**
- average CLV: **3.919%** (6 of 10 beat the close)
- average CLV on **clean** rows: **-1.728%**
- average CLV on **flagged** rows: **6.339%**

  If the clean rows do not beat the flagged ones over time, our confidence gate is decoration and we would rather know it.

## Known limits — stated, not hidden
- NFL only so far; other leagues collect but are not tuned.
- Pregame only. No in-play pricing.
- Leader/laggard needs many hours of history; it currently reports nothing rather than guessing.
- Upstream feeds are public sportsbook client APIs. They can change or close without notice; there is no SLA behind them.