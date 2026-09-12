# Product proof report
_Generated 2026-09-12 04:54 UTC from live data — last 24h_

## Collection health
- collection runs: **1381 total, 1211 ok, 152 failed** (88% uptime)
- prices collected: **405,355** across **231** events
- snapshots: **7656** over **1439 minutes** of observation
  - DAZN Bet (altenar): 240 events, 144,594 prices
  - BetMGM (entain): 85 events, 174,241 prices
  - bwin (entain): 14 events, 24,554 prices
  - BetRivers (kambi): 192 events, 110,950 prices
  - NEO.bet (neo): 47 events, 7,841 prices
  - Pinnacle (pinnacle): 162 events, 29,364 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **266**
- exact markets priced by 2 or more engines: **16,076**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,340 | 89.7% |
  | betrivers_on vs bwin | 2,338 | 12.0% |
  | bwin vs neobet | 644 | 11.2% |
  | betmgm vs betrivers_on | 7,597 | 10.3% |
  | betmgm vs neobet | 693 | 10.2% |
  | betrivers_on vs neobet | 762 | 9.3% |
  | bwin vs dazn_bet | 1,958 | 2.4% |
  | dazn_bet vs neobet | 718 | 2.2% |
  | betrivers_on vs dazn_bet | 7,248 | 1.7% |
  | betrivers_on vs pinnacle | 3,989 | 1.6% |
  | betmgm vs dazn_bet | 6,717 | 1.5% |
  | dazn_bet vs pinnacle | 2,696 | 1.0% |
  | bwin vs pinnacle | 776 | 0.9% |
  | betmgm vs pinnacle | 2,420 | 0.8% |
  | neobet vs pinnacle | 304 | 0.3% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | spread | 14,402 | 1.85 | 1,189 | 2,980 |
  | total | 13,800 | 1.88 | 1,140 | 3,242 |
  | team_total | 4,712 | 1.35 | 84 | 836 |
  | moneyline | 987 | 1.80 | 114 | 369 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **1438 minutes**, 7664 snapshots
- unbiased (randomised collection order): **1756 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | pinnacle → neo | 2 | 100.0% | polling artifact |
  | kambi → neo | 12 | 100.0% | polling artifact |
  | neo → pinnacle | 1 | 100.0% | polling artifact |
  | neo → kambi | 26 | 92.3% | polling artifact |
  | pinnacle → kambi | 18 | 83.3% | polling artifact |
  | kambi → pinnacle | 16 | 81.3% | polling artifact |
  | neo → entain | 9 | 77.8% | polling artifact |
  | pinnacle → altenar | 30 | 73.3% | polling artifact |
  | kambi → entain | 14 | 64.3% | polling artifact |
  | entain → altenar | 467 | 62.3% | polling artifact |
  | altenar → entain | 357 | 61.6% | polling artifact |
  | entain → pinnacle | 40 | 60.0% | polling artifact |
  | altenar → neo | 32 | 59.4% | polling artifact |
  | altenar → pinnacle | 54 | 59.3% | polling artifact |
  | pinnacle → entain | 44 | 59.1% | polling artifact |
  | kambi → altenar | 93 | 48.4% | noise |
  | altenar → kambi | 109 | 43.1% | polling artifact |
  | neo → altenar | 17 | 41.2% | polling artifact |
  | entain → neo | 5 | 40.0% | polling artifact |
  | entain → kambi | 25 | 36.0% | polling artifact |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **953**
- passed clean (zero warnings): **53**
- flagged or withheld: **900** (94% of everything found)
- rated high confidence: **0**
- average quoted edge, clean rows: **2.39%**
- average quoted edge, flagged rows: **2.75%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **4,708**
- best price vs the **median** price: **1.82%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.44%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **East Tennessee State Buccaneers ** — 21.00 worst vs **51.00** at BetMGM (**+142.9%**)

## Book movement (stale-line detection)
- observed window: **1439 minutes**, 7654 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 12103 | 6557 | 5546 | 45.8% |
  | Pinnacle | pinnacle | 6915 | 4857 | 2058 | 29.8% |
  | bwin | entain | 3836 | 2859 | 977 | 25.5% |
  | DAZN Bet | altenar | 11709 | 8890 | 2819 | 24.1% |
  | BetMGM | entain | 11610 | 9023 | 2587 | 22.3% |
  | NEO.bet | neo | 1106 | 938 | 168 | 15.2% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **1,921**
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