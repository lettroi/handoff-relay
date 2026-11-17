# 状态文件 · HANDOFF.md

last_updated: 2026-11-17 08:30
current_owner: 豆包（工作模式）
task: 电商用户复购分析看板

## goal（目标与验收标准，写清口径）
交付可运行的 Streamlit 中文看板：用户行为 CSV → 复购率分层 + 关键特征，含 README 与单元测试。验收口径：AUC 指 5 折 CV 均值（非单次切分），需 >= 0.85；单元测试覆盖复购率计算逻辑。

## stack（技术栈与环境，必须完整列出已装/可用工具）
- Python 3.11 + pandas + scikit-learn + streamlit + plotly + lightgbm（均已安装可用）
- 目标机器离线，不得引入需联网下载模型的依赖
- ⚠ 优化器改用 sklearn 内置 RandomizedSearchCV（已可用），不用 optuna（离线未安装）

## constraints（约束与偏好）
- 界面全中文，图表用 Plotly
- 不引入需联网下载模型的依赖

## decisions（已定决策，每条含理由）
- LightGBM 而非 XGBoost → 同数据 CV 高 0.02 且训练更快
- 复购定义为"90 天内下单 >= 2 次" → 业务方确认过口径
- 不存特征交叉 → 样本仅 8 万，交叉后过拟合

## progress（进度）
done:
- 数据清洗完成，缺失值中位数填充 → ./data/clean.csv
- 基线模型 AUC=0.81 → ./src/train.py
- EDA 结论 → ./notes/eda.md
in_progress:
- LightGBM 调参，卡在 max_depth 网格搜索太慢（单轮 3 分钟）
todo:
- 完成调参至 CV AUC >= 0.85
- 写 Streamlit 界面
- 写 README + 单元测试

## artifacts（产物索引，只写指针）
- ./data/clean.csv → 清洗后数据，8 万行，正负样本约 9:1
- ./src/train.py → 训练脚本，已含 LightGBM 与基线，网格搜索在 _tune() 函数
- ./notes/eda.md → EDA 发现（复购用户集中前 3 品类）

## gotchas（已知坑：失败路径 + 原因，全量记录不可删）
- SMOTE 过采样降 AUC 3 个点 → 已放弃，不要再试
- 原始 timestamp 做特征会数据泄漏 → 必须用相对天数

## next_action（下一步第一动作，具体到可执行）
用 sklearn RandomizedSearchCV 对 ./src/train.py 的 max_depth / n_estimators 做 30 次采样，替换 _tune() 中的 GridSearchCV

## handoff_log（交接记录）
- 2026-11-17 08:30 豆包 → 完成数据清洗与基线，调参未完成，额度将尽

## 接手须知（给下一位智能体）
1. 接手后第一件事：把 current_owner 改为你的名字、更新 last_updated，并在 handoff_log 追加一行。
2. 验收以 goal 中写明的 5 折 CV 均值口径为准，不要用单次切分。
3. 严禁重做 progress.done 事项、严禁推翻 decisions、严禁踩 gotchas。
