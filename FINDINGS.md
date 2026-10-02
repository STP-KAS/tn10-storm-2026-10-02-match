# Findings

Checked 2026-10-02. Testnet-10 only. No wallet secrets and no addresses are in this note.

## Before the top-up

A synced kaspad 2.1.0 node showed the treasury at 24.41431202 tKAS across the first 32 receive indexes. The main receive key held 1.69909802 tKAS in 12 coins. The second seat held 22.71521400 tKAS.

The desk sender log recorded 980,024.00330406 tKAS at 2026-10-01 23:07:09 UTC, 105,237.11301968 tKAS at 2026-10-02 00:25:17 UTC, and 550.07616450 tKAS at 2026-10-02 00:33:11 UTC. Those hops pay the same wallet, so the missing testnet value left as fees.

The controlled ramp was not started then. The live balance was already under the 100,000 tKAS reserve.

## After the top-up

No local kaspad was listening. Public kaspad 2.1.0 nodes were synced to testnet-10. muon-10's mempool was about 34,000. vector-10 was about 146,000. proton-10, neutrino-10, and boson-10 were about 397,000. Sends use muon-10 only. A node at or above 92,000 mempool transactions is not used.

The new coins had already been cut into roughly 141,000 outputs. The largest was about 241 tKAS, so one input cannot be split into a fresh 300 tKAS output. The run moves existing coins of at least 50 tKAS onto 20 derived receive indexes, capped at 800,000 tKAS moved, and leaves at least 100,000 tKAS on the main key.

## This run

Resumed 2026-10-02 07:29:22 UTC on muon-10, kaspad 2.1.0, mempool 34,033, synced.

- Confirmed balance on the main key: 2,080,971.4416 tKAS in 140,931 coins.
- Already on the 20 working indexes: 1,589 coins, 392,503.8357 tKAS.
- Still to move: 411 coins. Projected total moved: 490,608.1500 tKAS. Left on the main key: 1,982,867.1274 tKAS.
- Fan-out fee tier: 100 sompi/gram. The first batches were accepted with no rejects.

An earlier fan-out in the same hour died after 628 accepts. This resume counts coins already on the working indexes and does not move them again.

After the new coins confirm, the schedule is 1-input 2-output hops between those 20 indexes:

- 10, 25, 50, 100, then 200 tx/s
- 5 minutes at each step
- the highest step at or above 95 percent accepted, with the node still synced, is held for 60 minutes

Stop if the node leaves testnet-10 or loses sync, if more than 10 percent are rejected across 2 minutes, if free disk falls under 10 GB, if fees would cross the 800,000 tKAS cap or the 100,000 tKAS reserve, or if muon-10's mempool reaches 92,000. Working outputs are then consolidated back to the main key.

The mass sender was stopped for this run so it would not spend the same coins. One other desk session has been clearing that stop and starting it again. It was stopped again at the resume above.

This note will be updated when the schedule finishes.
