# EEG 运动想象实验

这是一个基于 MNE、MOABB 和 scikit-learn 的 EEG 运动想象分类基线实验。实验使用 BNCI 2014-001 数据集，选取左手和双脚两类运动想象任务，使用 CSP + LDA 完成分类。

## 环境

建议使用 Python 3.10 或更高版本，并安装以下依赖：

```bash
pip install mne moabb scikit-learn pyriemann jupyter
```

当前实验环境中的主要版本为：

- MNE 1.12.1
- MOABB 1.5.0
- scikit-learn 1.9.0
- pyRiemann 0.12

## 运行

1. 启动 Jupyter Notebook：

   ```bash
   jupyter notebook
   ```

2. 打开 `motor_imagery_baseline.ipynb`。
3. 按顺序运行所有代码单元格。
4. 首次运行时，MOABB 会自动下载 BNCI 2014-001 数据集，请确保网络连接正常。

## 实验流程

1. 检查 MNE、MOABB、scikit-learn 和 pyRiemann 的版本。
2. 设置数据、临时文件和 Matplotlib 的保存目录。
3. 加载 BNCI 2014-001 数据集。
4. 选择第 1 个被试，以及 `left_hand` 和 `feet` 两类任务。
5. 对 EEG 数据进行以下处理：
   - 频带：8--30 Hz
   - 时间窗口：0.5--4.0 s
   - 重采样：128 Hz
6. 使用 CSP 提取空间特征，再通过线性判别分析（LDA）进行分类。
7. 使用 5 折分层交叉验证，并以 balanced accuracy 作为评价指标。

## 数据集信息

BNCI 2014-001 包含 9 名被试，任务标签包括：

- `left_hand`：左手运动想象
- `right_hand`：右手运动想象
- `feet`：双脚运动想象
- `tongue`：舌头运动想象

当前 notebook 的示例结果通常包含 288 个试次、22 个 EEG 通道和 449 个时间采样点，具体结果可能因数据版本和环境略有差异。

## 目录说明

```text
motor_imagery_baseline.ipynb  EEG 运动想象分类实验
README.md                     项目说明
```

## 注意事项

- Notebook 中的数据目录默认设置为 `F:\eeg_bci`。如果本机路径不同，请修改对应代码单元格中的 `base` 路径。
- Windows 环境下，代码对 MOABB 的路径处理进行了兼容设置；如果更换操作系统，可能需要调整这部分配置。
- `MNE_DATA`、`MOABB_DATA` 等环境变量应在加载和下载数据前设置。
- 首次下载数据可能需要较长时间，后续运行会直接使用本地缓存。
