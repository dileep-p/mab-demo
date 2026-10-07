# DRL Assignment I — Group 150
**Assignment Problem IV:** *A Survey on Practical Applications of Multi-Armed and Contextual Bandits*
Bouneffouf, D. & Rish, I. (2019). arXiv:1904.10040 · https://arxiv.org/abs/1904.10040
Learning Facilitator: Subash Arun

## Team & ownership
| Member | BITS ID | Paper sections owned | Evidence in this repo |
|---|---|---|---|
| Dhiraj Kumar | 2025AG05127 | Abstract, §1: objectives, MAB vs CMAB formal setting | `notes/dhiraj.md`, `screenshots/dhiraj_*` |
| Sreeram Thattat | 2025AG05125 | §1–2 algorithms: UCB1, Thompson Sampling, LinUCB | `bandit_demo.ipynb`, `figures/`, `notes/sreeram.md` |
| Dileep P | 2025AG05847 | §2 (2.1–2.9) & §3 (3.1–3.6): Tables 1 & 2, case studies | `notes/dileep.md`, `screenshots/dileep_*` |
| Sayli Vinod Patil | 2025AG05781 | §2.10, §3.7, §4: summary, future directions, limitations | `notes/sayli.md`, `screenshots/sayli_*` |

> Each member commits their own notes and screenshots from their own GitHub account, so the commit history shows individual contributions.

## Repository layout
```
bandit_demo.ipynb   # 3 experiments, one per survey setting (executed, outputs included)
figures/            # regret plots used in the slides
notes/              # one file per member (copy notes/TEMPLATE.md)
screenshots/        # highlighted paper pages, table comparisons, git history
requirements.txt
```

## Bandit demo: what we checked and the results
The survey is a literature review with no experiments of its own, so we ran simulations of the algorithms it reviews across its taxonomy of settings.

| # | Survey setting | Compared | Result (cumulative regret, lower = better) |
|---|---|---|---|
| 1 | Stationary MAB (5 Bernoulli arms, T = 10,000, 200 runs) | ε-greedy (ε=0.1), UCB1, Thompson Sampling | TS **54.7** · UCB1 **225.4** · ε-greedy **285.8**. UCB1 overtakes ε-greedy at around t ≈ 5,500 |
| 2 | Contextual MAB (d = 5, K = 5, T = 2,000, 50 runs) | LinUCB, UCB1 (context-blind), Random | LinUCB **12.5** · UCB1 **1043.2** · Random **1044.1** |
| 3 | Non-stationary MAB (best arm flips at t = 1,500) | TS vs Discounted TS (γ = 0.99) | Total: TS **448.2** vs D-TS **218.4**. Before the change: TS 18.7 vs D-TS 98.8 |

**Takeaways**
1. UCB1 and TS (the survey's two canonical families, §1) have sub-linear regret; ε-greedy's is linear. TS is best in practice.
2. When the best arm depends on context, a context-blind bandit is no better than random. This is why CMAB dominates Table 1.
3. Forgetting old evidence costs regret when the world is stable but is essential under drift. This supports the survey's call for non-stationary bandits (§2.10, §3.7).

## Reproduce
```bash
pip install -r requirements.txt
jupyter nbconvert --to notebook --execute bandit_demo.ipynb   # ~15 s; seed = 150
```

## References
1. Bouneffouf, D., & Rish, I. (2019). A Survey on Practical Applications of Multi-Armed and Contextual Bandits. arXiv:1904.10040.
2. Auer, P., Cesa-Bianchi, N., & Fischer, P. (2002). Finite-time analysis of the multiarmed bandit problem. *Machine Learning*, 47, 235–256.
3. Agrawal, S., & Goyal, N. (2012). Analysis of Thompson Sampling for the multi-armed bandit problem. *COLT*.
4. Li, L., Chu, W., Langford, J., & Schapire, R. E. (2010). A contextual-bandit approach to personalized news article recommendation. *WWW*.
5. Chapelle, O., & Li, L. (2011). An empirical evaluation of Thompson Sampling. *NeurIPS*.
6. Raj, V., & Kalyani, S. (2017). Taming non-stationary bandits: A Bayesian approach. arXiv:1707.09727.

## Video
Presentation recording: <PASTE GOOGLE DRIVE LINK, shared as "Anyone with the link">
