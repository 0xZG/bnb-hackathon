# Crypto Rumble

```mermaid
sequenceDiagram

actor P as Players
participant VRF as VRF <br /> (Polyhedra)
participant Contract as Smart Contract <br /> @opBNB
participant ZK as ZK Verifier

P ->> VRF: Request a new seed
VRF ->> P: seed + proof*1

P ->>+ Contract: Start new game with the seed and proof*1
Contract ->> ZK: verify the seed
ZK -->> Contract: verified
Contract ->>- P: Initial round

P ->> P: play locally
P -->> P: generate proof*2

P ->>+ Contract: Upload score with proof*2
Contract ->> ZK: verify the score
ZK -->> Contract: verified
Contract ->> Contract: Leaderboard
Contract -->- P: Done
```