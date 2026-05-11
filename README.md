# NCUT-Thesis-2026

> 北方工业大学本科毕业设计(论文) LaTeX 模板（2026 届适用）

[![LaTeX](https://img.shields.io/badge/LaTeX-XeLaTeX-008080?logo=latex)](https://www.latex-project.org/)
[![License](https://img.shields.io/badge/License-LPPL%201.3c-blue.svg)](./LICENSE)

一套可直接通过**学校格式自动检测系统**的 LaTeX 模板，开箱即用，无需手动调字体字号。

---

## 特性

- ✅ 正文自动渲染页眉「北方工业大学本科毕业设计(论文)」+ 横线
- ✅ 章节标题使用 Times New Roman 字体（一级三号、二级四号、三级小四）
- ✅ 图题 / 表题小五 9pt，符合 GB/T 规范
- ✅ 参考文献单一类型标识（`[J]` / `[C]` / `[M]`）
- ✅ 基于 GB/T 7714-2015 的参考文献格式（数字 / 作者-年份 两种样式）
- ✅ 支持 XeLaTeX + BibTeX，跨平台（Windows / macOS / Linux）

---

## 快速上手

### 1. 下载模板

```bash
git clone https://github.com/SunYuQi123/NCUT-Thesis-2026.git
cd NCUT-Thesis-2026
```

### 2. 创建工程目录

将三个核心文件放到你的论文工程根目录：

```
你的论文工程/
├── main.tex                        # 基于 main-template.tex 修改
├── chinathesis.cls                 # 从本模板拷贝
├── chinathesis-numerical.bst       # 从本模板拷贝
├── chinathesis-authoryear.bst      # 从本模板拷贝
├── chapters/
│   ├── abstract.tex                # 中英文摘要
│   ├── chap01.tex                  # 绪论
│   ├── chap02.tex                  # ...
│   └── thanks.tex                  # 致谢
├── bibs/
│   └── refs.bib                    # 参考文献
└── figures/                        # 配图
```

### 3. 以 `main-template.tex` 为起点编写主文件

```latex
\documentclass[numerical]{chinathesis}

\title{你的论文题目}
\author{你的姓名}
\advisor{导师姓名}
\school{学院名称}
\major{专业}
\studentid{学号}
\date{2026}

\bibliographystyle{chinathesis-numerical}

\begin{document}

\frontmatter
\maketitle
\include{chapters/abstract}
\tableofcontents

\mainmatter
\pagestyle{main}        % ← 必须：启用正文页眉
\include{chapters/chap01}
\include{chapters/chap02}
% ... 其他章节

\bibliography{bibs/refs}
\include{chapters/thanks}

\end{document}
```

### 4. 编译

```bash
xelatex -interaction=nonstopmode main.tex
bibtex main
xelatex -interaction=nonstopmode main.tex
xelatex -interaction=nonstopmode main.tex
```

首次编译需运行 4 次以解析交叉引用、目录与参考文献。

---

## 编译环境

| 组件 | 版本 |
|------|------|
| TeX 发行版 | TeX Live 2022+ 或 MiKTeX |
| 编译引擎 | **XeLaTeX**（不支持 pdfLaTeX） |
| 参考文献 | BibTeX |
| 中文支持 | ctex + fontspec |

**一键编译脚本**（可选，需 `latexmk`）：

```bash
latexmk -xelatex main.tex
```

---

## 使用约定

模板已处理所有格式层面的规范，但写作时请遵守以下内容层面的约定：

| 约定 | ❌ 错误 | ✅ 正确 |
|------|--------|--------|
| 三级标题不含数学公式 | `\subsection{$z_{modal}$ 编码器}` | `\subsection{模态编码器（z-modal）}` |
| 图题/表题末尾不加句号 | `\caption{模型架构。}` | `\caption{模型架构}` |
| 中文段落使用全角标点 | `模型(本文)达到` | `模型（本文）达到` |
| 期刊条目补全字段 | `@article{... year={2025}}` | 必须含 `volume` 和 `pages` |

---

## 参考文献样式切换

模板内置两种样式，在 `\documentclass` 选项中切换：

```latex
% 数字引用 [1][2][3]（默认）
\documentclass[numerical]{chinathesis}
\bibliographystyle{chinathesis-numerical}

% 作者-年份引用 (Smith, 2023)
\documentclass[authoryear]{chinathesis}
\bibliographystyle{chinathesis-authoryear}
```

---

## 仓库结构

```
NCUT-Thesis-2026/
├── README.md                       # 本文件
├── LICENSE                         # LPPL 1.3c 许可协议
├── .gitignore                      # LaTeX 构建产物忽略规则
├── main-template.tex               # 主文件模板（起步用）
├── chinathesis.cls                 # 论文文档类
├── chinathesis-numerical.bst       # 数字引用样式
└── chinathesis-authoryear.bst      # 作者-年份引用样式
```

---

## 常见问题

**Q: 编译报错 `Missing fancyhdr.sty`？**  
A: 执行 `tlmgr install fancyhdr` 或更新 TeX 发行版。

**Q: 页眉没出现？**  
A: 检查 `main.tex` 的 `\mainmatter` 下方是否写了 `\pagestyle{main}`。

**Q: 中文字体乱码或缺失？**  
A: 确保使用 XeLaTeX 编译，且系统安装了宋体/黑体。Windows 自带，macOS/Linux 需额外安装。

**Q: 参考文献有多个类型标识 `[A][M][C]`？**  
A: 确认你用的是本仓库的 `chinathesis-numerical.bst`，而非其他同名文件。

---

## 许可协议

本模板基于 [LaTeX Project Public License (LPPL) 1.3c](./LICENSE) 分发。

你可以：
- ✅ 用于自己的学位论文
- ✅ 修改后继续传播
- ✅ 基于本仓库 fork 维护

---

## 反馈

欢迎通过 [Issue](https://github.com/SunYuQi123/NCUT-Thesis-2026/issues) 反馈 bug 或格式问题，提交时请附上：
1. TeX 发行版与版本
2. 完整错误日志（`main.log`）
3. 学校格式检测报告截图（如有）
