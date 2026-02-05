<div align="center">
  <img src="https://img.shields.io/badge/Language-中文-red.svg" alt="中文">
  <img src="https://img.shields.io/badge/Language-English-blue.svg" alt="English">
  <img src="https://img.shields.io/badge/Language-Español-yellow.svg" alt="Español">
  <img src="https://img.shields.io/badge/Language-Português-green.svg" alt="Português">
  <img src="https://img.shields.io/badge/Model-SDTL-orange" alt="Model">
  <img src="https://img.shields.io/badge/Task-SOH_Estimation-blueviolet" alt="Task">
  
  <h1>📚 读书笔记：SDTL——基于自注意力机制深度迁移学习的锂电池 SOH 在线估计 </h1>
  <p>论文：Deep transfer learning enabled online state-of-health estimation of lithium-ion batteries under small samples across different cathode materials, ambient temperature and charge-discharge protocols</p>
  
  <div style="margin: 10px 0;">
    <a href="#readme" style="padding: 5px 10px; background: #333; border-radius: 4px; text-decoration: none; color: #fff; font-weight: bold;">简体中文</a> | 
    <a href="README_en.html" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px; text-decoration: none; color: #333;">English</a> | 
    <a href="README_es.html" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px; text-decoration: none; color: #333;">Español</a> | 
    <a href="README_pt.html" style="padding: 5px 10px; background: #f0f0f0; border-radius: 4px; text-decoration: none; color: #333;">Português</a>
  </div>
</div>

> **论文标题**：Deep transfer learning enabled online state-of-health estimation of lithium-ion batteries under small samples across different cathode materials, ambient temperature and charge-discharge protocols  
> **发表期刊**：Journal of Power Sources (2025, Vol. 650, 237503)  
> **核心方法**：SDTL (Self-attention-based Deep Transfer Learning)  
> **研究对象**：跨正极材料 (NCM/NCA)、跨温度、跨倍率的小样本 SOH 估计。

## 🔍 核心问题
锂离子电池的健康状态 (SOH) 估计在实际应用中面临以下挑战：
- **数据稀缺**：新电池或特定工况下的早期数据通常不足。
- **工况多变**：不同正极材料（如 NCM 和 NCA）、环境温度（如低温 $4^{\circ}C$）和充放电倍率导致电池老化模式差异巨大。
- **模型泛化性**：传统深度学习模型难以在未见过的工况下保持高精度，而重新训练模型成本高昂。

## 💡 方法论：SDTL 框架
论文提出了一种基于自注意力机制的深度迁移学习 (SDTL) 方法。该方法利用源域的大量历史数据进行预训练，并通过微调 (Fine-tuning) 快速适应仅有少量早期数据的目标域电池。

> 📊 **SDTL 方法框架图**
> ![SDTL Framework](assets/fig1.jpg)
> *该图展示了 SDTL 的整体流程：从不同工况的电池数据采集、健康因子 (HI) 提取与筛选，到源域模型的离线预训练，以及利用目标域前 10% 数据进行的在线微调与评估。*

### 关键技术细节
1.  **特征工程**：
    -   从电压、电流和增量容量 (IC) 曲线中提取了 18 个健康因子 (HIs)。
    -   通过皮尔逊相关系数 (PCC) 筛选出 3 个关键 HIs：恒流放电时间 (HI5)、电流熵 (HI17) 和电流斜率 (HI18)。
2.  **模型结构**：
    -   采用 **多头自注意力机制 (Multi-Head Self-Attention)** 捕捉时间序列中的长期依赖关系。
    -   引入位置编码 (Positional Encoding) 以保留序列信息。
3.  **迁移策略**：
    -   **预训练 (Pre-training)**：在源域数据上训练模型参数。
    -   **微调 (Fine-tuning)**：冻结除全连接层以外的网络层，仅使用目标电池前 10% 的数据更新输出层参数。

> 📊 **自注意力模型结构图**
> ![Model Structure](assets/fig5.jpg)
> *图示了基于自注意力的网络结构，包含位置编码、多头注意力模块、层归一化 (Layer Norm) 和前馈网络 (FFN)。*

## 📈 实验结果
研究在两个数据集（A系列 NCM 电池，B系列 NASA NCA 电池）上验证了模型，涵盖不同温度 ($24^{\circ}C, 4^{\circ}C$) 和倍率 (1C, 2C)。

- **精度表现**：相比于 Transformer 和 LSTM 基准模型，SDTL 在 RMSE 和 MAE 指标上均有显著降低。
- **少样本适应**：仅需目标电池 10% 的早期循环数据即可实现高精度的全寿命周期预测。
- **对比优势**：与领域自适应 (DAAP, DAAD) 等其他迁移学习方法相比，SDTL 在准确性和稳定性上表现更优。

> 📊 **SOH 估计结果可视化**
> ![Estimation Results](assets/fig8.jpg)
> *图 (a) 展示了 SDTL 在三个不同系列电池上的估计效果；图 (b) 重点展示了在低温 ($4^{\circ}C$) 工况下的拟合情况；图 (c) 为误差分布对比。*

## 📚 参考资料
- **引用格式**: X. Li, M. Zhao*, S. Zhong, J. Li, S. Fu, Z. Yan. Deep transfer learning enabled online state-of-health estimation of lithium-ion batteries under small samples across different cathode materials, ambient temperature and charge-discharge protocols[J]. Journal of Power Sources, 2025, 650: 237503.
- **数据来源**: 自测 NCM 电池数据集与 NASA Prognostics Repository (NCA)。

<br>

<div align="center">
  <p>© 2026 技术博客笔记 | 论文来源：<a href="https://doi.org/10.1016/j.jpowsour.2025.237503">Journal of Power Sources</a></p>
  <br>
  <a href="#readme">简体中文</a> | 
  <a href="README_en.html">English</a> | 
  <a href="README_es.html">Español</a> | 
  <a href="README_pt.html">Português</a>
</div>
