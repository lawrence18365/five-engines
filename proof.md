# Product proof report
_Generated 2026-09-11 17:40 UTC from live data — last 24h_

## Collection health
- collection runs: **1531 total, 1317 ok, 212 failed** (86% uptime)
- prices collected: **213,743** across **92** events
- snapshots: **3796** over **1161 minutes** of observation
  - DAZN Bet (altenar): 70 events, 61,200 prices
  - BetMGM (entain): 32 events, 79,236 prices
  - bwin (entain): 14 events, 17,782 prices
  - BetRivers (kambi): 62 events, 40,513 prices
  - NEO.bet (neo): 33 events, 4,202 prices
  - Pinnacle (pinnacle): 32 events, 10,810 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **232**
- exact markets priced by 2 or more engines: **5,070**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,329 | 91.5% |
  | betrivers_on vs bwin | 2,325 | 10.4% |
  | bwin vs neobet | 631 | 9.7% |
  | betmgm vs betrivers_on | 3,052 | 9.7% |
  | betrivers_on vs neobet | 746 | 9.0% |
  | betmgm vs neobet | 683 | 8.6% |
  | dazn_bet vs neobet | 574 | 2.8% |
  | betrivers_on vs dazn_bet | 2,336 | 2.3% |
  | bwin vs dazn_bet | 1,711 | 2.3% |
  | betmgm vs dazn_bet | 2,264 | 2.2% |
  | betrivers_on vs pinnacle | 1,314 | 1.6% |
  | betmgm vs pinnacle | 1,080 | 1.5% |
  | bwin vs pinnacle | 764 | 1.2% |
  | dazn_bet vs pinnacle | 972 | 0.9% |
  | neobet vs pinnacle | 288 | 0.7% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | total | 4,507 | 1.95 | 634 | 608 |
  | spread | 4,012 | 1.95 | 597 | 841 |
  | team_total | 2,940 | 1.27 | 20 | 428 |
  | moneyline | 239 | 1.90 | 30 | 94 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **1161 minutes**, 3796 snapshots
- unbiased (randomised collection order): **1082 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | pinnacle → neo | 20 | 100.0% | noise |
  | kambi → neo | 8 | 100.0% | polling artifact |
  | neo → entain | 47 | 97.9% | polling artifact |
  | altenar → neo | 51 | 84.3% | polling artifact |
  | altenar → kambi | 49 | 75.5% | polling artifact |
  | entain → pinnacle | 263 | 71.9% | polling artifact |
  | pinnacle → kambi | 148 | 70.9% | polling artifact |
  | neo → pinnacle | 6 | 66.7% | polling artifact |
  | kambi → altenar | 60 | 66.7% | polling artifact |
  | entain → altenar | 429 | 61.5% | weak |
  | pinnacle → entain | 242 | 59.9% | weak |
  | kambi → pinnacle | 422 | 57.1% | polling artifact |
  | pinnacle → altenar | 51 | 56.9% | noise |
  | altenar → pinnacle | 133 | 55.6% | polling artifact |
  | kambi → entain | 99 | 53.5% | polling artifact |
  | altenar → entain | 336 | 49.7% | polling artifact |
  | entain → kambi | 190 | 47.9% | polling artifact |
  | entain → neo | 41 | 43.9% | polling artifact |
  | neo → altenar | 24 | 41.7% | polling artifact |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **556**
- passed clean (zero warnings): **86**
- flagged or withheld: **470** (85% of everything found)
- rated high confidence: **27**
- average quoted edge, clean rows: **1.02%**
- average quoted edge, flagged rows: **3.12%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **2,239**
- best price vs the **median** price: **2.11%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.84%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **Under 5.50** — 1.56 worst vs **3.40** at BetMGM (**+117.9%**)

## Book movement (stale-line detection)
- observed window: **1161 minutes**, 3796 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 4100 | 2803 | 1297 | 31.6% |
  | Pinnacle | pinnacle | 2675 | 1950 | 725 | 27.1% |
  | bwin | entain | 4027 | 2950 | 1077 | 26.7% |
  | BetMGM | entain | 5188 | 4001 | 1187 | 22.9% |
  | DAZN Bet | altenar | 2764 | 2245 | 519 | 18.8% |
  | NEO.bet | neo | 1199 | 1004 | 195 | 16.3% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **919**
- graded against a closing line so far: **0**

  Nothing is graded yet — a closing line only exists once an event starts. This section will fill in on its own, and we publish it whichever way it goes.

## Known limits — stated, not hidden
- NFL only so far; other leagues collect but are not tuned.
- Pregame only. No in-play pricing.
- Leader/laggard needs many hours of history; it currently reports nothing rather than guessing.
- Upstream feeds are public sportsbook client APIs. They can change or close without notice; there is no SLA behind them.