# Product proof report
_Generated 2026-09-11 01:12 UTC from live data — last 24h_

## Collection health
- collection runs: **286 total, 282 ok, 2 failed** (99% uptime)
- prices collected: **75,321** across **95** events
- snapshots: **658** over **175 minutes** of observation
  - DAZN Bet (altenar): 63 events, 18,031 prices
  - BetMGM (entain): 17 events, 33,994 prices
  - BetRivers (kambi): 53 events, 17,442 prices
  - NEO.bet (neo): 30 events, 2,210 prices
  - Pinnacle (pinnacle): 28 events, 3,644 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **224**
- exact markets priced by 2 or more engines: **4,014**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs neobet | 676 | 11.5% |
  | betmgm vs betrivers_on | 2,562 | 9.9% |
  | betrivers_on vs neobet | 742 | 8.0% |
  | betmgm vs dazn_bet | 1,729 | 2.7% |
  | dazn_bet vs neobet | 500 | 2.0% |
  | betrivers_on vs dazn_bet | 1,782 | 1.9% |
  | betrivers_on vs pinnacle | 880 | 1.7% |
  | dazn_bet vs pinnacle | 804 | 0.9% |
  | betmgm vs pinnacle | 832 | 0.7% |
  | neobet vs pinnacle | 282 | 0.4% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | total | 3,825 | 1.81 | 376 | 625 |
  | spread | 3,674 | 1.96 | 580 | 615 |
  | team_total | 2,818 | 1.24 | 18 | 310 |
  | moneyline | 218 | 1.90 | 30 | 74 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **175 minutes**, 658 snapshots
- unbiased (randomised collection order): **94 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | entain → neo | 5 | 60.0% | polling artifact |
  | entain → altenar | 226 | 59.3% | weak |
  | pinnacle → entain | 32 | 56.3% | noise |
  | entain → pinnacle | 57 | 50.9% | polling artifact |
  | neo → pinnacle | 4 | 50.0% | polling artifact |
  | pinnacle → altenar | 15 | 46.7% | insufficient sample |
  | altenar → entain | 197 | 34.5% | polling artifact |
  | altenar → pinnacle | 9 | 22.2% | insufficient sample |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **392**
- passed clean (zero warnings): **81**
- flagged or withheld: **311** (79% of everything found)
- rated high confidence: **37**
- average quoted edge, clean rows: **1.32%**
- average quoted edge, flagged rows: **6.16%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **5 minutes** of the others: **1,923**
- best price vs the **median** price: **2.00%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.76%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **Baltimore Ravens -14.00** — 4.00 worst vs **5.40** at BetRivers (**+35.0%**)

## Book movement (stale-line detection)
- observed window: **175 minutes**, 658 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 1723 | 603 | 1120 | 65.0% |
  | NEO.bet | neo | 493 | 237 | 256 | 51.9% |
  | Pinnacle | pinnacle | 964 | 477 | 487 | 50.5% |
  | BetMGM | entain | 2287 | 1404 | 883 | 38.6% |
  | DAZN Bet | altenar | 1569 | 1149 | 420 | 26.8% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **274**
- graded against a closing line so far: **0**

  Nothing is graded yet — a closing line only exists once an event starts. This section will fill in on its own, and we publish it whichever way it goes.

## Known limits — stated, not hidden
- NFL only so far; other leagues collect but are not tuned.
- Pregame only. No in-play pricing.
- Leader/laggard needs many hours of history; it currently reports nothing rather than guessing.
- Upstream feeds are public sportsbook client APIs. They can change or close without notice; there is no SLA behind them.