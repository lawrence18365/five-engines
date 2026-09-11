# Product proof report
_Generated 2026-09-11 16:16 UTC from live data — last 24h_

## Collection health
- collection runs: **1465 total, 1251 ok, 212 failed** (85% uptime)
- prices collected: **189,678** across **92** events
- snapshots: **3265** over **1076 minutes** of observation
  - DAZN Bet (altenar): 70 events, 54,502 prices
  - BetMGM (entain): 32 events, 71,790 prices
  - bwin (entain): 14 events, 15,845 prices
  - BetRivers (kambi): 62 events, 35,416 prices
  - NEO.bet (neo): 33 events, 3,695 prices
  - Pinnacle (pinnacle): 32 events, 8,467 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **232**
- exact markets priced by 2 or more engines: **5,043**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,324 | 98.1% |
  | bwin vs neobet | 629 | 11.1% |
  | betrivers_on vs bwin | 2,322 | 10.4% |
  | betmgm vs neobet | 679 | 10.2% |
  | betrivers_on vs neobet | 744 | 10.1% |
  | betmgm vs betrivers_on | 3,046 | 9.6% |
  | betrivers_on vs dazn_bet | 2,334 | 2.4% |
  | dazn_bet vs neobet | 574 | 2.3% |
  | betmgm vs dazn_bet | 2,258 | 2.0% |
  | bwin vs dazn_bet | 1,708 | 2.0% |
  | betrivers_on vs pinnacle | 1,302 | 1.6% |
  | bwin vs pinnacle | 756 | 0.9% |
  | betmgm vs pinnacle | 1,068 | 0.9% |
  | dazn_bet vs pinnacle | 960 | 0.7% |
  | neobet vs pinnacle | 288 | 0.7% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | total | 4,399 | 1.97 | 624 | 606 |
  | spread | 4,008 | 1.95 | 595 | 843 |
  | team_total | 2,932 | 1.27 | 20 | 428 |
  | moneyline | 239 | 1.90 | 30 | 94 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **1078 minutes**, 3301 snapshots
- unbiased (randomised collection order): **997 minutes**

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
  | entain → neo | 10 | 70.0% | polling artifact |
  | entain → pinnacle | 202 | 66.3% | polling artifact |
  | kambi → pinnacle | 331 | 62.5% | polling artifact |
  | entain → altenar | 279 | 60.6% | weak |
  | altenar → kambi | 25 | 52.0% | polling artifact |
  | kambi → entain | 93 | 51.6% | polling artifact |
  | neo → pinnacle | 4 | 50.0% | polling artifact |
  | pinnacle → altenar | 22 | 45.5% | noise |
  | pinnacle → entain | 148 | 45.3% | noise |
  | neo → altenar | 7 | 42.9% | polling artifact |
  | entain → kambi | 166 | 42.2% | polling artifact |
  | altenar → entain | 212 | 38.7% | polling artifact |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **573**
- passed clean (zero warnings): **89**
- flagged or withheld: **484** (84% of everything found)
- rated high confidence: **21**
- average quoted edge, clean rows: **0.90%**
- average quoted edge, flagged rows: **3.06%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **2,239**
- best price vs the **median** price: **2.11%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.83%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **Under 5.50** — 1.56 worst vs **3.40** at BetMGM (**+117.9%**)

## Book movement (stale-line detection)
- observed window: **1076 minutes**, 3269 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 3813 | 2286 | 1527 | 40.0% |
  | bwin | entain | 3532 | 2350 | 1182 | 33.5% |
  | BetMGM | entain | 4673 | 3361 | 1312 | 28.1% |
  | Pinnacle | pinnacle | 2556 | 1841 | 715 | 28.0% |
  | NEO.bet | neo | 1096 | 884 | 212 | 19.3% |
  | DAZN Bet | altenar | 2651 | 2142 | 509 | 19.2% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **828**
- graded against a closing line so far: **0**

  Nothing is graded yet — a closing line only exists once an event starts. This section will fill in on its own, and we publish it whichever way it goes.

## Known limits — stated, not hidden
- NFL only so far; other leagues collect but are not tuned.
- Pregame only. No in-play pricing.
- Leader/laggard needs many hours of history; it currently reports nothing rather than guessing.
- Upstream feeds are public sportsbook client APIs. They can change or close without notice; there is no SLA behind them.