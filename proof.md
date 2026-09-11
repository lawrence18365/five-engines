# Product proof report
_Generated 2026-09-11 18:03 UTC from live data — last 24h_

## Collection health
- collection runs: **1548 total, 1332 ok, 212 failed** (86% uptime)
- prices collected: **218,208** across **101** events
- snapshots: **3900** over **1186 minutes** of observation
  - DAZN Bet (altenar): 79 events, 62,749 prices
  - BetMGM (entain): 32 events, 80,801 prices
  - bwin (entain): 14 events, 17,782 prices
  - BetRivers (kambi): 62 events, 41,481 prices
  - NEO.bet (neo): 33 events, 4,406 prices
  - Pinnacle (pinnacle): 32 events, 10,989 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **232**
- exact markets priced by 2 or more engines: **5,070**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,329 | 91.5% |
  | bwin vs neobet | 631 | 9.7% |
  | betmgm vs betrivers_on | 3,052 | 9.7% |
  | betrivers_on vs bwin | 2,325 | 9.6% |
  | betmgm vs neobet | 683 | 8.8% |
  | betrivers_on vs neobet | 746 | 8.7% |
  | betrivers_on vs dazn_bet | 2,336 | 2.7% |
  | betmgm vs dazn_bet | 2,264 | 2.2% |
  | bwin vs dazn_bet | 1,711 | 2.2% |
  | dazn_bet vs neobet | 574 | 2.1% |
  | betrivers_on vs pinnacle | 1,314 | 1.8% |
  | betmgm vs pinnacle | 1,080 | 1.4% |
  | bwin vs pinnacle | 764 | 1.2% |
  | dazn_bet vs pinnacle | 972 | 1.0% |
  | neobet vs pinnacle | 288 | 0.7% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | total | 4,705 | 1.91 | 634 | 608 |
  | spread | 4,014 | 1.95 | 597 | 841 |
  | team_total | 2,940 | 1.28 | 20 | 426 |
  | moneyline | 239 | 1.90 | 30 | 94 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **1186 minutes**, 3900 snapshots
- unbiased (randomised collection order): **1104 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | pinnacle → neo | 21 | 100.0% | noise |
  | kambi → neo | 33 | 90.9% | polling artifact |
  | neo → entain | 77 | 87.0% | polling artifact |
  | altenar → neo | 82 | 78.0% | polling artifact |
  | entain → pinnacle | 299 | 73.2% | polling artifact |
  | pinnacle → kambi | 185 | 71.9% | polling artifact |
  | neo → pinnacle | 13 | 69.2% | polling artifact |
  | kambi → altenar | 105 | 67.6% | noise |
  | altenar → kambi | 93 | 65.6% | polling artifact |
  | entain → altenar | 481 | 62.6% | weak |
  | entain → neo | 59 | 61.0% | weak |
  | kambi → entain | 177 | 59.9% | polling artifact |
  | pinnacle → entain | 253 | 58.5% | weak |
  | kambi → pinnacle | 436 | 56.0% | polling artifact |
  | altenar → pinnacle | 136 | 55.9% | polling artifact |
  | pinnacle → altenar | 57 | 54.4% | noise |
  | neo → kambi | 44 | 50.0% | polling artifact |
  | altenar → entain | 357 | 49.9% | polling artifact |
  | entain → kambi | 264 | 49.2% | polling artifact |
  | neo → altenar | 24 | 41.7% | polling artifact |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **555**
- passed clean (zero warnings): **82**
- flagged or withheld: **473** (85% of everything found)
- rated high confidence: **16**
- average quoted edge, clean rows: **1.04%**
- average quoted edge, flagged rows: **3.07%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **2,237**
- best price vs the **median** price: **2.08%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.80%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **Under 5.50** — 1.56 worst vs **3.40** at BetMGM (**+117.9%**)

## Book movement (stale-line detection)
- observed window: **1186 minutes**, 3900 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 4117 | 2850 | 1267 | 30.8% |
  | Pinnacle | pinnacle | 2676 | 1951 | 725 | 27.1% |
  | bwin | entain | 4038 | 2963 | 1075 | 26.6% |
  | BetMGM | entain | 5204 | 4038 | 1166 | 22.4% |
  | DAZN Bet | altenar | 2767 | 2253 | 514 | 18.6% |
  | NEO.bet | neo | 1208 | 1014 | 194 | 16.1% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **943**
- graded against a closing line so far: **0**

  Nothing is graded yet — a closing line only exists once an event starts. This section will fill in on its own, and we publish it whichever way it goes.

## Known limits — stated, not hidden
- NFL only so far; other leagues collect but are not tuned.
- Pregame only. No in-play pricing.
- Leader/laggard needs many hours of history; it currently reports nothing rather than guessing.
- Upstream feeds are public sportsbook client APIs. They can change or close without notice; there is no SLA behind them.