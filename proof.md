# Product proof report
_Generated 2026-09-13 08:39 UTC from live data — last 24h_

## Collection health
- collection runs: **655 total, 547 ok, 108 failed** (84% uptime)
- prices collected: **358,085** across **222** events
- snapshots: **6894** over **1430 minutes** of observation
  - DAZN Bet (altenar): 274 events, 275,396 prices
  - BetMGM (entain): 170 events, 291,177 prices
  - bwin (entain): 14 events, 43,964 prices
  - BetRivers (kambi): 208 events, 193,003 prices
  - NEO.bet (neo): 69 events, 16,656 prices
  - Pinnacle (pinnacle): 177 events, 61,492 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **280**
- exact markets priced by 2 or more engines: **19,713**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,362 | 99.8% |
  | betrivers_on vs bwin | 2,356 | 10.2% |
  | bwin vs neobet | 665 | 10.2% |
  | betmgm vs neobet | 709 | 9.9% |
  | betmgm vs betrivers_on | 8,805 | 8.9% |
  | betrivers_on vs neobet | 824 | 8.1% |
  | dazn_bet vs neobet | 734 | 3.7% |
  | betrivers_on vs dazn_bet | 8,333 | 2.1% |
  | betrivers_on vs pinnacle | 4,864 | 1.9% |
  | bwin vs dazn_bet | 1,972 | 1.5% |
  | betmgm vs dazn_bet | 7,602 | 1.4% |
  | bwin vs pinnacle | 776 | 1.0% |
  | dazn_bet vs pinnacle | 3,364 | 1.0% |
  | betmgm vs pinnacle | 3,074 | 0.9% |
  | neobet vs pinnacle | 318 | 0.9% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | spread | 17,155 | 1.82 | 1,309 | 3,562 |
  | total | 16,115 | 1.92 | 1,586 | 3,803 |
  | team_total | 5,842 | 1.45 | 116 | 1,434 |
  | moneyline | 1,416 | 1.67 | 136 | 366 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **1435 minutes**, 6891 snapshots
- unbiased (randomised collection order): **3421 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | pinnacle → neo | 2 | 100.0% | polling artifact |
  | neo → pinnacle | 2 | 100.0% | polling artifact |
  | kambi → neo | 45 | 93.3% | polling artifact |
  | pinnacle → altenar | 47 | 91.5% | polling artifact |
  | entain → pinnacle | 11 | 81.8% | polling artifact |
  | kambi → pinnacle | 46 | 76.1% | polling artifact |
  | altenar → kambi | 6 | 66.7% | polling artifact |
  | pinnacle → kambi | 3 | 66.7% | polling artifact |
  | neo → entain | 11 | 63.6% | polling artifact |
  | altenar → neo | 27 | 59.3% | polling artifact |
  | neo → altenar | 42 | 57.1% | polling artifact |
  | entain → neo | 12 | 50.0% | polling artifact |
  | entain → altenar | 175 | 49.1% | polling artifact |
  | altenar → entain | 274 | 38.3% | polling artifact |
  | pinnacle → entain | 3 | 33.3% | polling artifact |
  | altenar → pinnacle | 33 | 27.3% | polling artifact |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **495**
- passed clean (zero warnings): **50**
- flagged or withheld: **445** (90% of everything found)
- rated high confidence: **2**
- average quoted edge, clean rows: **2.06%**
- average quoted edge, flagged rows: **2.29%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **2,077**
- best price vs the **median** price: **2.00%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.13%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **Western Kentucky ** — 21.00 worst vs **141.00** at BetRivers (**+571.4%**)

## Book movement (stale-line detection)
- observed window: **1430 minutes**, 6889 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 14043 | 8551 | 5492 | 39.1% |
  | BetMGM | entain | 12829 | 10000 | 2829 | 22.1% |
  | bwin | entain | 4103 | 3216 | 887 | 21.6% |
  | DAZN Bet | altenar | 14134 | 11304 | 2830 | 20.0% |
  | Pinnacle | pinnacle | 7743 | 6680 | 1063 | 13.7% |
  | NEO.bet | neo | 1180 | 1064 | 116 | 9.8% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **3,833**
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