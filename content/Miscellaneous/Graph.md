---
title: Graph
---

```mermaid
graph LR
      a1[Attacker Logs In] --> a2[Attacker Attacks] --> a3[Attacker Logs Out];
      a1 -.-> s1[Script: Create Recycle Cronjob];
      a3 -.-> s2[Script: Call Recycle Script];
      s1 -.-> s3[Recycle Script: Destroy / Create New Honeypot, Remove Cronjob];
      s2 -.-> s3;
```