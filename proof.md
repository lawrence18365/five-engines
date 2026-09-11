# Product proof report
_Generated 2026-09-11 14:06 UTC from live data — last 24h_

## Collection health
- collection runs: **1413 total, 1200 ok, 212 failed** (85% uptime)
- prices collected: **162,048** across **92** events
- snapshots: **2778** over **946 minutes** of observation
  - DAZN Bet (altenar): 69 events, 47,836 prices
  - BetMGM (entain): 32 events, 58,709 prices
  - bwin (entain): 14 events, 14,998 prices
  - BetRivers (kambi): 62 events, 31,306 prices
  - NEO.bet (neo): 33 events, 3,215 prices
  - Pinnacle (pinnacle): 32 events, 5,984 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **230**
- exact markets priced by 2 or more engines: **4,965**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,322 | 96.2% |
  | betrivers_on vs bwin | 2,320 | 10.6% |
  | bwin vs neobet | 627 | 10.5% |
  | betmgm vs neobet | 679 | 10.2% |
  | betmgm vs betrivers_on | 3,044 | 10.1% |
  | betrivers_on vs neobet | 744 | 9.4% |
  | betrivers_on vs dazn_bet | 2,138 | 2.6% |
  | dazn_bet vs neobet | 530 | 2.5% |
  | betrivers_on vs pinnacle | 1,296 | 2.2% |
  | betmgm vs dazn_bet | 2,106 | 2.0% |
  | bwin vs dazn_bet | 1,562 | 1.9% |
  | bwin vs pinnacle | 756 | 1.1% |
  | betmgm vs pinnacle | 1,062 | 1.1% |
  | dazn_bet vs pinnacle | 950 | 0.9% |
  | neobet vs pinnacle | 288 | 0.7% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | total | 4,387 | 1.93 | 614 | 692 |
  | spread | 3,974 | 1.94 | 583 | 821 |
  | team_total | 2,928 | 1.27 | 18 | 430 |
  | moneyline | 239 | 1.90 | 30 | 94 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **946 minutes**, 2778 snapshots
- unbiased (randomised collection order): **867 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | neo → altenar | 1 | 100.0% | insufficient sample |
  | pinnacle → kambi | 57 | 87.7% | polling artifact |
  | entain → neo | 7 | 71.4% | polling artifact |
  | kambi → pinnacle | 149 | 60.4% | polling artifact |
  | kambi → entain | 58 | 58.6% | polling artifact |
  | entain → pinnacle | 115 | 58.3% | weak |
  | entain → altenar | 242 | 55.4% | weak |
  | neo → pinnacle | 4 | 50.0% | polling artifact |
  | pinnacle → altenar | 22 | 45.5% | noise |
  | altenar → kambi | 22 | 45.5% | noise |
  | altenar → entain | 201 | 35.3% | polling artifact |
  | altenar → pinnacle | 12 | 33.3% | polling artifact |
  | pinnacle → entain | 67 | 32.8% | noise |
  | entain → kambi | 7 | 14.3% | polling artifact |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **453**
- passed clean (zero warnings): **103**
- flagged or withheld: **350** (77% of everything found)
- rated high confidence: **26**
- average quoted edge, clean rows: **0.64%**
- average quoted edge, flagged rows: **2.36%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **10 minutes** of the others: **2,096**
- best price vs the **median** price: **2.08%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.88%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **Los Angeles Rams -14.00** — 3.62 worst vs **4.60** at BetMGM (**+26.9%**)

## Book movement (stale-line detection)
- observed window: **946 minutes**, 2778 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 3479 | 1718 | 1761 | 50.6% |
  | Pinnacle | pinnacle | 2343 | 1589 | 754 | 32.2% |
  | bwin | entain | 3311 | 2342 | 969 | 29.3% |
  | BetMGM | entain | 4351 | 3093 | 1258 | 28.9% |
  | NEO.bet | neo | 1044 | 827 | 217 | 20.8% |
  | DAZN Bet | altenar | 2483 | 2077 | 406 | 16.4% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **632**
- graded against a closing line so far: **0**

  Nothing is graded yet — a closing line only exists once an event starts. This section will fill in on its own, and we publish it whichever way it goes.

## Known limits — stated, not hidden
- NFL only so far; other leagues collect but are not tuned.
- Pregame only. No in-play pricing.
- Leader/laggard needs many hours of history; it currently reports nothing rather than guessing.
- Upstream feeds are public sportsbook client APIs. They can change or close without notice; there is no SLA behind them.