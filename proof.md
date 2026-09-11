# Product proof report
_Generated 2026-09-11 08:36 UTC from live data — last 24h_

## Collection health
- collection runs: **961 total, 825 ok, 134 failed** (86% uptime)
- prices collected: **98,956** across **99** events
- snapshots: **1536** over **619 minutes** of observation
  - DAZN Bet (altenar): 66 events, 33,810 prices
  - BetMGM (entain): 17 events, 35,694 prices
  - BetRivers (kambi): 60 events, 23,586 prices
  - NEO.bet (neo): 30 events, 2,222 prices
  - Pinnacle (pinnacle): 28 events, 3,644 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **224**
- exact markets priced by 2 or more engines: **4,338**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs neobet | 676 | 11.4% |
  | betmgm vs betrivers_on | 2,562 | 9.5% |
  | betrivers_on vs neobet | 742 | 8.5% |
  | betmgm vs dazn_bet | 1,733 | 2.2% |
  | dazn_bet vs neobet | 500 | 2.2% |
  | betrivers_on vs pinnacle | 1,132 | 1.8% |
  | betrivers_on vs dazn_bet | 1,960 | 1.8% |
  | betmgm vs pinnacle | 832 | 0.7% |
  | dazn_bet vs pinnacle | 804 | 0.6% |
  | neobet vs pinnacle | 282 | 0.4% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | total | 4,065 | 1.82 | 376 | 663 |
  | spread | 3,766 | 1.97 | 580 | 731 |
  | team_total | 2,834 | 1.26 | 18 | 378 |
  | moneyline | 222 | 1.93 | 30 | 84 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **619 minutes**, 1536 snapshots
- unbiased (randomised collection order): **538 minutes**

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
- opportunities detected: **482**
- passed clean (zero warnings): **70**
- flagged or withheld: **412** (85% of everything found)
- rated high confidence: **8**
- average quoted edge, clean rows: **1.02%**
- average quoted edge, flagged rows: **5.38%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **5 minutes** of the others: **84**
- best price vs the **median** price: **2.83%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **5.33%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **Los Angeles Rams -14.00** — 3.62 worst vs **4.60** at BetMGM (**+26.9%**)

## Book movement (stale-line detection)
- observed window: **619 minutes**, 1536 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | Pinnacle | pinnacle | 1348 | 477 | 871 | 64.6% |
  | NEO.bet | neo | 595 | 237 | 358 | 60.2% |
  | BetRivers | kambi | 2765 | 1322 | 1443 | 52.2% |
  | BetMGM | entain | 2754 | 1409 | 1345 | 48.8% |
  | DAZN Bet | altenar | 2176 | 1878 | 298 | 13.7% |

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