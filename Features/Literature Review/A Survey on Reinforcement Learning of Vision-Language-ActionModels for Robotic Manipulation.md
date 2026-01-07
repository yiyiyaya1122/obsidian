---
type: paper
title: A Survey on Reinforcement Learning of Vision-Language-ActionModels for Robotic Manipulation
year: "2025.12"
authors: Haoyuan Deng∗ , Zhenyu Wu∗ , Haichao Liu∗ , Wenkai Guo, Yuquan Xue, Ziyu Shan, Chuanrui Zhang, Bofang Jia,Yuan Ling, Guanxing Lu, and Ziwei Wang
url:
tags:
  - paper
  - review
---
# ❓ 为什么要研究该领域（动机 / 目的）

> [!NOTE] Note
> - **核心问题**：这个领域要解决什么？
> - **研究价值**：为什么现在要研究这个？
> - **不研究的后果**：会卡在哪里？

- 现有 **预训练 VLA** 依赖模仿学习（IL），在真实世界部署时 **OOD 泛化能力不足**
- 真实环境中的状态 / 动作空间远超数据集覆盖范围
- **强化学习（RL）** 通过自探索和结果驱动优化，有潜力弥补 IL 的泛化缺陷
- 核心目标：**打通「大规模预训练 → 真实世界部署」之间的鸿沟**


---
## 🧠 这篇综述做了什么（工作内容）

> [!NOTE] Note
> - 梳理了哪些方向 / 任务？
> - 对比了哪些方法 / 维度？
> - 给出了哪些总结或观点？
 
- 系统性梳理 **RL-VLA 训练范式**，作为连接预训练与部署的关键桥梁
- 总结 RL 在提升 VLA **OOD 泛化能力** 中的作用机制
- 覆盖从模型设计、训练方式到真实世界部署的**完整生命周期**
- 讨论评测方法、开放挑战以及通向**通用机器人系统**的路径


---
## 🧩 领域分类与代表性工作

Existing **RL-VLA training paradigms** can be categorized into three types based on the way agents obtain and utilize feedback from the environmen.

| 类别                   | 分类依据                                                                               | 代表工作                                                            | 优缺点 |
| -------------------- | ---------------------------------------------------------------------------------- | --------------------------------------------------------------- | --- |
| **Online RL-VLA**    | involves the direct interaction with the environment during training               | VLA-RL,SimpleVLA-RL,FLaRe                                       |     |
| **Offline RL-VLA**   | focuses on learning from static datasets without further environmental interaction | ReinboT , ConRFT , CO-RFT , $\pi_{0.6}^{*}$, NORA-1.5, RESample |     |
| **Test-time RL-VLA** | adapt their behavior during deployment without altering their parameters           | V-GPS, Hume,STRAP, RA-DT, ReSA                                  |     |

---
## 🧠 我的思考与总结

- **我真正学到的结构是**：
- **我认可 / 不认可作者的地方**：
- **如果让我选一条路线，我会选**：
