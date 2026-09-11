# Product proof report
_Generated 2026-09-11 16:02 UTC from live data — last 24h_

## Collection health
- collection runs: **1454 total, 1241 ok, 212 failed** (85% uptime)
- prices collected: **186,220** across **92** events
- snapshots: **3188** over **1060 minutes** of observation
  - DAZN Bet (altenar): 70 events, 53,135 prices
  - BetMGM (entain): 32 events, 69,918 prices
  - bwin (entain): 14 events, 15,845 prices
  - BetRivers (kambi): 62 events, 35,180 prices
  - NEO.bet (neo): 33 events, 3,675 prices
  - Pinnacle (pinnacle): 32 events, 8,467 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **230**
- exact markets priced by 2 or more engines: **4,977**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,324 | 98.1% |
  | bwin vs neobet | 629 | 11.1% |
  | betrivers_on vs bwin | 2,322 | 10.3% |
  | betmgm vs neobet | 679 | 10.2% |
  | betrivers_on vs neobet | 744 | 9.9% |
  | betmgm vs betrivers_on | 3,046 | 9.5% |
  | betrivers_on vs dazn_bet | 2,148 | 2.4% |
  | dazn_bet vs neobet | 530 | 2.3% |
  | bwin vs dazn_bet | 1,564 | 2.0% |
  | betmgm vs dazn_bet | 2,114 | 1.9% |
  | betrivers_on vs pinnacle | 1,302 | 1.5% |
  | bwin vs pinnacle | 756 | 0.9% |
  | betmgm vs pinnacle | 1,068 | 0.8% |
  | dazn_bet vs pinnacle | 956 | 0.7% |
  | neobet vs pinnacle | 288 | 0.7% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | total | 4,399 | 1.93 | 620 | 692 |
  | spread | 3,978 | 1.94 | 583 | 825 |
  | team_total | 2,932 | 1.27 | 20 | 428 |
  | moneyline | 239 | 1.90 | 30 | 94 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **1064 minutes**, 3189 snapshots
- unbiased (randomised collection order): **983 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | kambi → altenar | 14 | 100.0% | polling artifact |
  | pinnacle → kambi | 94 | 81.9% | polling artifact |
  | altenar → pinnacle | 46 | 80.4% | polling artifact |
  | altenar → neo | 7 | 71.4% | polling artifact |
  | entain → neo | 10 | 70.0% | polling artifact |
  | entain → pinnacle | 187 | 64.7% | polling artifact |
  | kambi → pinnacle | 325 | 61.8% | polling artifact |
  | entain → altenar | 277 | 60.3% | weak |
  | kambi → entain | 80 | 60.0% | polling artifact |
  | altenar → kambi | 25 | 52.0% | polling artifact |
  | neo → pinnacle | 4 | 50.0% | polling artifact |
  | pinnacle → entain | 133 | 48.9% | noise |
  | pinnacle → altenar | 22 | 45.5% | noise |
  | neo → altenar | 7 | 42.9% | polling artifact |
  | entain → kambi | 159 | 39.6% | polling artifact |
  | altenar → entain | 212 | 38.7% | polling artifact |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **447**
- passed clean (zero warnings): **82**
- flagged or withheld: **365** (82% of everything found)
- rated high confidence: **31**
- average quoted edge, clean rows: **0.87%**
- average quoted edge, flagged rows: **2.74%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **2,101**
- best price vs the **median** price: **2.08%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.84%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **Under 5.50** — 1.56 worst vs **3.40** at BetMGM (**+117.9%**)

## Book movement (stale-line detection)
- observed window: **1060 minutes**, 3188 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 3812 | 2286 | 1526 | 40.0% |
  | bwin | entain | 3531 | 2350 | 1181 | 33.4% |
  | BetMGM | entain | 4669 | 3355 | 1314 | 28.1% |
  | Pinnacle | pinnacle | 2556 | 1841 | 715 | 28.0% |
  | NEO.bet | neo | 1094 | 884 | 210 | 19.2% |
  | DAZN Bet | altenar | 2553 | 2136 | 417 | 16.3% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **709**
- graded against a closing line so far: **0**

  Nothing is graded yet — a closing line only exists once an event starts. This section will fill in on its own, and we publish it whichever way it goes.

## Known limits — stated, not hidden
- NFL only so far; other leagues collect but are not tuned.
- Pregame only. No in-play pricing.
- Leader/laggard needs many hours of history; it currently reports nothing rather than guessing.
- Upstream feeds are public sportsbook client APIs. They can change or close without notice; there is no SLA behind them.