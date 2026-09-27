# DSCI 521 Milestone 3 任务清单

> 用途：把官方 Milestone 3 要求拆成可以逐项确认的工作清单。
> 
> 官方要求：<https://ubc-mds.github.io/DSCI_521_platforms-dsci/assignments/milestone3.html>
> 
> 官方标题：**Reproducible environments and two computational posts**。
> 本 Milestone 总分 **35 分**；另有可选 **+5 分 bonus**。

## 一、目标和范围

Milestone 3 是在 Milestone 2 网站的基础上继续完成，不是重新做一个独立项目。最终仓库需要满足：

1. 网站中有两个新的 computational posts：一个使用 R，一个使用 Python。
2. 两种语言各有一个可复现、已锁定依赖版本的环境。
3. 陌生人从 GitHub clone 仓库后，可以按照 `README.md` 的说明重新渲染整个网站。
4. GitHub Pages 上的 live site 可访问，页面、导航、图片、代码、输出都正常。
5. 按要求将仓库 URL 和网站 URL 提交到 Gradescope。

分析主题可以相同，也可以不同；重点不是分析有多复杂，而是分析确实执行、环境可复现、读者能理解。

---

## 二、任务 1：规划两个 computational posts

### 2.1 为每篇 post 选题和数据

- [ ] 选择一个 R post 的分析主题和数据集。
- [ ] 选择一个 Python post 的分析主题和数据集。
- [ ] 每篇 post 都有明确的问题、数据处理/分析步骤和结果解释。
- [ ] 每篇 post 放在独立目录中，目录格式为：

  ```text
  posts/<short-name>/index.qmd
  ```

- [ ] 目录名使用小写、连字符、无空格。
- [ ] 先完成数据许可检查，再把数据文件放入公开仓库。

### 2.2 检查数据来源和公开许可

对每个数据集：

- [ ] 在对应 post 的正文中明确写出数据来自哪里。
- [ ] 在正文中提供数据来源链接；不能只写在 `README.md` 或代码注释中。
- [ ] 查明数据集的许可证或使用条款。
- [ ] 确认允许将数据文件重新发布到公开 GitHub 仓库。
- [ ] 如果许可证要求署名或特定引用，按要求署名/引用。
- [ ] 提交到仓库的数据文件大小约小于 **5 MB**。
- [ ] 如果不能公开提交数据文件，改为在渲染时从 URL 读取，并在 `README.md` 中说明：构建需要网络，而且依赖该数据托管地址可用。
- [ ] 不使用需要登录、API key 或 token 的数据源。

可以使用包内数据集，例如 R 的 `palmerpenguins`、`gapminder`、`mtcars`、`iris`，或 Python 的 `palmerpenguins`、scikit-learn bundled datasets。注意：`seaborn.load_dataset()` 每次会联网下载，不能当作完全本地的内置数据集处理。

---

## 三、任务 2：建立 Python 可复现环境（4 分）

环境文件放在仓库顶层，与 `_quarto.yml` 同级；不能在每个 post 内单独建立环境。

### 3.1 创建和配置环境

- [ ] 顶层存在 `pyproject.toml`。
- [ ] 顶层存在 `uv.lock`。
- [ ] 顶层存在 `.python-version`。
- [ ] 使用 `uv` 管理 Python 环境和依赖。
- [ ] `jupyter` 和 `ipykernel` 已加入环境；Quarto 的 Python chunk 需要对应的 Jupyter kernel。
- [ ] Python post 所有实际 import 的包都已加入 `pyproject.toml` 和 `uv.lock`。
- [ ] `uv.lock` 已在新增或修改依赖后重新生成/同步。

官方建议的起点：

```bash
uv init --bare
uv python pin 3.14
uv add jupyter ipykernel
# 再加入 post 实际需要的包，例如：
uv add pandas altair
```

### 3.2 确认 Quarto 使用正确 Python

- [ ] 从仓库顶层执行渲染，而不是在 post 子目录中执行。
- [ ] 使用以下方式渲染 Python 内容：

  ```bash
  uv run quarto render
  ```

- [ ] 在 Python chunk 中检查过 `sys.executable`；路径应指向当前仓库 `.venv` 中的 Python。
- [ ] `.venv/` 不提交到 GitHub。

---

## 四、任务 3：建立 R 可复现环境（4 分）

环境文件同样放在仓库顶层。

### 4.1 创建和锁定环境

- [ ] 顶层存在 `renv.lock`。
- [ ] 顶层存在 `.Rprofile`。
- [ ] 顶层存在 `renv/activate.R`。
- [ ] 顶层存在 `renv/` 目录。
- [ ] 已从仓库顶层的 R session 执行 `renv::init()`。
- [ ] 已安装 R post 实际需要的包。
- [ ] 已执行 `renv::snapshot()`。
- [ ] `renv.lock` 列出了 R post 所有实际使用的包。
- [ ] 没有把本地 R library 或 `renv/library` 提交到 GitHub。

关键点：不需要手动激活环境。只要从仓库顶层运行 Quarto，R 会读取 `.Rprofile` 并启用 `renv`。

---

## 五、任务 4：完成 R computational post（7 分）

在 `posts/<r-post-name>/index.qmd` 中完成：

- [ ] YAML header 至少包含 `title`、`author`、`date`。
- [ ] 正文明确说明数据来源，并包含可点击链接。
- [ ] 至少有 **3 个真正做分析工作的代码 chunk**。
- [ ] `library()` 或 import 单独不算分析 chunk。
- [ ] 代码至少完成实际的数据读取、整理、计算、统计分析或可视化等工作。
- [ ] 至少有一个由代码生成的 figure 或 table。
- [ ] 有 prose 解释做了什么、得到什么结果、结果意味着什么。
- [ ] 渲染页面同时显示代码和代码输出。
- [ ] 不是把预先生成的图片截图贴到页面上冒充计算结果。
- [ ] 使用 Quarto 的 `#|` chunk-option 写法，不使用旧的 inline `{r, ...}` 方式。
- [ ]（建议）本篇至少有一个 figure 使用 label 和 caption；官方最低线是两篇 post 合计至少有一个带 label 和 caption 的 figure，例如：

  ```r
  #| label: fig-example
  #| fig-cap: "图表说明。"
  ```

- [ ]（建议）本篇至少有一个 chunk 有目的地使用 `message` 或 `warning` 选项控制输出噪声。官方最低线是两篇 post 合计至少有一个这样的 chunk，例如 setup chunk：

  ```r
  #| message: false
  #| warning: false
  ```

- [ ] 对应 R 依赖都已写入 `renv.lock`。

---

## 六、任务 5：完成 Python computational post（7 分）

在 `posts/<python-post-name>/index.qmd` 中完成：

- [ ] YAML header 至少包含 `title`、`author`、`date`。
- [ ] 正文明确说明数据来源，并包含可点击链接。
- [ ] 至少有 **3 个真正做分析工作的代码 chunk**。
- [ ] import 单独不算分析 chunk。
- [ ] 代码至少完成实际的数据读取、整理、计算、统计分析或可视化等工作。
- [ ] 至少有一个由代码生成的 figure 或 table。
- [ ] 有 prose 解释做了什么、得到什么结果、结果意味着什么。
- [ ] 渲染页面同时显示代码和代码输出。
- [ ] 不是把预先生成的图片截图贴到页面上冒充计算结果。
- [ ] 使用 Quarto 的 `#|` chunk-option 写法。
- [ ] 至少有一个 figure 使用 label 和 caption，例如：

  ```python
  #| label: fig-example
  #| fig-cap: "图表说明。"
  ```

- [ ] 两篇 post 合计至少有一个 chunk 有目的地使用 `message` 或 `warning` 选项；更稳妥的做法是两篇各自都明确使用一次。
- [ ] 对应 Python 依赖都已写入 `pyproject.toml` 和 `uv.lock`。

---

## 七、任务 6：更新 `README.md`（6 分）

`README.md` 是本 Milestone 的正式交付物。它要让“只有仓库、没有其他上下文的人”完成构建。

### 6.1 项目说明

- [ ] 用一两句话说明这个仓库是什么、网站是什么。

### 6.2 前置软件和版本

- [ ] 列出需要事先安装的软件。
- [ ] 至少说明 Quarto、`uv`、R 的版本或兼容要求。
- [ ] 说明 `renv` 如何获得/启动；不把未记录的本地状态当作前置条件。

### 6.3 从 clone 到渲染的完整命令

- [ ] 写出从 `git clone` 开始的命令。
- [ ] 命令按实际执行顺序排列。
- [ ] 每条命令都可以复制粘贴。
- [ ] 说明 shell 命令和 R 命令分别在哪里执行。
- [ ] 说明必须从仓库顶层执行 `quarto render`。
- [ ] 说明 Python 环境如何同步，例如 `uv sync`。
- [ ] 说明 R 环境如何恢复，例如 `renv::restore()`（如果采用该流程）。
- [ ] 写出实际渲染命令：Python 环境至少应覆盖 `uv run quarto render` 的使用方式。

### 6.4 构建结果和数据说明

- [ ] 说明渲染的网站输出在哪里；本项目应为 `docs/`。
- [ ] 说明如何在本地打开或预览构建结果。
- [ ] 列出两个 post 的数据来源。
- [ ] 明确构建是否需要网络。
- [ ] 如果渲染时从 URL 下载数据，明确写出网络依赖和数据地址。

### 6.5 从干净 clone 实测

- [ ] 在另一个临时目录重新 clone 仓库。
- [ ] 不依靠记忆、IDE 自动配置或原目录残留文件。
- [ ] 严格逐行执行 `README.md` 的命令。
- [ ] 成功生成完整 `docs/` 网站。
- [ ] 将实测中遇到的缺失步骤补回 `README.md`。

示例测试起点：

```bash
git clone git@github.com:username/username.github.io.git ~/tmp/m3-test
cd ~/tmp/m3-test
```

---

## 八、任务 7：清理网站和仓库（2 分中的网站部分）

以下检查要在 live site 和 GitHub 仓库上完成，不只看本地 preview。

### 8.1 live site

- [ ] 所有 navbar 链接都能打开。
- [ ] 所有图片都能加载。
- [ ] Blog listing 包含所有 posts，并按日期倒序排列。
- [ ] 两篇新 post 都能从 Blog 页面打开。
- [ ] 没有 broken internal links。
- [ ] 没有 Quarto 模板残留文本，例如 starter “About this site”。
- [ ] Home page 和 About page 仍然内容完整、可读。
- [ ] 两篇 computational post 的代码和输出在 live site 上都可见。
- [ ] 图表和 caption 在 live site 上都出现。

### 8.2 GitHub 仓库

- [ ] `docs/.nojekyll` 存在并已提交。
- [ ] `.quarto/` 不在 GitHub 上。
- [ ] `_site/` 不在 GitHub 上。
- [ ] `.DS_Store` 不在 GitHub 上。
- [ ] `.venv/` 不在 GitHub 上。
- [ ] `renv/library` 不在 GitHub 上。
- [ ] 顶层有 `.gitignore`，至少忽略：

  ```gitignore
  .quarto/
  _site/
  .DS_Store
  .venv/
  ```

- [ ] 如果这些目录已经被 Git 跟踪，仅添加 `.gitignore` 不够；必须停止跟踪并提交修改。
- [ ] 仓库仍然是 Public。
- [ ] 仓库中没有 token、API key、密码或其他私人信息。

---

## 九、任务 8：渲染、提交和 GitHub Pages 检查

### 8.1 正确渲染顺序

从仓库顶层执行：

```bash
uv run quarto render
git status
git add .
git commit -m "milestone 3"
git push origin main
```

如果项目采用手动创建 `.nojekyll` 的方式，要确认每次渲染后 `docs/.nojekyll` 仍然存在。

- [ ] 本地完整渲染成功。
- [ ] `docs/` 中包含更新后的首页、About、Blog 和所有 posts。
- [ ] 检查 `git status`，没有把禁止提交的文件加入暂存区。
- [ ] push 后检查 GitHub 上实际存在的文件，而不是只检查本地文件。

### 8.2 GitHub Pages 和 live site

- [ ] GitHub Pages 的 Source 为 `Deploy from a branch`。
- [ ] Branch 为 `main`。
- [ ] Folder 为 `/docs`。
- [ ] 等待 GitHub Pages 构建完成。
- [ ] 打开 live site：`https://username.github.io`。
- [ ] 在 private/incognito window 中再次检查，确认不依赖登录状态或本地缓存。
- [ ] 点击 Home、About、Blog、两篇新 post，并检查图片、代码、输出和图表。

### 8.3 Git 提交历史

- [ ] 整个 Milestone 至少有 **5 个 commits**。
- [ ] 不要只在最后做一个大 commit。
- [ ] 提交历史能够反映逐步完成网站、环境、post、README 和渲染检查的过程。

---

## 十、任务 9：制作提交 PDF（2 分中的提交部分）

制作一个 PDF，包含以下两个 URL：

1. GitHub 仓库 URL：

   ```text
   https://github.com/username/username.github.io
   ```

2. live website URL：

   ```text
   https://username.github.io
   ```

- [ ] 两个 URL 都指向 `github.com` / live GitHub Pages，而不是 `github.ubc.ca`。
- [ ] PDF 已上传到 Gradescope。
- [ ] 提交前确认两个 URL 在 private/incognito window 中可访问。

---

## 十一、可选 Bonus：一个 post 同时运行 R 和 Python（+5 分）

这部分不是完成基本 Milestone 3 的必需项。

- [ ] 新增第三篇 post。
- [ ] 同一份 `.qmd` 中同时运行 R 和 Python。
- [ ] 使用 `reticulate`。
- [ ] R 和 Python 之间实际传递对象：例如 Python 读取 R 对象，或 R 读取 Python 对象。
- [ ] `reticulate` 已加入 `renv.lock`。
- [ ] 已正确让 `reticulate` 使用本项目的 `.venv`。
- [ ] 从 clean clone 按自己的 `README.md` 能成功渲染 bonus post。
- [ ] 在 Gradescope PDF 中加入 bonus post 的**单独 URL**，必须直接打开该 post，不能只放仓库 URL 或首页 URL。
- [ ] 在 PDF 中写明这 5 分要计入哪个 assignment，例如：`Apply the bonus to Milestone 2.`
- [ ] 5 分只能全部计入一个 assignment，不能拆分；任何 assignment 不能超过 100%。

---

## 十二、按评分表核对（35 分）

| 项目 | 分值 | 完成 |
|---|---:|:---:|
| Python post：真实分析、live site 上可见代码和输出、数据来源说明 | 7 | [ ] |
| R post：真实分析、live site 上可见代码和输出、数据来源说明 | 7 | [ ] |
| 两篇 post 有目的地使用 chunk options | 3 | [ ] |
| Python 环境：`pyproject.toml`、`uv.lock`、`.python-version` 完整 | 4 | [ ] |
| R 环境：`renv.lock`、`.Rprofile`、`renv/activate.R` 完整 | 4 | [ ] |
| `README.md`：可从 clean clone 执行的构建说明 | 6 | [ ] |
| 网站清理：导航、链接、图片、无模板残留文本 | 2 | [ ] |
| live GitHub Pages、至少 5 个 commits、Gradescope 提交两个 URL | 2 | [ ] |
| **总分** | **35** | [ ] |

---

## 十三、最终总检查

提交前逐项确认：

- [ ] 两篇新 computational posts：一篇 R，一篇 Python。
- [ ] 每篇至少 3 个有效分析 chunk。
- [ ] 每篇至少一个代码生成的 figure 或 table。
- [ ] 每篇正文都有数据来源链接。
- [ ] 已检查数据许可；提交的数据文件约小于 5 MB。
- [ ] 渲染页面同时显示代码和输出。
- [ ] 至少一个 figure 有 label 和 caption。
- [ ] `#|` chunk-option 写法已使用。
- [ ] 有目的地使用了 `message` 或 `warning`。
- [ ] Python 三个环境文件已提交：`pyproject.toml`、`uv.lock`、`.python-version`。
- [ ] R 环境文件已提交：`renv.lock`、`.Rprofile`、`renv/activate.R`。
- [ ] 两个 lockfile 都包含实际使用的依赖。
- [ ] `README.md` 已从 clean clone 实测。
- [ ] live site 的导航、图片、内部链接全部正常。
- [ ] Blog listing 包含所有 post。
- [ ] 没有模板 placeholder text。
- [ ] GitHub 上有 `docs/.nojekyll`。
- [ ] GitHub 上没有 `.quarto`、`_site`、`.DS_Store`、`.venv`、`renv/library`。
- [ ] 仓库为 Public。
- [ ] live site 在 private/incognito window 中检查通过。
- [ ] 至少 5 个 commits。
- [ ] 仓库中没有 token、key、密码或私人信息。
- [ ] 含两个 URL 的 PDF 已上传 Gradescope。

完成以上基本项目后，才考虑 Bonus。
