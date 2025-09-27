# Kronos Copilot Instructions

## 项目架构与主要组件
- Kronos 是面向金融市场K线（K-line）序列的基础模型，采用解码器结构，专为高噪声金融数据设计。
- 主要目录：
  - `model/`：核心模型代码（如 `kronos.py`、`module.py`）。
  - `finetune/`：微调、数据处理与训练脚本（如 `train_predictor.py`、`qlib_data_preprocess.py`）。
  - `webui/`：基于 Flask 的 Web UI，支持多种数据格式、设备和预测参数调整。
  - `examples/`：批量预测、无波动预测等示例脚本。

## 关键开发与运行流程
- **Web UI 启动**：
  - 推荐：`cd webui; python run.py` 或 `python app.py`，访问 http://localhost:7070
  - Linux/macOS 可用 `start.sh` 脚本
- **模型微调与训练**：
  - 参考 `finetune/train_predictor.py`、`finetune/train_tokenizer.py`，需先准备/预处理数据（见 `finetune/qlib_data_preprocess.py`）
- **批量预测**：
  - 参考 `examples/prediction_batch_example.py`，支持自定义数据与参数

## 项目约定与模式
- 数据格式以金融K线（如CSV、Feather）为主，时间窗口通常为400+120点
- 预测参数（如 temperature、top_p、sample_count）可通过 Web UI 或脚本灵活调整
- 训练与推理均支持多设备（CPU/CUDA/MPS）
- 结果输出统一为 JSON 或图表，存放于 `webui/prediction_results/`

## 依赖与集成
- 依赖见 `requirements.txt` 与 `webui/requirements.txt`
- 主要依赖：PyTorch、Flask、pandas、plotly 等
- 外部数据需放置于 `examples/data/` 或指定路径

## 重要文件参考
- `model/kronos.py`：模型主结构
- `finetune/train_predictor.py`：训练主入口
- `webui/app.py`、`webui/run.py`：Web UI 启动与路由
- `examples/prediction_batch_example.py`：批量预测范例

## 其他说明
- 遵循已有目录结构与命名规范，新增功能建议参考现有脚本风格
- 详细用法、参数说明见各目录下 README.md

---
如需补充项目约定或遇到不明确的开发流程，请优先查阅对应目录 README 或向维护者反馈。