# Product proof report
_Generated 2026-09-11 14:25 UTC from live data — last 24h_

## Collection health
- collection runs: **1426 total, 1213 ok, 212 failed** (85% uptime)
- prices collected: **169,633** across **92** events
- snapshots: **2906** over **965 minutes** of observation
  - DAZN Bet (altenar): 70 events, 49,060 prices
  - BetMGM (entain): 32 events, 62,307 prices
  - bwin (entain): 14 events, 14,998 prices
  - BetRivers (kambi): 62 events, 32,881 prices
  - NEO.bet (neo): 33 events, 3,295 prices
  - Pinnacle (pinnacle): 32 events, 7,092 prices

## Independence — the thing that makes the consensus mean anything
- exact markets priced by **all 5** engines: **230**
- exact markets priced by 2 or more engines: **4,973**
- measured pairwise price agreement (identical price on the same exact bet):

  | pair | shared markets | identical |
  |---|---:|---:|
  | betmgm vs bwin | 2,322 | 96.2% |
  | betrivers_on vs bwin | 2,320 | 10.4% |
  | bwin vs neobet | 627 | 10.2% |
  | betmgm vs betrivers_on | 3,044 | 10.1% |
  | betmgm vs neobet | 679 | 9.9% |
  | betrivers_on vs neobet | 744 | 9.4% |
  | betrivers_on vs dazn_bet | 2,146 | 2.6% |
  | dazn_bet vs neobet | 530 | 2.5% |
  | betmgm vs dazn_bet | 2,110 | 2.0% |
  | betrivers_on vs pinnacle | 1,298 | 2.0% |
  | bwin vs dazn_bet | 1,562 | 1.9% |
  | betmgm vs pinnacle | 1,064 | 1.4% |
  | bwin vs pinnacle | 756 | 1.1% |
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
- observed window: **965 minutes**, 2906 snapshots
- unbiased (randomised collection order): **887 minutes**

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
  | kambi → entain | 69 | 58.0% | polling artifact |
  | entain → altenar | 261 | 57.9% | weak |
  | altenar → kambi | 25 | 52.0% | polling artifact |
  | neo → pinnacle | 4 | 50.0% | polling artifact |
  | pinnacle → altenar | 22 | 45.5% | noise |
  | pinnacle → entain | 88 | 42.0% | noise |
  | altenar → entain | 206 | 36.9% | polling artifact |
  | entain → kambi | 83 | 28.9% | polling artifact |

**Rates move as samples grow. entain->altenar read 60.0% at n=160 and 53.8% at n=325 on the same unbiased data - regression to the mean, not a signal. Treat any relationship here as provisional until its sample is several hundred paired moves.**

We publish the rejections beside the survivor. A product built to find fake edges has no business hiding one of its own.

## What the gate rejected
- opportunities detected: **451**
- passed clean (zero warnings): **93**
- flagged or withheld: **358** (79% of everything found)
- rated high confidence: **26**
- average quoted edge, clean rows: **0.78%**
- average quoted edge, flagged rows: **2.74%**

  The flagged rows carry the *larger* average edge. That is the entire point: in this dataset the biggest number is usually the biggest bug, and a product that ranks on edge alone sells you its own defects.

## Line shopping value
- comparable bets priced by 3+ engines, every price confirmed within **20 minutes** of the others: **2,101**
- best price vs the **median** price: **2.06%** — what shopping saves a typical bettor, and the figure we advertise
- best price vs the **worst** price: **4.83%** — the spread across the market, a different question

  These two get quoted interchangeably in this industry. They are not the same number and we keep them apart deliberately.
- largest: **Under 5.50** — 1.56 worst vs **3.40** at BetMGM (**+117.9%**)

## Book movement (stale-line detection)
- observed window: **965 minutes**, 2906 snapshots

  | book | engine | active bets | repriced | held | stale % |
  |---|---|---:|---:|---:|---:|
  | BetRivers | kambi | 3657 | 1970 | 1687 | 46.1% |
  | Pinnacle | pinnacle | 2421 | 1650 | 771 | 31.8% |
  | bwin | entain | 3421 | 2342 | 1079 | 31.5% |
  | BetMGM | entain | 4480 | 3167 | 1313 | 29.3% |
  | NEO.bet | neo | 1056 | 832 | 224 | 21.2% |
  | DAZN Bet | altenar | 2499 | 2080 | 419 | 16.8% |

## Closing-line value — the scoreboard we can be judged by

Everything above is a claim about the present. This is the one number that says whether those claims were right, and it is the only one a matching bug cannot fake into looking like profit: a mismatched market produces nonsense CLV exactly as readily as a nonsense edge, and both read as noise.

- opportunities logged and awaiting settlement: **655**
- graded against a closing line so far: **0**

  Nothing is graded yet — a closing line only exists once an event starts. This section will fill in on its own, and we publish it whichever way it goes.

## Known limits — stated, not hidden
- NFL only so far; other leagues collect but are not tuned.
- Pregame only. No in-play pricing.
- Leader/laggard needs many hours of history; it currently reports nothing rather than guessing.
- Upstream feeds are public sportsbook client APIs. They can change or close without notice; there is no SLA behind them.