# Findings

Checked 2026-10-02. Testnet-10 only. No wallet secrets are in this note.

## Before the top-up

A synced kaspad 2.1.0 node showed the treasury at 24.41431202 tKAS across the first 32 receive indexes. The main receive key held 1.69909802 tKAS in 12 coins. The second seat held 22.71521400 tKAS.

The same desk sender log had recorded 980,024.00330406 tKAS at 2026-10-01 23:07:09 UTC, 105,237.11301968 tKAS at 2026-10-02 00:25:17 UTC, and 550.07616450 tKAS at 2026-10-02 00:33:11 UTC. Those hops pay the same wallet, so the missing testnet value left as fees.

A controlled ramp (2,000 coins of about 300 tKAS, then 10 to 200 tx/s) was not started. The live balance was already under the 100,000 tKAS reserve that ramp required.

## After the top-up

The mass sender was still running and had started cutting the new coins into lanes. It was stopped so this match run could use the coins.

A later synced read, still kaspad 2.1.0 on testnet-10, showed:

- Main receive key: 14,759 coins, 2,985,029.51770311 tKAS, largest 240.67272792 tKAS.
- Second seat: 23 coins, 22.715214 tKAS, largest 0.997727 tKAS. None of those coins can pay a 1.5 tKAS join.

The priority feerate was moving quickly while the mass sender stopped. One quote was about 11,217 sompi/gram. The successful seat fund below was quoted at 100 sompi/gram.

## Seat fund

The first launch connected at virtual DAA 585931091 and priority about 1,149 sompi/gram, so the threefold seat rate was 3,447. It picked the smallest coin that could cover 12 tKAS. That coin was about 12.58 tKAS. At that rate the storage-heavy shape has mass 80,752 and the fee does not fit, so the node SDK returned "Insufficient funds" and no game was sent.

The retry uses one of the largest coins. It connected at virtual DAA 585932973, priority 100 sompi/gram, seat rate 300 sompi/gram. The 12 tKAS seat fund was accepted on the first attempt: mass 2,036, fee 610,800 sompi. That is the same mass and fee as the 1 Oct 2026 seat fund at this rate.

## Slate

Ten hosted games are in progress: four First, three Second, three Draw, then exit-leaf claims. Carrier transactions stay on the encoder floor. This note will be updated when that slate finishes.

The mass sender is held off for this run. One other desk session removed the stop file and started it again after the top-up. It was stopped again before the accepted seat fund.
