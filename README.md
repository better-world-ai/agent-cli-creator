# agent-cli-creator

[English](./README_EN.md) | 中文

你想在网页上反复做的事，一句话告诉 AI agent，它就能帮你做成 CLI 工具。生成的 CLI 让 agent 随时调用，直接驱动你真实的 Chrome 登录态，不走 API，不折腾 token。

本仓库就是让 agent 学会"做 CLI"的那个 skill 本身。装好它，对你的 agent 说一句「帮我给 example.com 做个 CLI」即可。已经用这套方法做出来的工作示例见 [better-world-ai/x-cli](https://github.com/better-world-ai/x-cli)。

DEMO（一个 CLI 的诞生过程）：

https://github.com/user-attachments/assets/c1d04187-972a-4b8a-b243-df085281fc77

## 前置依赖

要让 agent 真正控制你的浏览器，需要装 [kimi-webbridge](https://www.kimi.com/zh-cn/features/webbridge)。它分两部分：

1. **浏览器插件**，agent 控制浏览器的入口工具。装好之后，所有点击、输入、读取都通过它转发，你登录过的 Chrome 会话自动被复用。
   - 中文：<https://www.kimi.com/zh-cn/features/webbridge>
   - English：<https://www.kimi.com/features/webbridge>

2. **本地 skill**，让 agent 知道怎么用上面那个插件。装好：

   ```bash
   curl -fsSL https://kimi-web-img.moonshot.cn/webbridge/install.sh | bash
   ```

## 安装 skill

```bash
npx skills add better-world-ai/agent-cli-creator
```

<details>
<summary>没有 Node.js？手动安装</summary>

把本仓库的内容（`SKILL.md` + `references/`）复制到你 agent 的 skills 目录下的 `agent-cli-creator/` 子目录里（Claude Code 是 `~/.claude/skills/agent-cli-creator/`）。不确定路径？把这一段 README 丢给你的 agent，它会自己判断。

</details>

装完就能用，对话里说一句「帮我给 example.com 做个 CLI」即可触发。

## 怎么用

1. 启动 kimi-webbridge，并在 Chrome 里登录目标网站。
2. 对 agent 说，比如：
   > "帮我做一个 example.com 的 CLI，我要能拉首页信息流，并且能发评论。"
3. agent 会先问你几个问题（用什么语言、前 1–3 个功能是什么），然后自己去分析站点、搭脚手架、实现命令，关键节点会停下来确认。
4. 最终你会拿到一个这样用的工具：
   ```bash
   example-cli login-status
   example-cli home --limit 10
   example-cli post --content "hello"
   ```

## 工作示例

[better-world-ai/x-cli](https://github.com/better-world-ai/x-cli) 收录了一批用这套方法做出来的 CLI——AI 画图、中国租房（58 同城、安居客）、英美欧租房、酒店机票预订、高考志愿查询等场景。

## License

MIT，见 [LICENSE](./LICENSE)。
