# Product proof report
_Generated 2026-09-11 19:32 UTC from live data — last 24h_

## Collection health
- collection runs: **1622 total, 1404 ok, 212 failed** (87% uptime)
- prices collected: **302,596** across **253** events
- snapshots: **4916** over **1274 minutes** of observation
  - DAZN Bet (altenar): 234 events, 87,472 prices
  - BetMGM (entain): 84 events, 106,237 prices
  - bwin (entain): 14 events, 19,561 prices
  - BetRivers (kambi): 179 events, 68,272 prices
  - NEO.bet (neo): 33 events, 4,816 prices
  - Pinnacle (pinnacle): 84 events, 16,311 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **232**
- exact markets priced by 2 or more engines: **13,625**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,330 | 100.0% |
  | betrivers_on vs bwin | 2,326 | 11.0% |
  | betmgm vs betrivers_on | 7,425 | 10.4% |
  | bwin vs neobet | 633 | 10.3% |
  | betmgm vs neobet | 683 | 9.8% |
  | betrivers_on vs neobet | 746 | 8.3% |
  | bwin vs dazn_bet | 1,744 | 2.1% |
  | dazn_bet vs neobet | 580 | 1.9% |
  | betmgm vs dazn_bet | 5,889 | 1.7% |
  | betrivers_on vs pinnacle | 3,004 | 1.5% |
  | betrivers_on vs dazn_bet | 6,554 | 1.4% |
  | betmgm vs pinnacle | 2,352 | 1.1% |
  | bwin vs pinnacle | 764 | 1.0% |
  | neobet vs pinnacle | 288 | 0.7% |
  | dazn_bet vs pinnacle | 2,056 | 0.5% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | spread | 12,861 | 1.85 | 1,085 | 2,678 |
  | total | 12,454 | 1.82 | 1,114 | 2,318 |
  | team_total | 4,176 | 1.33 | 70 | 638 |
  | moneyline | 934 | 1.80 | 114 | 367 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **1276 minutes**, 4934 snapshots
- unbiased (randomised collection order): **1194 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | pinnacle → neo | 21 | 100.0% | polling artifact |
  | kambi → neo | 45 | 93.3% | polling artifact |
  | neo → entain | 77 | 87.0% | polling artifact |
  | altenar → neo | 92 | 75.0% | polling artifact |
  | entain → pinnacle | 305 | 73.4% | polling artifact |
  | kambi → altenar | 130 | 70.8% | noise |
  | neo → pinnacle | 13 | 69.2% | polling artifact |
  | pinnacle → kambi | 255 | 63.9% | weak |
  | entain → neo | 63 | 63.5% | weak |
  | entain → altenar | 558 | 60.0% | polling artifact |
  | altenar → kambi | 106 | 59.4% | polling artifact |
  | altenar → pinnacle | 143 | 58.0% | polling artifact |
  | entain → kambi | 332 | 57.5% | polling artifact |
  | kambi → pinnacle | 533 | 57.2% | polling artifact |
  | pinnacle → entain | 289 | 57.1% | polling artifact |
  | kambi → entain | 191 | 55.5% | polling artifact |
  | pinnacle → altenar | 66 | 54.5% | noise |
  | altenar → entain | 389 | 50.6% | polling artifact |
  | neo → kambi | 49 | 49.0% | polling artifact |
  | neo → altenar | 38 | 47.4% | noise |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **1,087**
- passed clean (zero warnings): **172**
- flagged or withheld: **915** (84% of everything found)
- rated high confidence: **47**
- average quoted edge, clean rows: **1.27%**
- average quoted edge, flagged rows: **2.73%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **5,758**
- best price vs the **median** price: **2.03%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.80%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **Utah State ** — 11.00 worst vs **20.00** at BetRivers (**+81.8%**)

## Book movement (stale-line detection)
- observed window: **1275 minutes**, 4923 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 5988 | 3899 | 2089 | 34.9% |
  | DAZN Bet | altenar | 4876 | 3264 | 1612 | 33.1% |
  | Pinnacle | pinnacle | 3332 | 2271 | 1061 | 31.8% |
  | BetMGM | entain | 6572 | 4595 | 1977 | 30.1% |
  | bwin | entain | 4061 | 2979 | 1082 | 26.6% |
  | NEO.bet | neo | 1235 | 1062 | 173 | 14.0% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **1,469**
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