# Week 6 — Explain It Like You Built It
**Author:** Rafiul Islam  
**Track:** General AI Fluency  
**Assignment:** ML-09 — Explain It Like You Built It

---

## What I Learned: Feature Leakage in My FlyRank Model

In my FlyRank project I created a feature called `impression_momentum`, which was last 30 days impressions divided by the previous 30 days impressions. But I realized that when this value goes below 1, it means the page is declining — and that was exactly my label. So the model never actually learned anything from the other features, it just used this one shortcut. In real deployment this would be a problem because for new pages you can't know the last vs previous 30 day comparison in advance — so this feature can't be used at all.
