# Product proof report
_Generated 2026-09-11 20:27 UTC from live data — last 24h_

## Collection health
- collection runs: **1659 total, 1441 ok, 212 failed** (87% uptime)
- prices collected: **331,358** across **257** events
- snapshots: **5451** over **1329 minutes** of observation
  - DAZN Bet (altenar): 235 events, 95,688 prices
  - BetMGM (entain): 84 events, 115,180 prices
  - bwin (entain): 14 events, 19,561 prices
  - BetRivers (kambi): 179 events, 77,026 prices
  - NEO.bet (neo): 43 events, 5,206 prices
  - Pinnacle (pinnacle): 128 events, 18,697 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **256**
- exact markets priced by 2 or more engines: **14,287**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,330 | 95.6% |
  | betrivers_on vs bwin | 2,326 | 12.9% |
  | bwin vs neobet | 635 | 11.2% |
  | betmgm vs neobet | 685 | 10.9% |
  | betmgm vs betrivers_on | 7,436 | 10.8% |
  | betrivers_on vs neobet | 752 | 10.4% |
  | bwin vs dazn_bet | 1,876 | 2.3% |
  | betmgm vs dazn_bet | 6,089 | 1.7% |
  | dazn_bet vs neobet | 706 | 1.7% |
  | betrivers_on vs pinnacle | 3,640 | 1.5% |
  | betrivers_on vs dazn_bet | 6,792 | 1.3% |
  | bwin vs pinnacle | 766 | 0.8% |
  | neobet vs pinnacle | 292 | 0.7% |
  | betmgm vs pinnacle | 2,368 | 0.6% |
  | dazn_bet vs pinnacle | 2,368 | 0.6% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | spread | 13,061 | 1.87 | 1,151 | 2,758 |
  | total | 12,895 | 1.84 | 1,118 | 2,497 |
  | team_total | 4,260 | 1.34 | 74 | 670 |
  | moneyline | 934 | 1.82 | 114 | 349 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **1332 minutes**, 5466 snapshots
- unbiased (randomised collection order): **1250 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | pinnacle → neo | 21 | 100.0% | polling artifact |
  | kambi → neo | 53 | 94.3% | polling artifact |
  | neo → entain | 77 | 87.0% | polling artifact |
  | kambi → altenar | 190 | 80.0% | noise |
  | entain → pinnacle | 386 | 73.8% | polling artifact |
  | altenar → neo | 101 | 70.3% | polling artifact |
  | neo → kambi | 83 | 69.9% | polling artifact |
  | neo → pinnacle | 13 | 69.2% | polling artifact |
  | altenar → pinnacle | 193 | 66.8% | polling artifact |
  | kambi → entain | 257 | 63.8% | polling artifact |
  | entain → neo | 63 | 63.5% | weak |
  | pinnacle → entain | 317 | 59.9% | polling artifact |
  | pinnacle → kambi | 392 | 59.9% | polling artifact |
  | entain → altenar | 658 | 59.3% | polling artifact |
  | altenar → entain | 603 | 59.0% | polling artifact |
  | pinnacle → altenar | 70 | 57.1% | polling artifact |
  | kambi → pinnacle | 620 | 55.3% | polling artifact |
  | entain → kambi | 437 | 51.5% | polling artifact |
  | altenar → kambi | 218 | 51.4% | polling artifact |
  | neo → altenar | 39 | 46.2% | noise |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **1,148**
- passed clean (zero warnings): **146**
- flagged or withheld: **1,002** (87% of everything found)
- rated high confidence: **43**
- average quoted edge, clean rows: **2.18%**
- average quoted edge, flagged rows: **2.68%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **5,879**
- best price vs the **median** price: **2.04%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.71%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **Texas Southern Tigers ** — 11.00 worst vs **21.00** at BetRivers (**+90.9%**)

## Book movement (stale-line detection)
- observed window: **1329 minutes**, 5451 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | DAZN Bet | altenar | 6943 | 4490 | 2453 | 35.3% |
  | Pinnacle | pinnacle | 4513 | 2970 | 1543 | 34.2% |
  | BetRivers | kambi | 8417 | 5603 | 2814 | 33.4% |
  | BetMGM | entain | 8376 | 5904 | 2472 | 29.5% |
  | bwin | entain | 4255 | 3060 | 1195 | 28.1% |
  | NEO.bet | neo | 1274 | 1093 | 181 | 14.2% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **1,731**
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