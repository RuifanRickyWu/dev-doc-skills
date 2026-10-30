# dev-doc-skills

和 Claude 一起做开发时，把大任务一层层拆成文档。先聊，聊定了才写；你说拆哪块，它才拆哪块。

## 安装

在终端里运行：

```bash
claude plugin marketplace add RuifanRickyWu/dev-doc-skills
claude plugin install dev-doc@dev-doc-skills
```

装好后重启 Claude Code。

不想用插件的话，把 [`skills/dev-doc`](skills/dev-doc) 这个文件夹复制到 `~/.claude/skills/` 下面也行。

## 解决什么问题

跟 agent 一起做大项目，最累的是反复对齐：

- 聊好的东西，换个对话就没了，又得从头讲一遍。
- agent 爱自己拿主意，替你把框架拆了。
- 文档越写越长，结论和讨论混在一起，最后谁也不想看。

dev-doc 让 agent 按你的节奏来：

- 讨论留在对话里，定下来的结论才写进文档。
- 你说拆哪块，它就给哪块建一个新文件夹。
- 每份文档都写清楚上级和依赖。改了一份，它会告诉你还有哪些要跟着改。

## 用起来是这样

> **你**：（聊了几轮大框架）大纲定了，写进去。
>
> **Claude**：写好了：`dev-doc/file-pipeline/file-pipeline.md`。
>
> **你**：先聊上传，拆出来。
>
> **Claude**：建好了 `upload/upload.md`，大纲最后的“子模块”里也加上了上传。
>
> ……后来又拆了分片上传和解析……
>
> **你**：上传完成的消息里只放文件 ID 就行。定了。
>
> **Claude**：`upload.md` 改好了。解析用到了这条消息，`parse.md` 第 1 条也得改成“先用文件 ID 查出文件信息”。要改吗？

最后聊出来的文件：

```text
dev-doc/
└── file-pipeline/
    ├── file-pipeline.md      ← 大纲
    ├── upload/
    │   ├── upload.md
    │   └── chunking/
    │       └── chunking.md
    └── parse/
        └── parse.md
```

完整的例子在 [examples/](examples/) 里：[整段对话](examples/file-pipeline-chat.md)，和它聊出来的[全部文档](examples/dev-doc/file-pipeline/file-pipeline.md)。

## 七条规则

全文在 [SKILL.md](skills/dev-doc/SKILL.md)。

1. 没说定，就不写。
2. 只写结论。
3. 拆一次，建一个新文件夹。
4. 每份文档开头写上级和依赖。
5. 一件事只写一次。
6. 聊一个模块前，先读它的上级和依赖。
7. 改完一份，检查相关的文档。

## 改成你自己的

Fork 这个 repo，改 `skills/dev-doc/SKILL.md`，再按上面的方法安装，把 `RuifanRickyWu` 换成你的 GitHub 用户名。

## 灵感

来自 Karpathy 的 [LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)：让 LLM 维护一套一直在更新的 markdown 文档，而不是每次从头再来。dev-doc 把这个想法用在开发上，但反过来：结构和决定都是你的，agent 只负责记下来、维护好。

## License

[MIT](LICENSE)
