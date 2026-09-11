# Product proof report
_Generated 2026-09-11 22:07 UTC from live data — last 24h_

## Collection health
- collection runs: **1724 total, 1501 ok, 214 failed** (87% uptime)
- prices collected: **370,764** across **260** events
- snapshots: **6217** over **1429 minutes** of observation
  - DAZN Bet (altenar): 236 events, 108,456 prices
  - BetMGM (entain): 84 events, 125,117 prices
  - bwin (entain): 14 events, 19,561 prices
  - BetRivers (kambi): 179 events, 89,128 prices
  - NEO.bet (neo): 43 events, 6,679 prices
  - Pinnacle (pinnacle): 151 events, 22,022 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **266**
- exact markets priced by 2 or more engines: **14,536**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,330 | 89.4% |
  | betrivers_on vs bwin | 2,326 | 12.7% |
  | bwin vs neobet | 643 | 10.7% |
  | betmgm vs betrivers_on | 7,452 | 10.4% |
  | betrivers_on vs neobet | 760 | 9.7% |
  | betmgm vs neobet | 693 | 9.5% |
  | dazn_bet vs neobet | 712 | 2.5% |
  | bwin vs dazn_bet | 1,932 | 2.1% |
  | betrivers_on vs dazn_bet | 6,895 | 1.8% |
  | betmgm vs dazn_bet | 6,213 | 1.8% |
  | betrivers_on vs pinnacle | 3,735 | 1.5% |
  | betmgm vs pinnacle | 2,390 | 1.0% |
  | bwin vs pinnacle | 776 | 0.8% |
  | dazn_bet vs pinnacle | 2,470 | 0.6% |
  | neobet vs pinnacle | 304 | 0.3% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | spread | 13,221 | 1.88 | 1,169 | 2,752 |
  | total | 13,034 | 1.85 | 1,132 | 2,575 |
  | team_total | 4,310 | 1.34 | 78 | 704 |
  | moneyline | 937 | 1.82 | 114 | 348 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **1431 minutes**, 6248 snapshots
- unbiased (randomised collection order): **1351 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | pinnacle → neo | 30 | 96.7% | polling artifact |
  | kambi → neo | 68 | 95.6% | polling artifact |
  | entain → pinnacle | 481 | 75.7% | polling artifact |
  | altenar → neo | 117 | 70.1% | polling artifact |
  | altenar → pinnacle | 287 | 70.0% | polling artifact |
  | neo → kambi | 83 | 69.9% | polling artifact |
  | neo → entain | 102 | 69.6% | polling artifact |
  | pinnacle → entain | 439 | 68.1% | polling artifact |
  | altenar → entain | 936 | 66.0% | polling artifact |
  | entain → neo | 63 | 63.5% | weak |
  | pinnacle → altenar | 145 | 62.8% | weak |
  | entain → altenar | 1017 | 61.5% | polling artifact |
  | kambi → pinnacle | 796 | 58.3% | polling artifact |
  | altenar → kambi | 301 | 57.8% | polling artifact |
  | pinnacle → kambi | 462 | 56.7% | polling artifact |
  | kambi → entain | 311 | 56.3% | polling artifact |
  | neo → pinnacle | 18 | 55.6% | polling artifact |
  | kambi → altenar | 355 | 49.9% | noise |
  | entain → kambi | 506 | 48.6% | polling artifact |
  | neo → altenar | 46 | 45.7% | polling artifact |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **1,078**
- passed clean (zero warnings): **74**
- flagged or withheld: **1,004** (93% of everything found)
- rated high confidence: **21**
- average quoted edge, clean rows: **1.74%**
- average quoted edge, flagged rows: **1.39%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **6,032**
- best price vs the **median** price: **2.00%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.76%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **Texas Southern Tigers ** — 11.00 worst vs **21.00** at BetRivers (**+90.9%**)

## Book movement (stale-line detection)
- observed window: **1430 minutes**, 6230 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 10336 | 6677 | 3659 | 35.4% |
  | DAZN Bet | altenar | 8712 | 6271 | 2441 | 28.0% |
  | BetMGM | entain | 9978 | 7222 | 2756 | 27.6% |
  | Pinnacle | pinnacle | 5817 | 4333 | 1484 | 25.5% |
  | bwin | entain | 4524 | 3426 | 1098 | 24.3% |
  | NEO.bet | neo | 1337 | 1198 | 139 | 10.4% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **1,977**
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