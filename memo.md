# Recommendation to the Head of Strategy

**From:** Matías Mouat and María José López · **Topic:** rival pit-stop alert, Lab 3

**What the alert is for.** At the end of each lap, the alert says whether a rival driver is likely to pit in their next three laps. It could help the pit wall decide when to watch a rival closely or have an undercut or cover plan ready. It does not tell us when *we* should stop.

**How we tested it.** We trained on 2018–2021 races and checked on the first 11 races of 2022. In those races there were 370 rival pit stops. Every version was allowed to raise an alert on at most 1 in 10 laps checked (about 945 alerts), so they all had the same warning budget.

**What we found.**

| Version | Stops flagged in time | Alerts raised | Alerts that were right |
|---|---|---|---|
| Simple history table (tyre age, compound, track) | 94 of 370 | 931 | 27% |
| Current best model | 140 of 370 | 945 | 36% |
| Same model, one setting changed (our test) | **159 of 370** | 938 | **40%** |

A stop counts as "flagged in time" if the alert went off at least once in the three laps before it. Our change makes the model's rules less detailed, so it reacts less to one-off situations from past seasons. It flagged 19 more stops with slightly fewer alerts.

**Where it fails.** The clearest problem is hard tyres: 230 of 274 alerts on hard tyres were wrong (84%). The model sees an old hard tyre and expects a stop, but most of those drivers did not stop in the next three laps. It also missed every stop made on nearly new tyres, 5 laps old or less (49 of 49), and in one race (10 July 2022) it caught only 4 of 42 stops.

**Recommendation: check further, do not use in races yet.** The change is a clear improvement over the current model, but it still misses 211 of 370 stops (almost 6 in 10). The 2022 races were also used to set the alert level, so they are not a fully fair test. We cannot say anything about positions or time gained.

**Main limitation.** All results come from 11 races of rebuilt historical data. We do not know how the alert would behave with live timing delays, or at tracks where teams changed their usual strategy.

**Next check.** Run the frozen model, with its alert level fixed, once on later races it has never seen. Until then, only try it offline (for example replaying past races), and treat hard-tyre alerts with extra caution.
