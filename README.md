# RABiTPy 复现项目

本仓库用于复现 Lund et al. (2025) 论文 "Genetic compatibility and ecological connectivity drive the dissemination of antibiotic resistance genes" 中的关键结果，包括主图 (Fig2-Fig5) 和补充图。

# 项目简介
本项目利用 RABiTPy (Rapid Artificially Intelligent Bacterial Tracker) 工具，对细菌运动视频进行自动化分析与统计，复现原论文中的关键数据图表。

# 项目结构

- `data_for_figures/`       # 存放用于生成图表的原始数据文件
- `report/`                 # HTML 格式的分析报告目录
  - `Main Results.html`     # 主要结果报告，包含关键指标和可视化
  - `Supp Results.html`     # 补充结果报告，包含附加分析和细节
- `results/`                # 最终导出的图像文件目录
- `supp_results/`           # 生成补充的结果
- `Main Results.ipynb`      # 生成主结果的 Jupyter 笔记本
- `Supp Results.ipynb`      # 生成补充结果的 Jupyter 笔记本
- `README.md`               # 说明文档

# 环境与依赖安装

### 1. 创建 Conda 环境
建议使用 Conda 管理环境，确保 Python 版本为 3.10。

## 创建名为 rabit_env 的环境
conda create -n rabit_env python=3.10 -y

## 激活环境
conda activate rabit_env


### 2. 安装 RABiTPy 及依赖
由于原项目基于 RABiTPy，需要安装该包及其依赖（如 Omnipose）。

## 安装 RABiTPy 核心包
pip install RABiTPy

## 安装依赖项 Omnipose (用于图像分割)
pip install git+https://github.com/kevinjohncutler/omnipose.git@6304051af0d52174dee7ff18e

## 需要从源码安装最新版 RABiTPy 
 pip install git+https://github.com/indraneel207/RABiTPy.git


# 复现简要过程

### 1. 准备数据与视频
将细菌运动视频（`sample.avi`）放入项目根目录或指定路径。
复现要使用原始论文数据，将 `data_for_figures` 文件夹放置在项目根目录。

### 2. 运行分析代码 (Jupyter Notebook)
使用 Jupyter Lab 运行。

- 打开 `Main Results.ipynb` 和 `Supp Results.ipynb`。
- 确保右上角的内核选择为 `rabit_env` (Jupyter Kernel)。
- 按顺序一步步运行代码块（Code Cell）。
  - 代码包含：加载视频 (`capture.load_video`)、处理帧、初始化识别对象、应用灰度/算法阈值等。
  - 分析结果将自动保存在 `results/` 和 `supp_results/` 文件夹中。

### 3. HTML 文件的生成
运行完 Notebook 后，需要将 `.ipynb` 文件转换为 GitHub 支持预览的 HTML 格式。

打开终端 (Terminal / Anaconda Prompt)，进入项目目录：

# 切换到项目文件夹
cd path/to/your/project_folder

# 使用命令转换为 HTML 文件
jupyter nbconvert --to html "Main Results.ipynb"
jupyter nbconvert --to html "Supp Results.ipynb"

转换后的文件将保存在 `report/` 目录下，可以在 GitHub 仓库的 `report` 文件夹中直接点击预览。

## 复现过程中遇到的问题
- **网络问题**： `pip install` 过程中出现 `Read timed out` 报错，配置国内镜像源（如清华源）或重试。
- **依赖冲突**：出现包版本冲突，建议检查 `conda` 环境是否纯净，或在新的环境中重新安装。
