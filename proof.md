# Product proof report
_Generated 2026-09-12 04:09 UTC from live data — last 24h_

## Collection health
- collection runs: **1428 total, 1247 ok, 164 failed** (87% uptime)
- prices collected: **400,664** across **230** events
- snapshots: **7577** over **1438 minutes** of observation
  - DAZN Bet (altenar): 239 events, 141,113 prices
  - BetMGM (entain): 85 events, 172,559 prices
  - bwin (entain): 14 events, 24,554 prices
  - BetRivers (kambi): 192 events, 110,245 prices
  - NEO.bet (neo): 46 events, 7,682 prices
  - Pinnacle (pinnacle): 162 events, 29,364 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **266**
- exact markets priced by 2 or more engines: **15,952**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,340 | 90.8% |
  | betrivers_on vs bwin | 2,338 | 12.0% |
  | bwin vs neobet | 644 | 11.0% |
  | betmgm vs betrivers_on | 7,593 | 10.3% |
  | betmgm vs neobet | 693 | 10.2% |
  | betrivers_on vs neobet | 762 | 9.8% |
  | dazn_bet vs neobet | 718 | 2.4% |
  | bwin vs dazn_bet | 1,956 | 2.1% |
  | betrivers_on vs dazn_bet | 7,230 | 1.7% |
  | betrivers_on vs pinnacle | 3,983 | 1.6% |
  | betmgm vs dazn_bet | 6,715 | 1.5% |
  | dazn_bet vs pinnacle | 2,696 | 1.0% |
  | bwin vs pinnacle | 776 | 0.9% |
  | betmgm vs pinnacle | 2,420 | 0.7% |
  | neobet vs pinnacle | 304 | 0.3% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | spread | 14,306 | 1.85 | 1,187 | 2,940 |
  | total | 13,704 | 1.88 | 1,140 | 3,200 |
  | team_total | 4,708 | 1.35 | 84 | 820 |
  | moneyline | 967 | 1.82 | 114 | 369 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **1437 minutes**, 7570 snapshots
- unbiased (randomised collection order): **1711 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | pinnacle → neo | 16 | 93.8% | polling artifact |
  | kambi → neo | 39 | 92.3% | polling artifact |
  | neo → entain | 67 | 82.1% | polling artifact |
  | entain → pinnacle | 78 | 80.8% | polling artifact |
  | pinnacle → kambi | 48 | 79.2% | polling artifact |
  | kambi → entain | 69 | 73.9% | polling artifact |
  | altenar → neo | 109 | 71.6% | polling artifact |
  | pinnacle → entain | 79 | 70.9% | polling artifact |
  | kambi → pinnacle | 23 | 69.6% | polling artifact |
  | entain → neo | 36 | 69.4% | polling artifact |
  | altenar → pinnacle | 121 | 68.6% | polling artifact |
  | neo → pinnacle | 10 | 60.0% | polling artifact |
  | pinnacle → altenar | 60 | 58.3% | polling artifact |
  | entain → altenar | 647 | 58.1% | polling artifact |
  | altenar → entain | 460 | 57.6% | polling artifact |
  | kambi → altenar | 136 | 57.4% | weak |
  | entain → kambi | 97 | 54.6% | polling artifact |
  | neo → kambi | 43 | 51.2% | polling artifact |
  | neo → altenar | 28 | 50.0% | polling artifact |
  | altenar → kambi | 147 | 49.0% | polling artifact |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **1,033**
- passed clean (zero warnings): **79**
- flagged or withheld: **954** (92% of everything found)
- rated high confidence: **23**
- average quoted edge, clean rows: **2.00%**
- average quoted edge, flagged rows: **1.57%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **5,584**
- best price vs the **median** price: **1.98%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.67%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **East Tennessee State Buccaneers ** — 21.00 worst vs **51.00** at BetMGM (**+142.9%**)

## Book movement (stale-line detection)
- observed window: **1439 minutes**, 7572 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 12015 | 6535 | 5480 | 45.6% |
  | Pinnacle | pinnacle | 6875 | 4857 | 2018 | 29.4% |
  | bwin | entain | 3829 | 2855 | 974 | 25.4% |
  | DAZN Bet | altenar | 11591 | 8784 | 2807 | 24.2% |
  | BetMGM | entain | 11544 | 8909 | 2635 | 22.8% |
  | NEO.bet | neo | 1124 | 936 | 188 | 16.7% |

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