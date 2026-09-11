# Product proof report
_Generated 2026-09-11 17:25 UTC from live data — last 24h_

## Collection health
- collection runs: **1513 total, 1299 ok, 212 failed** (86% uptime)
- prices collected: **206,217** across **92** events
- snapshots: **3654** over **1145 minutes** of observation
  - DAZN Bet (altenar): 70 events, 59,157 prices
  - BetMGM (entain): 32 events, 77,282 prices
  - bwin (entain): 14 events, 17,881 prices
  - BetRivers (kambi): 62 events, 37,458 prices
  - NEO.bet (neo): 33 events, 4,030 prices
  - Pinnacle (pinnacle): 32 events, 10,559 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **232**
- exact markets priced by 2 or more engines: **5,064**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,329 | 100.0% |
  | betrivers_on vs bwin | 2,325 | 10.1% |
  | betrivers_on vs neobet | 744 | 9.8% |
  | betmgm vs betrivers_on | 3,050 | 9.4% |
  | bwin vs neobet | 631 | 8.7% |
  | betmgm vs neobet | 681 | 8.4% |
  | dazn_bet vs neobet | 574 | 2.6% |
  | betmgm vs dazn_bet | 2,262 | 2.3% |
  | bwin vs dazn_bet | 1,711 | 2.2% |
  | betrivers_on vs dazn_bet | 2,334 | 2.2% |
  | betrivers_on vs pinnacle | 1,314 | 1.9% |
  | betmgm vs pinnacle | 1,080 | 1.2% |
  | bwin vs pinnacle | 764 | 0.9% |
  | dazn_bet vs pinnacle | 972 | 0.8% |
  | neobet vs pinnacle | 288 | 0.3% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | total | 4,505 | 1.95 | 634 | 608 |
  | spread | 4,012 | 1.95 | 595 | 839 |
  | team_total | 2,938 | 1.27 | 20 | 430 |
  | moneyline | 239 | 1.90 | 30 | 94 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **1146 minutes**, 3715 snapshots
- unbiased (randomised collection order): **1066 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | pinnacle → neo | 8 | 100.0% | insufficient sample |
  | neo → pinnacle | 8 | 75.0% | polling artifact |
  | altenar → pinnacle | 50 | 74.0% | polling artifact |
  | altenar → kambi | 43 | 72.1% | polling artifact |
  | pinnacle → kambi | 177 | 70.1% | polling artifact |
  | entain → pinnacle | 275 | 69.5% | polling artifact |
  | neo → entain | 31 | 61.3% | polling artifact |
  | kambi → pinnacle | 367 | 61.0% | polling artifact |
  | entain → neo | 15 | 60.0% | polling artifact |
  | entain → altenar | 347 | 59.1% | weak |
  | pinnacle → entain | 222 | 56.8% | weak |
  | kambi → altenar | 64 | 56.3% | polling artifact |
  | kambi → entain | 100 | 51.0% | polling artifact |
  | altenar → neo | 21 | 47.6% | polling artifact |
  | entain → kambi | 187 | 45.5% | polling artifact |
  | neo → altenar | 7 | 42.9% | polling artifact |
  | altenar → entain | 361 | 40.2% | polling artifact |
  | pinnacle → altenar | 63 | 36.5% | polling artifact |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **571**
- passed clean (zero warnings): **99**
- flagged or withheld: **472** (83% of everything found)
- rated high confidence: **22**
- average quoted edge, clean rows: **1.49%**
- average quoted edge, flagged rows: **3.30%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **2,239**
- best price vs the **median** price: **2.11%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.90%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **Under 5.50** — 1.56 worst vs **3.40** at BetMGM (**+117.9%**)

## Book movement (stale-line detection)
- observed window: **1145 minutes**, 3655 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 3911 | 2303 | 1608 | 41.1% |
  | bwin | entain | 3855 | 2816 | 1039 | 27.0% |
  | Pinnacle | pinnacle | 2643 | 1940 | 703 | 26.6% |
  | BetMGM | entain | 5014 | 3867 | 1147 | 22.9% |
  | DAZN Bet | altenar | 2728 | 2215 | 513 | 18.8% |
  | NEO.bet | neo | 1180 | 980 | 200 | 16.9% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **899**
- graded against a closing line so far: **0**

  Nothing is graded yet — a closing line only exists once an event starts. This section will fill in on its own, and we publish it whichever way it goes.

## Known limits — stated, not hidden
- NFL only so far; other leagues collect but are not tuned.
- Pregame only. No in-play pricing.
- Leader/laggard needs many hours of history; it currently reports nothing rather than guessing.
- Upstream feeds are public sportsbook client APIs. They can change or close without notice; there is no SLA behind them.