# Product proof report
_Generated 2026-09-11 14:33 UTC from live data — last 24h_

## Collection health
- collection runs: **1432 total, 1219 ok, 212 failed** (85% uptime)
- prices collected: **171,949** across **92** events
- snapshots: **2949** over **971 minutes** of observation
  - DAZN Bet (altenar): 70 events, 49,440 prices
  - BetMGM (entain): 32 events, 62,864 prices
  - bwin (entain): 14 events, 15,845 prices
  - BetRivers (kambi): 62 events, 33,339 prices
  - NEO.bet (neo): 33 events, 3,369 prices
  - Pinnacle (pinnacle): 32 events, 7,092 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **230**
- exact markets priced by 2 or more engines: **4,973**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,324 | 100.0% |
  | betrivers_on vs bwin | 2,322 | 10.3% |
  | betmgm vs betrivers_on | 3,044 | 10.1% |
  | bwin vs neobet | 629 | 9.9% |
  | betrivers_on vs neobet | 744 | 9.5% |
  | betmgm vs neobet | 679 | 9.4% |
  | dazn_bet vs neobet | 530 | 2.6% |
  | betrivers_on vs dazn_bet | 2,146 | 2.6% |
  | betrivers_on vs pinnacle | 1,298 | 2.0% |
  | betmgm vs dazn_bet | 2,110 | 2.0% |
  | bwin vs dazn_bet | 1,564 | 1.8% |
  | betmgm vs pinnacle | 1,064 | 1.2% |
  | bwin vs pinnacle | 756 | 0.9% |
  | dazn_bet vs pinnacle | 952 | 0.7% |
  | neobet vs pinnacle | 288 | 0.7% |

  A pair near 100% is one trading desk wearing two logos and is counted once.

## Consensus depth — how many engines actually price each market
  | market | exact markets | avg engines | 4 or more | only 2 |
  |---|---:|---:|---:|---:|
  | total | 4,392 | 1.93 | 616 | 692 |
  | spread | 3,974 | 1.94 | 583 | 825 |
  | team_total | 2,928 | 1.27 | 20 | 428 |
  | moneyline | 239 | 1.90 | 30 | 94 |

  Five engines collect, but they do not all price the same lines. NEO posts spreads far more than totals; Altenar posts few moneylines. Most individual markets are therefore covered by two or three engines, not five. The confidence score already penalises thin coverage, and this table is here so the headline number is never read as if every row had five opinions behind it.

## Lead / lag between engines — tested, and NOT supported
- observed window: **976 minutes**, 2976 snapshots
- unbiased (randomised collection order): **894 minutes**

We looked for the most commercially attractive signal five independent engines could offer: does one desk move before another? Early results looked excellent — two relationships at 77-79% same-direction with p-values under 0.001.

**They were an artifact of our own collector.** Books were polled in a fixed order, so any price that moved between passes was timestamped in that order, and whichever book we happened to poll first appeared to lead every book polled later by exactly the polling gap. The tell was a relationship that hit 100.0% agreement at precisely the 47-second gap between two of our own requests.

Collection order is now randomised every pass, and lead/lag is computed **only** on data collected since. On that basis:

- nothing clears the sample and significance bar

  | pair | paired moves | same direction | verdict |
  |---|---:|---:|---|
  | neo → altenar | 1 | 100.0% | insufficient sample |
  | pinnacle → kambi | 83 | 88.0% | polling artifact |
  | entain → neo | 7 | 71.4% | polling artifact |
  | altenar → pinnacle | 25 | 68.0% | polling artifact |
  | entain → pinnacle | 142 | 64.1% | weak |
  | kambi → pinnacle | 189 | 62.4% | polling artifact |
  | entain → altenar | 261 | 57.9% | weak |
  | kambi → entain | 73 | 57.5% | polling artifact |
  | altenar → kambi | 25 | 52.0% | polling artifact |
  | neo → pinnacle | 4 | 50.0% | polling artifact |
  | pinnacle → altenar | 22 | 45.5% | noise |
  | pinnacle → entain | 93 | 41.9% | noise |
  | altenar → entain | 206 | 36.9% | polling artifact |
  | entain → kambi | 85 | 28.2% | polling artifact |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **463**
- passed clean (zero warnings): **94**
- flagged or withheld: **369** (80% of everything found)
- rated high confidence: **25**
- average quoted edge, clean rows: **0.84%**
- average quoted edge, flagged rows: **2.73%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **2,101**
- best price vs the **median** price: **2.08%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.84%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **Under 5.50** — 1.56 worst vs **3.40** at BetMGM (**+117.9%**)

## Book movement (stale-line detection)
- observed window: **971 minutes**, 2949 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 3718 | 2093 | 1625 | 43.7% |
  | bwin | entain | 3462 | 2342 | 1120 | 32.4% |
  | Pinnacle | pinnacle | 2435 | 1650 | 785 | 32.2% |
  | BetMGM | entain | 4527 | 3183 | 1344 | 29.7% |
  | NEO.bet | neo | 1063 | 850 | 213 | 20.0% |
  | DAZN Bet | altenar | 2519 | 2080 | 439 | 17.4% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **667**
- graded against a closing line so far: **0**

  Nothing is graded yet — a closing line only exists once an event starts. This section will fill in on its own, and we publish it whichever way it goes.

## Known limits — stated, not hidden
- NFL only so far; other leagues collect but are not tuned.
- Pregame only. No in-play pricing.
- Leader/laggard needs many hours of history; it currently reports nothing rather than guessing.
- Upstream feeds are public sportsbook client APIs. They can change or close without notice; there is no SLA behind them.