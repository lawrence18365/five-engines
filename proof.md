# Product proof report
_Generated 2026-09-11 19:48 UTC from live data — last 24h_

## Collection health
- collection runs: **1629 total, 1412 ok, 212 failed** (87% uptime)
- prices collected: **309,375** across **255** events
- snapshots: **5044** over **1287 minutes** of observation
  - DAZN Bet (altenar): 235 events, 89,505 prices
  - BetMGM (entain): 84 events, 108,856 prices
  - bwin (entain): 14 events, 19,561 prices
  - BetRivers (kambi): 179 events, 70,163 prices
  - NEO.bet (neo): 43 events, 4,979 prices
  - Pinnacle (pinnacle): 84 events, 16,311 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **254**
- exact markets priced by 2 or more engines: **13,820**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,330 | 100.0% |
  | betrivers_on vs bwin | 2,326 | 11.1% |
  | bwin vs neobet | 635 | 10.6% |
  | betmgm vs betrivers_on | 7,426 | 10.4% |
  | betmgm vs neobet | 685 | 10.1% |
  | betrivers_on vs neobet | 748 | 9.1% |
  | bwin vs dazn_bet | 1,862 | 2.3% |
  | betmgm vs dazn_bet | 6,057 | 1.7% |
  | betrivers_on vs dazn_bet | 6,736 | 1.5% |
  | betrivers_on vs pinnacle | 3,004 | 1.4% |
  | dazn_bet vs neobet | 706 | 1.4% |
  | bwin vs pinnacle | 764 | 1.0% |
  | betmgm vs pinnacle | 2,352 | 0.9% |
  | neobet vs pinnacle | 290 | 0.7% |
  | dazn_bet vs pinnacle | 2,076 | 0.6% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | spread | 12,935 | 1.86 | 1,139 | 2,722 |
  | total | 12,509 | 1.83 | 1,114 | 2,373 |
  | team_total | 4,216 | 1.34 | 70 | 654 |
  | moneyline | 934 | 1.80 | 114 | 367 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **1287 minutes**, 5044 snapshots
- unbiased (randomised collection order): **1210 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | pinnacle → neo | 21 | 100.0% | polling artifact |
  | kambi → neo | 45 | 93.3% | polling artifact |
  | neo → entain | 77 | 87.0% | polling artifact |
  | kambi → altenar | 160 | 76.3% | noise |
  | entain → pinnacle | 305 | 73.4% | polling artifact |
  | altenar → neo | 101 | 70.3% | polling artifact |
  | neo → pinnacle | 13 | 69.2% | polling artifact |
  | pinnacle → kambi | 255 | 63.9% | weak |
  | entain → neo | 63 | 63.5% | weak |
  | entain → altenar | 585 | 59.3% | weak |
  | altenar → pinnacle | 143 | 58.0% | polling artifact |
  | entain → kambi | 332 | 57.5% | polling artifact |
  | kambi → pinnacle | 533 | 57.2% | polling artifact |
  | pinnacle → entain | 289 | 57.1% | polling artifact |
  | neo → kambi | 58 | 56.9% | polling artifact |
  | kambi → entain | 195 | 55.4% | polling artifact |
  | pinnacle → altenar | 66 | 54.5% | noise |
  | altenar → entain | 419 | 52.7% | polling artifact |
  | altenar → kambi | 145 | 52.4% | polling artifact |
  | neo → altenar | 38 | 47.4% | noise |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **1,077**
- passed clean (zero warnings): **161**
- flagged or withheld: **916** (85% of everything found)
- rated high confidence: **43**
- average quoted edge, clean rows: **1.34%**
- average quoted edge, flagged rows: **2.65%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **5,180**
- best price vs the **median** price: **1.82%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.25%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **Bowling Green ** — 21.00 worst vs **29.00** at BetMGM (**+38.1%**)

## Book movement (stale-line detection)
- observed window: **1287 minutes**, 5044 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | Pinnacle | pinnacle | 3441 | 2271 | 1170 | 34.0% |
  | DAZN Bet | altenar | 5440 | 3611 | 1829 | 33.6% |
  | BetRivers | kambi | 6625 | 4426 | 2199 | 33.2% |
  | BetMGM | entain | 6897 | 4825 | 2072 | 30.0% |
  | bwin | entain | 4074 | 2979 | 1095 | 26.9% |
  | NEO.bet | neo | 1247 | 1070 | 177 | 14.2% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **1,559**
- graded against a closing line so far: **10**
- average CLV: **3.919%** (6 of 10 beat the close)
- average CLV on **clean** rows: **-1.728%**
- average CLV on **flagged** rows: **6.339%**

  If the clean rows do not beat the flagged ones over time, our confidence gate is decoration and we would rather know it.

## Known limits — stated, not hidden
- NFL only so far; other leagues collect but are not tuned.
- Pregame only. No in-play pricing.
- Leader/laggard needs many hours of history; it currently reports nothing rather than guessing.
- Upstream feeds are public sportsbook client APIs. They can change or close without notice; there is no SLA behind them.