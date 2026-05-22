# agent-cli-creator

让 AI agent 帮你把"网页上反复做的事"变成一个 CLI 工具。

装上这个 skill，对你的 agent 说一句「帮我给 example.com 做个 CLI，要能拉首页、能发评论」，它会自己去分析站点、跟你确认几个细节、搭脚手架、实现命令、跑通验证。最终你拿到一个直接能用的工具：

```bash
example-cli login-status
example-cli home --limit 10
example-cli post --content "hello"
```

生成的 CLI 直接复用你 Chrome 里的真实登录态——不走 API、不折腾 token、不需要去开发者后台申请 key。

## 前置依赖

要让 agent 真正控制你的浏览器，需要装 [kimi-webbridge](https://www.kimi.com/zh-cn/features/webbridge)。它分两部分：

1. **浏览器插件**——agent 控制 Chrome 的入口。装好之后所有点击、输入、读取都通过它转发，登录态自动复用。
   - 中文：<https://www.kimi.com/zh-cn/features/webbridge>
   - English：<https://www.kimi.com/features/webbridge>

2. **本地 skill**——让 agent 知道怎么用上面那个插件。装好：

   ```bash
   curl -fsSL https://kimi-web-img.moonshot.cn/webbridge/install.sh | bash
   ```

## 安装 skill

```bash
npx skills add better-world-ai/agent-cli-creator
```

<details>
<summary>没有 Node.js？手动安装</summary>

把这个仓库的内容复制到你 agent 的 skills 目录的 `agent-cli-creator/` 子目录里（Claude Code 是 `~/.claude/skills/agent-cli-creator/`）。不确定路径？把这一段 README 丢给你的 agent，它会自己判断。

</details>

装完就能用，对话里说一句「帮我给 example.com 做个 CLI」即可触发。

## 怎么用

1. 启动 kimi-webbridge，并在 Chrome 里登录你要做 CLI 的目标网站。
2. 对你的 agent 说，比如：
   > 「帮我做一个 example.com 的 CLI，我要能拉首页信息流，能发评论。」
3. agent 会先问你几个问题（用什么语言、前 1–3 个功能选什么），然后自己去分析站点、搭脚手架、实现命令，关键节点会停下来跟你确认。
4. 最终你会拿到一个像这样直接能用的工具：
   ```bash
   example-cli login-status
   example-cli home --limit 10
   example-cli post --content "hello"
   ```

跑出来的 CLI 同时还会附带一个配套 skill，让以后其他 agent 知道怎么"使用"这个 CLI——而不仅是当初它是怎么造出来的。

## 工作示例

[better-world-ai/x-cli](https://github.com/better-world-ai/x-cli) 收录了一批用这套方法做出来的 CLI——AI 画图、中国租房（58 同城、安居客）、英美欧租房、酒店机票预订、高考志愿查询等。每一个都是真的"对 agent 说一句话"做出来的，不是手写的脚手架。

## License

MIT，见 [LICENSE](./LICENSE)。
