# Cost optimization

> Failing to recognize the purpose of excess capacity, and then reducing it to save money, can create opportunities for cascade failures.

## Capacity planning

- forecast -> allocate -> approve -> deploy -> repeat
- monitor growth
- predict future demand
- plan for feature launchers

---
- perfkit benchmarker

---
- bulk use discounting/sustained use discounts
- committed use discounts
- preemptible VMs
- egress VM to VM in the same zone
    - 2Gbits/s cap per core (+2 for each core up to 16Gbits/s)
    - 0.5 vCPU or less get 1 Gbits/second cap
