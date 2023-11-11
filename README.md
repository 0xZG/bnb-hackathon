# Crypto Rumble :raised_hands: BNB Hackathon - Istanbul

- Please check out our [demo](https://test.zypher.game/CryptoRumble/) (you'll need to connect your crypto wallet with opBNB testnet gas :wink:)

- Contracts:
  - CryptoRumble: [`0x0Aa4135c7FD955A1421A238343D506Ff4BF656EC`](https://testnet.opbnbscan.com/address/0x0Aa4135c7FD955A1421A238343D506Ff4BF656EC)
  - GameHub: [`0x81186bD20f466c50D71B990B2a59621B020C7d9A`](https://testnet.opbnbscan.com/address/0x81186bD20f466c50D71B990B2a59621B020C7d9A)

- Git repositories:
  - [Web front-end](https://github.com/0xZG/crypto-rumble-frontend)
  - [Smart Contracts & ZK Circuits](https://github.com/0xZG/crypto-rumble-core)

### Dataflow:

```mermaid
sequenceDiagram

box Off-chain
actor P as Players
participant VRF as VRF <br /> (Polyhedra)
end

box rgba(239,185,11,0.4) On-chain
participant Contract as Smart Contract <br /> (opBNB)
participant ZK as ZK Verifier
end

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
