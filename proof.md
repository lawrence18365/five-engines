# Product proof report
_Generated 2026-09-12 05:33 UTC from live data — last 24h_

## Collection health
- collection runs: **1341 total, 1183 ok, 140 failed** (88% uptime)
- prices collected: **409,124** across **231** events
- snapshots: **7726** over **1439 minutes** of observation
  - DAZN Bet (altenar): 240 events, 146,715 prices
  - BetMGM (entain): 85 events, 175,254 prices
  - bwin (entain): 14 events, 24,554 prices
  - BetRivers (kambi): 193 events, 112,583 prices
  - NEO.bet (neo): 47 events, 7,978 prices
  - Pinnacle (pinnacle): 162 events, 30,060 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **266**
- exact markets priced by 2 or more engines: **16,162**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,340 | 89.7% |
  | betrivers_on vs bwin | 2,338 | 12.0% |
  | betmgm vs betrivers_on | 7,603 | 10.3% |
  | bwin vs neobet | 644 | 10.2% |
  | betmgm vs neobet | 693 | 9.4% |
  | betrivers_on vs neobet | 762 | 9.2% |
  | bwin vs dazn_bet | 1,958 | 2.4% |
  | dazn_bet vs neobet | 718 | 2.2% |
  | betrivers_on vs dazn_bet | 7,290 | 1.7% |
  | betrivers_on vs pinnacle | 4,001 | 1.7% |
  | betmgm vs dazn_bet | 6,719 | 1.6% |
  | bwin vs pinnacle | 776 | 0.9% |
  | betmgm vs pinnacle | 2,424 | 0.9% |
  | dazn_bet vs pinnacle | 2,698 | 0.9% |
  | neobet vs pinnacle | 304 | 0.3% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | spread | 14,454 | 1.85 | 1,191 | 2,998 |
  | total | 13,844 | 1.88 | 1,140 | 3,280 |
  | team_total | 4,734 | 1.35 | 84 | 848 |
  | moneyline | 989 | 1.80 | 114 | 369 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **1437 minutes**, 7741 snapshots
- unbiased (randomised collection order): **1795 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | pinnacle → neo | 12 | 100.0% | polling artifact |
  | kambi → neo | 15 | 100.0% | polling artifact |
  | neo → entain | 25 | 80.0% | polling artifact |
  | kambi → altenar | 124 | 77.4% | noise |
  | entain → pinnacle | 47 | 74.5% | polling artifact |
  | kambi → entain | 53 | 73.6% | polling artifact |
  | pinnacle → entain | 60 | 71.7% | polling artifact |
  | altenar → neo | 60 | 71.7% | polling artifact |
  | kambi → pinnacle | 22 | 68.2% | polling artifact |
  | altenar → pinnacle | 103 | 68.0% | polling artifact |
  | neo → kambi | 20 | 65.0% | polling artifact |
  | pinnacle → altenar | 70 | 64.3% | polling artifact |
  | altenar → entain | 524 | 63.5% | polling artifact |
  | entain → altenar | 633 | 59.6% | polling artifact |
  | neo → altenar | 22 | 59.1% | polling artifact |
  | altenar → kambi | 64 | 54.7% | polling artifact |
  | pinnacle → kambi | 36 | 52.8% | polling artifact |
  | entain → neo | 21 | 52.4% | polling artifact |
  | entain → kambi | 39 | 35.9% | polling artifact |
  | neo → pinnacle | 6 | 16.7% | polling artifact |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **1,040**
- passed clean (zero warnings): **83**
- flagged or withheld: **957** (92% of everything found)
- rated high confidence: **2**
- average quoted edge, clean rows: **1.94%**
- average quoted edge, flagged rows: **1.59%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **4,706**
- best price vs the **median** price: **1.82%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.44%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **East Tennessee State Buccaneers ** — 21.00 worst vs **51.00** at BetMGM (**+142.9%**)

## Book movement (stale-line detection)
- observed window: **1440 minutes**, 7744 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 12295 | 6798 | 5497 | 44.7% |
  | Pinnacle | pinnacle | 7106 | 5182 | 1924 | 27.1% |
  | bwin | entain | 3863 | 2859 | 1004 | 26.0% |
  | DAZN Bet | altenar | 11899 | 9066 | 2833 | 23.8% |
  | BetMGM | entain | 11692 | 9073 | 2619 | 22.4% |
  | NEO.bet | neo | 1110 | 939 | 171 | 15.4% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **1,950**
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