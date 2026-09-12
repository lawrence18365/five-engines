# Product proof report
_Generated 2026-09-12 03:52 UTC from live data — last 24h_

## Collection health
- collection runs: **1444 total, 1260 ok, 169 failed** (87% uptime)
- prices collected: **396,921** across **230** events
- snapshots: **7491** over **1439 minutes** of observation
  - DAZN Bet (altenar): 239 events, 138,361 prices
  - BetMGM (entain): 85 events, 171,658 prices
  - bwin (entain): 14 events, 24,554 prices
  - BetRivers (kambi): 192 events, 110,036 prices
  - NEO.bet (neo): 46 events, 7,570 prices
  - Pinnacle (pinnacle): 162 events, 28,954 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **266**
- exact markets priced by 2 or more engines: **15,900**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,340 | 94.1% |
  | betrivers_on vs bwin | 2,338 | 12.0% |
  | bwin vs neobet | 644 | 10.9% |
  | betrivers_on vs neobet | 762 | 10.5% |
  | betmgm vs neobet | 693 | 10.4% |
  | betmgm vs betrivers_on | 7,591 | 10.2% |
  | dazn_bet vs neobet | 718 | 2.2% |
  | bwin vs dazn_bet | 1,956 | 2.1% |
  | betrivers_on vs dazn_bet | 7,224 | 1.8% |
  | betmgm vs dazn_bet | 6,713 | 1.6% |
  | betrivers_on vs pinnacle | 3,981 | 1.6% |
  | bwin vs pinnacle | 776 | 0.9% |
  | dazn_bet vs pinnacle | 2,696 | 0.9% |
  | betmgm vs pinnacle | 2,420 | 0.7% |
  | neobet vs pinnacle | 304 | 0.3% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | spread | 14,298 | 1.85 | 1,185 | 2,948 |
  | total | 13,678 | 1.88 | 1,140 | 3,172 |
  | team_total | 4,662 | 1.35 | 84 | 810 |
  | moneyline | 967 | 1.82 | 114 | 369 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **1436 minutes**, 7498 snapshots
- unbiased (randomised collection order): **1694 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | kambi → neo | 12 | 100.0% | polling artifact |
  | pinnacle → neo | 14 | 92.9% | polling artifact |
  | entain → pinnacle | 70 | 84.3% | polling artifact |
  | neo → entain | 30 | 80.0% | polling artifact |
  | kambi → entain | 49 | 73.5% | polling artifact |
  | pinnacle → kambi | 37 | 73.0% | polling artifact |
  | pinnacle → entain | 85 | 68.2% | polling artifact |
  | entain → neo | 20 | 65.0% | polling artifact |
  | neo → kambi | 20 | 65.0% | polling artifact |
  | kambi → pinnacle | 17 | 64.7% | polling artifact |
  | kambi → altenar | 106 | 61.3% | weak |
  | altenar → entain | 637 | 60.3% | polling artifact |
  | entain → altenar | 835 | 59.6% | polling artifact |
  | altenar → neo | 65 | 56.9% | polling artifact |
  | pinnacle → altenar | 55 | 56.4% | polling artifact |
  | altenar → pinnacle | 83 | 54.2% | polling artifact |
  | altenar → kambi | 128 | 50.8% | polling artifact |
  | neo → pinnacle | 6 | 50.0% | polling artifact |
  | neo → altenar | 27 | 48.1% | polling artifact |
  | entain → kambi | 56 | 41.1% | polling artifact |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **1,052**
- passed clean (zero warnings): **82**
- flagged or withheld: **970** (92% of everything found)
- rated high confidence: **3**
- average quoted edge, clean rows: **1.82%**
- average quoted edge, flagged rows: **1.56%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **1,843**
- best price vs the **median** price: **1.82%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.17%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **Cincinnati Bengals -15.50** — 3.98 worst vs **5.25** at BetRivers (**+32.1%**)

## Book movement (stale-line detection)
- observed window: **1440 minutes**, 7504 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 11923 | 6501 | 5422 | 45.5% |
  | Pinnacle | pinnacle | 6744 | 4605 | 2139 | 31.7% |
  | bwin | entain | 3831 | 2851 | 980 | 25.6% |
  | DAZN Bet | altenar | 11397 | 8595 | 2802 | 24.6% |
  | BetMGM | entain | 11503 | 8901 | 2602 | 22.6% |
  | NEO.bet | neo | 1121 | 931 | 190 | 16.9% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **1,869**
- graded against a closing line so far: **445**
- average CLV: **3.114%** (276 of 445 beat the close)
- average CLV on **clean** rows: **3.429%**
- average CLV on **flagged** rows: **2.989%**

  If the clean rows do not beat the flagged ones over time, our confidence gate is decoration and we would rather know it.

## Known limits — stated, not hidden
- NFL only so far; other leagues collect but are not tuned.
- Pregame only. No in-play pricing.
- Leader/laggard needs many hours of history; it currently reports nothing rather than guessing.
- Upstream feeds are public sportsbook client APIs. They can change or close without notice; there is no SLA behind them.