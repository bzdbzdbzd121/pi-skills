# pi-skills

我的 agent skills 集合，面向中文技术写作、回复组织、观点讨论和独立复核。每个 skill 是 `skills/<name>/SKILL.md`，可选附带 examples 等引用材料，遵循 pi / Claude Code 的 skill 目录约定（YAML frontmatter 里的 `name` 与 `description`）。

## 收录

| Skill | 作用 | 触发场景 | 附带内容 |
|---|---|---|---|
| [`discussion`](skills/discussion/SKILL.md) | 平等讨论：把你的观点当待检验主张，独立查证后再给判断 | 你提出待推敲的想法、方案，或想评估自己的判断 | — |
| [`second-opinion`](skills/second-opinion/SKILL.md) | 独立复核：开一个独立子会话，带着原始需求与证据重新查证当前结论 | 结论要落地但想先验一遍；手动调用（`disable-model-invocation`） | — |
| [`clear-reply`](skills/clear-reply/SKILL.md) | 清楚回复：先答主问题，把行动说具体，措辞不超出证据 | 解释问题、说明步骤、比较方案、汇报结果，或你说“说清楚”“没看懂” | — |
| [`clear-prose-zh`](skills/clear-prose-zh/SKILL.md) | 清晰连贯的中文写作：保原意与置信度的前提下改写中文技术说明 | 润色 README、设计说明、PR 描述、状态汇报；文本“读起来不通顺”“短句太碎” | [`examples/before-after.md`](skills/clear-prose-zh/examples/before-after.md) |

三者的分工：`clear-reply` 管一次回复的写法，`clear-prose-zh` 管成篇中文文本的连贯，两者只改表达、不改事实。`discussion` 决定要不要接受一个观点，`second-opinion` 决定要不要相信一个已得出的结论——后者会另开独立上下文取证，不认同原作者的解释。`second-opinion` 默认只复核、不修复，且设了 `disable-model-invocation`，需要显式调用。

## 安装

```bash
git clone git@github.com:bzdbzdbzd121/pi-skills.git ~/workspace/pi-skills
```

软链接（推荐，之后 `git pull` 即生效）：

```bash
mkdir -p ~/.pi/agent/skills
for s in ~/workspace/pi-skills/skills/*/; do
  ln -sfn "${s%/}" ~/.pi/agent/skills/"$(basename "${s%/}")"
done
```

或直接拷贝：

```bash
cp -r ~/workspace/pi-skills/skills/* ~/.pi/agent/skills/
```

Claude Code 读取 `~/.claude/skills/`，改上面的目标目录即可。软链接请用绝对路径，相对链接在 skill 解析时容易断。

## 约定

- 只放我自己维护的 skill。外部来源（含上游仓库的 clone、他人的 skills 包）不收录，避免双源分叉。
- 中文优先。这些 skill 处理的是中文表达与其准确性，不是通用提示词模板。
- 改完一个 skill 请顺手更新上表的一句话说明，否则索引会失准。

## License

MIT，见 [LICENSE](LICENSE)。
