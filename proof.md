# Product proof report
_Generated 2026-09-11 15:47 UTC from live data — last 24h_

## Collection health
- collection runs: **1442 total, 1228 ok, 212 failed** (85% uptime)
- prices collected: **178,631** across **92** events
- snapshots: **3063** over **1048 minutes** of observation
  - DAZN Bet (altenar): 70 events, 50,046 prices
  - BetMGM (entain): 32 events, 68,642 prices
  - bwin (entain): 14 events, 15,845 prices
  - BetRivers (kambi): 62 events, 33,537 prices
  - NEO.bet (neo): 33 events, 3,610 prices
  - Pinnacle (pinnacle): 32 events, 7,711 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **230**
- exact markets priced by 2 or more engines: **4,975**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,324 | 98.1% |
  | bwin vs neobet | 629 | 10.8% |
  | betrivers_on vs bwin | 2,322 | 10.3% |
  | betrivers_on vs neobet | 744 | 10.2% |
  | betmgm vs neobet | 679 | 9.9% |
  | betmgm vs betrivers_on | 3,046 | 9.6% |
  | dazn_bet vs neobet | 530 | 2.5% |
  | betrivers_on vs dazn_bet | 2,146 | 2.5% |
  | betmgm vs dazn_bet | 2,110 | 1.8% |
  | betrivers_on vs pinnacle | 1,300 | 1.8% |
  | bwin vs dazn_bet | 1,564 | 1.7% |
  | betmgm vs pinnacle | 1,066 | 1.3% |
  | bwin vs pinnacle | 756 | 0.9% |
  | dazn_bet vs pinnacle | 954 | 0.9% |
  | neobet vs pinnacle | 288 | 0.7% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | total | 4,398 | 1.93 | 618 | 692 |
  | spread | 3,978 | 1.94 | 583 | 825 |
  | team_total | 2,930 | 1.27 | 20 | 428 |
  | moneyline | 239 | 1.90 | 30 | 94 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **1049 minutes**, 3129 snapshots
- unbiased (randomised collection order): **969 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | kambi → altenar | 14 | 100.0% | polling artifact |
  | pinnacle → kambi | 83 | 88.0% | polling artifact |
  | entain → neo | 10 | 70.0% | polling artifact |
  | altenar → pinnacle | 25 | 68.0% | polling artifact |
  | entain → pinnacle | 164 | 64.6% | polling artifact |
  | kambi → pinnacle | 199 | 63.8% | polling artifact |
  | entain → altenar | 277 | 60.3% | weak |
  | kambi → entain | 75 | 58.7% | polling artifact |
  | altenar → kambi | 25 | 52.0% | polling artifact |
  | neo → pinnacle | 4 | 50.0% | polling artifact |
  | pinnacle → entain | 133 | 48.9% | noise |
  | pinnacle → altenar | 22 | 45.5% | noise |
  | neo → altenar | 7 | 42.9% | polling artifact |
  | entain → kambi | 156 | 39.7% | polling artifact |
  | altenar → entain | 206 | 36.9% | polling artifact |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **0**
- passed clean (zero warnings): **0**
- flagged or withheld: **0** (0% of everything found)
- rated high confidence: **0**
- average quoted edge, clean rows: **0.00%**
- average quoted edge, flagged rows: **0.00%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **2,009**
- best price vs the **median** price: **1.71%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.12%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **Los Angeles Rams -14.00** — 3.62 worst vs **4.60** at BetMGM (**+26.9%**)

## Book movement (stale-line detection)
- observed window: **1048 minutes**, 3083 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 3741 | 2093 | 1648 | 44.1% |
  | bwin | entain | 3470 | 2350 | 1120 | 32.3% |
  | Pinnacle | pinnacle | 2465 | 1696 | 769 | 31.2% |
  | BetMGM | entain | 4608 | 3355 | 1253 | 27.2% |
  | NEO.bet | neo | 1086 | 872 | 214 | 19.7% |
  | DAZN Bet | altenar | 2536 | 2085 | 451 | 17.8% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **703**
- graded against a closing line so far: **0**

  Nothing is graded yet — a closing line only exists once an event starts. This section will fill in on its own, and we publish it whichever way it goes.

## Known limits — stated, not hidden
- NFL only so far; other leagues collect but are not tuned.
- Pregame only. No in-play pricing.
- Leader/laggard needs many hours of history; it currently reports nothing rather than guessing.
- Upstream feeds are public sportsbook client APIs. They can change or close without notice; there is no SLA behind them.