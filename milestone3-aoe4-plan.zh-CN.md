# DSCI 521 Milestone 3：AoE4 分析计划

## 一、项目主题

使用《帝国时代 IV》赛事数据，分析 **Red Bull Wololo: Legacy 2022** 中不同国家选手的参赛情况、名次和奖金。

数据来源：

[Esports Earnings：Red Bull Wololo: Legacy 2022 – Age of Empires IV](https://www.esportsearnings.com/tournaments/56552-red-bull-wololo-legacy-2022-age-of-empires-iv)

本项目只分析这一场赛事，不扩展到多个赛事，也不做预测模型或因果推断。

## 二、只回答三个问题

1. 参赛选手来自哪些国家？每个国家有多少名选手？
2. 不同国家的选手取得了什么名次？
3. 不同国家获得了多少奖金？

这三个问题已经足够满足 computational post 的分析需要。不再额外增加选手实力评分、跨赛事比较、显著性检验或机器学习任务。

## 三、数据表

使用两张表：

### `player_profiles`

记录选手信息：

- `player_id`
- `player_name`
- `country`

### `tournament_results`

记录赛事结果：

- `player_id`
- `placement`
- `prize_usd`

两张表通过 `player_id` 连接。需要统一处理选手姓名的大小写和别名，例如 `Lucifron` / `LucifroN`。

## 四、两篇 computational posts

### R post

使用 R 完成：

1. 读取并连接两张表；
2. 统计各国选手数量和名次；
3. 统计各国奖金并生成图表或表格。

### Python post

使用 Python 对同一份数据完成同样的三个问题：

1. 读取并连接两张表；
2. 统计各国选手数量和名次；
3. 统计各国奖金并生成图表或表格。

两篇 post 可以使用相同的分析问题。只要 R 和 Python 都真正执行了分析即可。

## 五、完成标准

- [ ] 有一篇 R post。
- [ ] 有一篇 Python post。
- [ ] 每篇 post 至少有 3 个真正执行分析的 code chunks。
- [ ] 每篇 post 至少有一个代码生成的图表或表格。
- [ ] 每篇 post 都说明数据来源并提供链接。
- [ ] 页面上同时显示代码和输出。
- [ ] Python 依赖写入 `pyproject.toml` 和 `uv.lock`。
- [ ] R 依赖写入 `renv.lock`。
- [ ] `README.md` 写明从 clone 到渲染网站的步骤。
- [ ] 网站能够从干净环境重新渲染。
- [ ] live site 的导航、Blog listing、图片和两个 post 都正常。
- [ ] 完成 Milestone 3 要求的 GitHub Pages、提交历史和 Gradescope PDF。

## 六、明确不做的事情

- 不增加第四个或更多研究问题。
- 不分析多个 AoE4 赛事。
- 不建立复杂的综合实力指标。
- 不做机器学习预测。
- 不做因果结论。
- 不为了“看起来更复杂”而增加额外数据源。

后续工作只围绕上述范围进行：准备数据、编写 R/Python post，以及完成 Milestone 3 的可复现工程配置。
