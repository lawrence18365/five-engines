# Product proof report
_Generated 2026-09-13 01:49 UTC from live data — last 24h_

## Collection health
- collection runs: **659 total, 593 ok, 65 failed** (90% uptime)
- prices collected: **383,610** across **209** events
- snapshots: **7639** over **1440 minutes** of observation
  - DAZN Bet (altenar): 257 events, 260,908 prices
  - BetMGM (entain): 165 events, 281,286 prices
  - bwin (entain): 14 events, 34,914 prices
  - BetRivers (kambi): 198 events, 187,476 prices
  - NEO.bet (neo): 62 events, 15,006 prices
  - Pinnacle (pinnacle): 177 events, 58,686 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **278**
- exact markets priced by 2 or more engines: **19,300**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,355 | 84.2% |
  | bwin vs neobet | 662 | 10.1% |
  | betrivers_on vs bwin | 2,350 | 9.7% |
  | betmgm vs neobet | 707 | 9.6% |
  | betmgm vs betrivers_on | 8,799 | 8.5% |
  | betrivers_on vs neobet | 790 | 7.3% |
  | dazn_bet vs neobet | 732 | 2.7% |
  | bwin vs dazn_bet | 1,968 | 2.1% |
  | betrivers_on vs pinnacle | 4,654 | 2.0% |
  | betrivers_on vs dazn_bet | 8,164 | 1.9% |
  | betmgm vs dazn_bet | 7,577 | 1.5% |
  | dazn_bet vs pinnacle | 3,336 | 0.9% |
  | bwin vs pinnacle | 776 | 0.8% |
  | betmgm vs pinnacle | 3,064 | 0.8% |
  | neobet vs pinnacle | 316 | 0.3% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | spread | 16,297 | 1.85 | 1,305 | 3,447 |
  | total | 15,770 | 1.92 | 1,582 | 3,766 |
  | team_total | 5,812 | 1.45 | 114 | 1,404 |
  | moneyline | 1,368 | 1.67 | 136 | 331 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **1439 minutes**, 7624 snapshots
- unbiased (randomised collection order): **3011 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | entain → pinnacle | 50 | 88.0% | polling artifact |
  | pinnacle → entain | 53 | 84.9% | polling artifact |
  | pinnacle → neo | 4 | 75.0% | polling artifact |
  | entain → altenar | 282 | 70.9% | polling artifact |
  | altenar → kambi | 13 | 69.2% | polling artifact |
  | altenar → pinnacle | 40 | 65.0% | polling artifact |
  | altenar → entain | 175 | 60.6% | polling artifact |
  | altenar → neo | 18 | 55.6% | polling artifact |
  | pinnacle → altenar | 8 | 50.0% | polling artifact |
  | entain → kambi | 4 | 50.0% | polling artifact |
  | kambi → entain | 17 | 47.1% | polling artifact |
  | neo → altenar | 9 | 44.4% | polling artifact |
  | kambi → altenar | 15 | 40.0% | polling artifact |
  | entain → neo | 8 | 37.5% | polling artifact |
  | neo → entain | 11 | 36.4% | polling artifact |
  | kambi → pinnacle | 15 | 0.0% | polling artifact |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **598**
- passed clean (zero warnings): **73**
- flagged or withheld: **525** (88% of everything found)
- rated high confidence: **2**
- average quoted edge, clean rows: **1.99%**
- average quoted edge, flagged rows: **2.79%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **2,270**
- best price vs the **median** price: **2.11%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.53%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **Western Kentucky ** — 21.00 worst vs **141.00** at BetRivers (**+571.4%**)

## Book movement (stale-line detection)
- observed window: **1439 minutes**, 7633 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 13982 | 8541 | 5441 | 38.9% |
  | bwin | entain | 3226 | 2061 | 1165 | 36.1% |
  | BetMGM | entain | 12428 | 9626 | 2802 | 22.5% |
  | Pinnacle | pinnacle | 7185 | 5968 | 1217 | 16.9% |
  | DAZN Bet | altenar | 14085 | 11767 | 2318 | 16.5% |
  | NEO.bet | neo | 1160 | 1062 | 98 | 8.4% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **3,735**
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