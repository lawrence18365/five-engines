# Product proof report
_Generated 2026-09-11 21:30 UTC from live data — last 24h_

## Collection health
- collection runs: **1701 total, 1479 ok, 214 failed** (87% uptime)
- prices collected: **351,473** across **259** events
- snapshots: **5896** over **1386 minutes** of observation
  - DAZN Bet (altenar): 235 events, 103,136 prices
  - BetMGM (entain): 84 events, 118,644 prices
  - bwin (entain): 14 events, 19,561 prices
  - BetRivers (kambi): 179 events, 83,669 prices
  - NEO.bet (neo): 43 events, 5,999 prices
  - Pinnacle (pinnacle): 151 events, 20,464 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **266**
- exact markets priced by 2 or more engines: **14,459**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,330 | 94.6% |
  | betrivers_on vs bwin | 2,326 | 12.9% |
  | betrivers_on vs neobet | 760 | 11.4% |
  | betmgm vs betrivers_on | 7,444 | 10.7% |
  | betmgm vs neobet | 693 | 9.7% |
  | bwin vs neobet | 643 | 9.3% |
  | bwin vs dazn_bet | 1,908 | 2.0% |
  | betmgm vs dazn_bet | 6,149 | 1.7% |
  | betrivers_on vs dazn_bet | 6,852 | 1.6% |
  | dazn_bet vs neobet | 712 | 1.5% |
  | betrivers_on vs pinnacle | 3,716 | 1.4% |
  | bwin vs pinnacle | 776 | 0.8% |
  | neobet vs pinnacle | 304 | 0.7% |
  | betmgm vs pinnacle | 2,386 | 0.7% |
  | dazn_bet vs pinnacle | 2,460 | 0.5% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | spread | 13,139 | 1.88 | 1,161 | 2,778 |
  | total | 12,978 | 1.84 | 1,126 | 2,535 |
  | team_total | 4,296 | 1.34 | 78 | 694 |
  | moneyline | 937 | 1.82 | 114 | 349 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **1394 minutes**, 5919 snapshots
- unbiased (randomised collection order): **1313 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | pinnacle → neo | 27 | 100.0% | polling artifact |
  | kambi → neo | 68 | 95.6% | polling artifact |
  | neo → entain | 78 | 87.2% | polling artifact |
  | entain → pinnacle | 390 | 73.6% | polling artifact |
  | altenar → pinnacle | 287 | 70.0% | polling artifact |
  | neo → kambi | 83 | 69.9% | polling artifact |
  | altenar → neo | 111 | 68.5% | polling artifact |
  | pinnacle → entain | 404 | 66.6% | polling artifact |
  | altenar → entain | 797 | 66.0% | polling artifact |
  | entain → neo | 63 | 63.5% | weak |
  | kambi → entain | 279 | 62.7% | polling artifact |
  | pinnacle → altenar | 111 | 62.2% | weak |
  | entain → altenar | 832 | 61.2% | polling artifact |
  | pinnacle → kambi | 392 | 59.9% | polling artifact |
  | altenar → kambi | 301 | 57.8% | polling artifact |
  | kambi → pinnacle | 737 | 57.0% | polling artifact |
  | neo → pinnacle | 18 | 55.6% | polling artifact |
  | kambi → altenar | 355 | 49.9% | noise |
  | entain → kambi | 477 | 48.6% | polling artifact |
  | neo → altenar | 42 | 47.6% | polling artifact |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **1,150**
- passed clean (zero warnings): **83**
- flagged or withheld: **1,067** (93% of everything found)
- rated high confidence: **15**
- average quoted edge, clean rows: **1.61%**
- average quoted edge, flagged rows: **1.47%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **6,009**
- best price vs the **median** price: **2.02%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.77%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **Texas Southern Tigers ** — 11.00 worst vs **21.00** at BetRivers (**+90.9%**)

## Book movement (stale-line detection)
- observed window: **1393 minutes**, 5897 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 9635 | 6385 | 3250 | 33.7% |
  | BetMGM | entain | 9163 | 6324 | 2839 | 31.0% |
  | Pinnacle | pinnacle | 5287 | 3704 | 1583 | 29.9% |
  | DAZN Bet | altenar | 7938 | 5593 | 2345 | 29.5% |
  | bwin | entain | 4344 | 3121 | 1223 | 28.2% |
  | NEO.bet | neo | 1335 | 1183 | 152 | 11.4% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **1,934**
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