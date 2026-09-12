# Product proof report
_Generated 2026-09-12 06:59 UTC from live data — last 24h_

## Collection health
- collection runs: **1245 total, 1113 ok, 114 failed** (89% uptime)
- prices collected: **418,915** across **232** events
- snapshots: **7947** over **1438 minutes** of observation
  - DAZN Bet (altenar): 240 events, 151,850 prices
  - BetMGM (entain): 85 events, 177,448 prices
  - bwin (entain): 14 events, 26,971 prices
  - BetRivers (kambi): 194 events, 115,246 prices
  - NEO.bet (neo): 48 events, 8,112 prices
  - Pinnacle (pinnacle): 162 events, 31,753 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **266**
- exact markets priced by 2 or more engines: **16,322**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,344 | 99.9% |
  | betrivers_on vs bwin | 2,342 | 12.8% |
  | betmgm vs betrivers_on | 7,607 | 10.2% |
  | bwin vs neobet | 646 | 9.6% |
  | betrivers_on vs neobet | 762 | 9.2% |
  | betmgm vs neobet | 693 | 9.2% |
  | bwin vs dazn_bet | 1,962 | 2.7% |
  | betrivers_on vs pinnacle | 4,037 | 1.9% |
  | dazn_bet vs neobet | 718 | 1.8% |
  | betrivers_on vs dazn_bet | 7,366 | 1.7% |
  | betmgm vs dazn_bet | 6,731 | 1.5% |
  | dazn_bet vs pinnacle | 2,716 | 1.0% |
  | betmgm vs pinnacle | 2,428 | 0.9% |
  | bwin vs pinnacle | 776 | 0.6% |
  | neobet vs pinnacle | 304 | 0.3% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | spread | 14,557 | 1.85 | 1,193 | 2,996 |
  | total | 13,894 | 1.89 | 1,144 | 3,330 |
  | team_total | 4,774 | 1.36 | 84 | 892 |
  | moneyline | 992 | 1.80 | 114 | 369 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **1437 minutes**, 7945 snapshots
- unbiased (randomised collection order): **1882 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | kambi → neo | 11 | 100.0% | polling artifact |
  | neo → pinnacle | 1 | 100.0% | polling artifact |
  | neo → entain | 32 | 84.4% | polling artifact |
  | neo → kambi | 19 | 84.2% | polling artifact |
  | entain → pinnacle | 74 | 81.1% | polling artifact |
  | pinnacle → kambi | 57 | 80.7% | polling artifact |
  | kambi → altenar | 41 | 75.6% | noise |
  | entain → altenar | 540 | 71.7% | polling artifact |
  | pinnacle → neo | 9 | 66.7% | polling artifact |
  | kambi → pinnacle | 3 | 66.7% | polling artifact |
  | pinnacle → altenar | 66 | 65.2% | polling artifact |
  | altenar → entain | 451 | 65.0% | polling artifact |
  | pinnacle → entain | 94 | 64.9% | polling artifact |
  | altenar → neo | 24 | 62.5% | polling artifact |
  | entain → kambi | 37 | 56.8% | polling artifact |
  | entain → neo | 16 | 56.3% | polling artifact |
  | altenar → pinnacle | 76 | 52.6% | polling artifact |
  | neo → altenar | 8 | 50.0% | polling artifact |
  | altenar → kambi | 44 | 45.5% | polling artifact |
  | kambi → entain | 30 | 40.0% | polling artifact |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **1,034**
- passed clean (zero warnings): **94**
- flagged or withheld: **940** (91% of everything found)
- rated high confidence: **1**
- average quoted edge, clean rows: **1.94%**
- average quoted edge, flagged rows: **1.51%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **5,265**
- best price vs the **median** price: **1.94%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.57%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **East Tennessee State Buccaneers ** — 21.00 worst vs **67.00** at BetRivers (**+219.0%**)

## Book movement (stale-line detection)
- observed window: **1438 minutes**, 7947 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 12969 | 7173 | 5796 | 44.7% |
  | bwin | entain | 4079 | 3102 | 977 | 24.0% |
  | Pinnacle | pinnacle | 7469 | 5749 | 1720 | 23.0% |
  | BetMGM | entain | 12128 | 9450 | 2678 | 22.1% |
  | DAZN Bet | altenar | 12438 | 9770 | 2668 | 21.5% |
  | NEO.bet | neo | 1118 | 950 | 168 | 15.0% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **1,997**
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