【接力卡片 · 电商用户复购分析看板】

① 目标：可运行的 Streamlit 中文看板（用户行为 CSV → 复购分层 + 关键特征），含 README 与单测；AUC 指 5 折 CV 均值，需 >= 0.85

② 技术栈/环境：Python 3.11 + pandas + sklearn + streamlit + plotly + lightgbm（均已装）；目标机器离线。⚠ 优化器用 sklearn RandomizedSearchCV，不用 optuna（离线未装）

③ 已完成：
- 数据清洗 → ./data/clean.csv（8 万行，正负 9:1）
- 基线 AUC=0.81 → ./src/train.py
- EDA → ./notes/eda.md

④ 决策（不可删）：
- LightGBM 而非 XGBoost → CV 高 0.02 且更快
- 复购口径=90 天内下单>=2 次 → 业务已确认
- 不存特征交叉 → 8 万样本下过拟合

⑤ 产物指针：./src/train.py（训练脚本，网格搜索在 _tune()）、./data/clean.csv、./notes/eda.md

⑥ 已知坑（不可删）：
- SMOTE 降 AUC 3 点 → 别再试
- 原始 timestamp 会数据泄漏 → 用相对天数

⑦ 待办：调参至 CV AUC>=0.85 / Streamlit 界面 / README+单测

⑧ 你现在要做的：用 sklearn RandomizedSearchCV 对 ./src/train.py 的 max_depth / n_estimators 做 30 次采样，替换 _tune() 中的 GridSearchCV

状态文件：HANDOFF.md（路径：./HANDOFF.md）｜last_updated：2026-11-17 08:30｜原 owner：豆包（工作模式）
