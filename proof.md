# Product proof report
_Generated 2026-09-12 04:30 UTC from live data — last 24h_

## Collection health
- collection runs: **1410 total, 1233 ok, 160 failed** (87% uptime)
- prices collected: **404,010** across **230** events
- snapshots: **7622** over **1437 minutes** of observation
  - DAZN Bet (altenar): 239 events, 143,760 prices
  - BetMGM (entain): 85 events, 173,296 prices
  - bwin (entain): 14 events, 24,554 prices
  - BetRivers (kambi): 192 events, 110,719 prices
  - NEO.bet (neo): 46 events, 7,766 prices
  - Pinnacle (pinnacle): 162 events, 29,364 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **266**
- exact markets priced by 2 or more engines: **16,064**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,340 | 89.7% |
  | betrivers_on vs bwin | 2,338 | 12.0% |
  | bwin vs neobet | 644 | 11.0% |
  | betmgm vs betrivers_on | 7,593 | 10.3% |
  | betmgm vs neobet | 693 | 10.1% |
  | betrivers_on vs neobet | 762 | 9.8% |
  | bwin vs dazn_bet | 1,958 | 2.5% |
  | dazn_bet vs neobet | 718 | 2.4% |
  | betrivers_on vs dazn_bet | 7,244 | 1.7% |
  | betmgm vs dazn_bet | 6,717 | 1.7% |
  | betrivers_on vs pinnacle | 3,989 | 1.6% |
  | bwin vs pinnacle | 776 | 0.9% |
  | dazn_bet vs pinnacle | 2,696 | 0.9% |
  | betmgm vs pinnacle | 2,420 | 0.8% |
  | neobet vs pinnacle | 304 | 0.3% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | spread | 14,388 | 1.85 | 1,187 | 2,972 |
  | total | 13,778 | 1.88 | 1,140 | 3,242 |
  | team_total | 4,710 | 1.35 | 84 | 832 |
  | moneyline | 987 | 1.80 | 114 | 369 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **1439 minutes**, 7630 snapshots
- unbiased (randomised collection order): **1732 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | pinnacle → neo | 15 | 100.0% | polling artifact |
  | kambi → neo | 48 | 93.8% | polling artifact |
  | entain → pinnacle | 60 | 88.3% | polling artifact |
  | pinnacle → kambi | 44 | 84.1% | polling artifact |
  | neo → entain | 67 | 82.1% | polling artifact |
  | kambi → entain | 64 | 78.1% | polling artifact |
  | pinnacle → entain | 83 | 73.5% | polling artifact |
  | altenar → pinnacle | 125 | 72.8% | polling artifact |
  | altenar → neo | 103 | 70.9% | polling artifact |
  | entain → neo | 33 | 69.7% | polling artifact |
  | kambi → pinnacle | 23 | 69.6% | polling artifact |
  | neo → kambi | 61 | 65.6% | polling artifact |
  | pinnacle → altenar | 69 | 60.9% | polling artifact |
  | altenar → entain | 488 | 58.8% | polling artifact |
  | entain → altenar | 717 | 58.2% | polling artifact |
  | kambi → altenar | 157 | 56.7% | weak |
  | neo → pinnacle | 9 | 55.6% | polling artifact |
  | entain → kambi | 101 | 51.5% | polling artifact |
  | altenar → kambi | 160 | 48.8% | polling artifact |
  | neo → altenar | 31 | 48.4% | polling artifact |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **1,019**
- passed clean (zero warnings): **79**
- flagged or withheld: **940** (92% of everything found)
- rated high confidence: **1**
- average quoted edge, clean rows: **1.99%**
- average quoted edge, flagged rows: **1.57%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **4,737**
- best price vs the **median** price: **1.81%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.44%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **East Tennessee State Buccaneers ** — 21.00 worst vs **51.00** at BetMGM (**+142.9%**)

## Book movement (stale-line detection)
- observed window: **1438 minutes**, 7629 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 12073 | 6550 | 5523 | 45.7% |
  | Pinnacle | pinnacle | 6906 | 4857 | 2049 | 29.7% |
  | bwin | entain | 3840 | 2859 | 981 | 25.5% |
  | DAZN Bet | altenar | 11678 | 8861 | 2817 | 24.1% |
  | BetMGM | entain | 11591 | 8981 | 2610 | 22.5% |
  | NEO.bet | neo | 1112 | 937 | 175 | 15.7% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **1,908**
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