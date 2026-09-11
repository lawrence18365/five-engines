# Product proof report
_Generated 2026-09-11 16:30 UTC from live data — last 24h_

## Collection health
- collection runs: **1478 total, 1265 ok, 212 failed** (86% uptime)
- prices collected: **193,531** across **92** events
- snapshots: **3362** over **1089 minutes** of observation
  - DAZN Bet (altenar): 70 events, 55,326 prices
  - BetMGM (entain): 32 events, 73,113 prices
  - bwin (entain): 14 events, 16,409 prices
  - BetRivers (kambi): 62 events, 35,566 prices
  - NEO.bet (neo): 33 events, 3,818 prices
  - Pinnacle (pinnacle): 32 events, 9,299 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **232**
- exact markets priced by 2 or more engines: **5,043**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,324 | 100.0% |
  | bwin vs neobet | 629 | 10.7% |
  | betmgm vs neobet | 679 | 10.2% |
  | betrivers_on vs bwin | 2,322 | 10.1% |
  | betrivers_on vs neobet | 744 | 9.9% |
  | betmgm vs betrivers_on | 3,046 | 9.5% |
  | dazn_bet vs neobet | 574 | 2.6% |
  | betrivers_on vs dazn_bet | 2,334 | 2.4% |
  | bwin vs dazn_bet | 1,708 | 2.2% |
  | betmgm vs dazn_bet | 2,258 | 2.0% |
  | betrivers_on vs pinnacle | 1,304 | 1.7% |
  | bwin vs pinnacle | 756 | 0.9% |
  | betmgm vs pinnacle | 1,070 | 0.8% |
  | dazn_bet vs pinnacle | 962 | 0.8% |
  | neobet vs pinnacle | 288 | 0.3% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | total | 4,403 | 1.97 | 626 | 606 |
  | spread | 4,008 | 1.95 | 595 | 841 |
  | team_total | 2,934 | 1.27 | 20 | 428 |
  | moneyline | 239 | 1.90 | 30 | 94 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **1094 minutes**, 3395 snapshots
- unbiased (randomised collection order): **1012 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | kambi → altenar | 14 | 100.0% | polling artifact |
  | pinnacle → kambi | 94 | 81.9% | polling artifact |
  | altenar → pinnacle | 46 | 80.4% | polling artifact |
  | altenar → neo | 7 | 71.4% | polling artifact |
  | entain → pinnacle | 251 | 70.1% | polling artifact |
  | entain → neo | 10 | 70.0% | polling artifact |
  | kambi → pinnacle | 331 | 62.5% | polling artifact |
  | entain → altenar | 279 | 60.6% | weak |
  | altenar → kambi | 25 | 52.0% | polling artifact |
  | kambi → entain | 93 | 51.6% | polling artifact |
  | neo → pinnacle | 4 | 50.0% | polling artifact |
  | pinnacle → entain | 157 | 46.5% | noise |
  | pinnacle → altenar | 22 | 45.5% | noise |
  | neo → altenar | 7 | 42.9% | polling artifact |
  | entain → kambi | 167 | 42.5% | polling artifact |
  | altenar → entain | 212 | 38.7% | polling artifact |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **568**
- passed clean (zero warnings): **87**
- flagged or withheld: **481** (85% of everything found)
- rated high confidence: **21**
- average quoted edge, clean rows: **0.94%**
- average quoted edge, flagged rows: **3.08%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **2,241**
- best price vs the **median** price: **2.09%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.85%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **Under 5.50** — 1.56 worst vs **3.40** at BetMGM (**+117.9%**)

## Book movement (stale-line detection)
- observed window: **1089 minutes**, 3362 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 3827 | 2286 | 1541 | 40.3% |
  | bwin | entain | 3546 | 2356 | 1190 | 33.6% |
  | BetMGM | entain | 4689 | 3370 | 1319 | 28.1% |
  | Pinnacle | pinnacle | 2563 | 1844 | 719 | 28.1% |
  | DAZN Bet | altenar | 2667 | 2155 | 512 | 19.2% |
  | NEO.bet | neo | 1132 | 928 | 204 | 18.0% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **832**
- graded against a closing line so far: **0**

  Nothing is graded yet — a closing line only exists once an event starts. This section will fill in on its own, and we publish it whichever way it goes.

## Known limits — stated, not hidden
- NFL only so far; other leagues collect but are not tuned.
- Pregame only. No in-play pricing.
- Leader/laggard needs many hours of history; it currently reports nothing rather than guessing.
- Upstream feeds are public sportsbook client APIs. They can change or close without notice; there is no SLA behind them.