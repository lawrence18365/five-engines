# Product proof report
_Generated 2026-09-11 13:27 UTC from live data — last 24h_

## Collection health
- collection runs: **1380 total, 1166 ok, 212 failed** (84% uptime)
- prices collected: **153,332** across **91** events
- snapshots: **2553** over **908 minutes** of observation
  - DAZN Bet (altenar): 69 events, 45,482 prices
  - BetMGM (entain): 32 events, 54,165 prices
  - bwin (entain): 14 events, 14,998 prices
  - BetRivers (kambi): 61 events, 30,347 prices
  - NEO.bet (neo): 33 events, 3,141 prices
  - Pinnacle (pinnacle): 32 events, 5,224 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **230**
- exact markets priced by 2 or more engines: **4,928**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,322 | 100.0% |
  | betrivers_on vs bwin | 2,320 | 10.6% |
  | bwin vs neobet | 627 | 10.5% |
  | betmgm vs neobet | 679 | 10.0% |
  | betmgm vs betrivers_on | 3,018 | 9.8% |
  | betrivers_on vs neobet | 744 | 9.4% |
  | betrivers_on vs dazn_bet | 2,124 | 2.6% |
  | dazn_bet vs neobet | 530 | 2.5% |
  | betmgm vs dazn_bet | 2,106 | 2.4% |
  | bwin vs dazn_bet | 1,562 | 2.2% |
  | betrivers_on vs pinnacle | 1,288 | 1.8% |
  | betmgm vs pinnacle | 1,062 | 1.4% |
  | dazn_bet vs pinnacle | 950 | 1.2% |
  | bwin vs pinnacle | 756 | 1.1% |
  | neobet vs pinnacle | 288 | 0.7% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | total | 4,364 | 1.93 | 606 | 686 |
  | spread | 3,966 | 1.95 | 583 | 821 |
  | team_total | 2,924 | 1.27 | 18 | 420 |
  | moneyline | 237 | 1.91 | 30 | 94 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **909 minutes**, 2569 snapshots
- unbiased (randomised collection order): **828 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | kambi → pinnacle | 44 | 95.5% | polling artifact |
  | altenar → kambi | 13 | 76.9% | polling artifact |
  | entain → neo | 7 | 71.4% | polling artifact |
  | entain → altenar | 242 | 55.4% | weak |
  | entain → pinnacle | 62 | 53.2% | polling artifact |
  | neo → pinnacle | 4 | 50.0% | polling artifact |
  | pinnacle → altenar | 15 | 46.7% | insufficient sample |
  | pinnacle → entain | 51 | 43.1% | noise |
  | altenar → entain | 201 | 35.3% | polling artifact |
  | altenar → pinnacle | 9 | 22.2% | polling artifact |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **658**
- passed clean (zero warnings): **116**
- flagged or withheld: **542** (82% of everything found)
- rated high confidence: **45**
- average quoted edge, clean rows: **0.66%**
- average quoted edge, flagged rows: **4.76%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **10 minutes** of the others: **2,087**
- best price vs the **median** price: **2.14%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **5.00%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **Baltimore Ravens -14.00** — 4.00 worst vs **5.40** at BetRivers (**+35.0%**)

## Book movement (stale-line detection)
- observed window: **908 minutes**, 2554 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 3383 | 1659 | 1724 | 51.0% |
  | Pinnacle | pinnacle | 2171 | 1359 | 812 | 37.4% |
  | BetMGM | entain | 4222 | 2839 | 1383 | 32.8% |
  | bwin | entain | 3249 | 2247 | 1002 | 30.8% |
  | NEO.bet | neo | 1044 | 827 | 217 | 20.8% |
  | DAZN Bet | altenar | 2454 | 2055 | 399 | 16.3% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **606**
- graded against a closing line so far: **0**

  Nothing is graded yet — a closing line only exists once an event starts. This section will fill in on its own, and we publish it whichever way it goes.

## Known limits — stated, not hidden
- NFL only so far; other leagues collect but are not tuned.
- Pregame only. No in-play pricing.
- Leader/laggard needs many hours of history; it currently reports nothing rather than guessing.
- Upstream feeds are public sportsbook client APIs. They can change or close without notice; there is no SLA behind them.