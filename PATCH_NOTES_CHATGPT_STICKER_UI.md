# ChatGPT 表情包内联显示补丁 v2

本补丁继续只处理 ChatGPT 自动调用与内联展示，不改图库、识图、频率策略或管理后台逻辑。

## 修改内容

- 将 `express` 的说明改为更明确的主动调用策略：日常聊天出现吐槽、摆烂、撒娇、庆祝、调侃等明显情绪时，可主动调用，无需等用户明确说“发表情包”。
- UI 资源 URI 升级为 `ui://sticker-mcp/sticker-preview-v2.html`，避免 ChatGPT 继续使用旧组件缓存。
- 组件优先监听 MCP Apps 标准 `ui/notifications/tool-result`，直接读取 Tool Result `_meta.sticker_preview`。
- 保留 `window.openai.toolOutput`、`window.openai.toolResponseMetadata` 与 `openai:set_globals` 兼容回退。
- `express` 仍同时返回标准 MCP `ImageContent`，不改变原有无 UI 客户端的行为。
- 版本号升级为 `0.1.0.dev3`。

## 依据

OpenAI 当前文档建议新 UI 使用 `_meta.ui.resourceUri` 绑定资源，并通过 MCP Apps 的 `ui/notifications/tool-result` 接收工具结果；组件内容更新时应更换资源 URI 作为缓存键。

## 验证

已执行 Python `compileall`。当前环境无法联网安装 `mcp==2.0.0`，因此完整 pytest 仍需在 Render / Codespaces 依赖齐全环境运行。
