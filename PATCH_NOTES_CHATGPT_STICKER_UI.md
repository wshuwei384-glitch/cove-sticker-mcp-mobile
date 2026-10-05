# ChatGPT 表情包内联显示补丁

本补丁只处理 ChatGPT 内联展示表情包，不改图库、识图、频率策略或管理后台逻辑。

## 修改内容

- `express` 继续返回标准 MCP `ImageContent`。
- 为 `express` 增加 `_meta.ui.resourceUri` 与 `openai/outputTemplate`。
- 新增 `ui://sticker-mcp/sticker-preview-v1.html` MCP App 资源。
- `express` 选中表情包时，把预览图副本放入 Tool Result `_meta.sticker_preview`，避免把大段 base64 放进模型可见文本。
- ChatGPT 内联组件从 `window.openai.toolResponseMetadata` 读取隐藏预览数据并显示图片。
- SDK 包版本从 `0.1.0.dev1` 调整为 `0.1.0.dev2`。

## 验证

已通过 Python `compileall` 语法检查。当前运行环境无法联网安装项目依赖，因此未在本地执行完整 pytest；部署后应以 ChatGPT 手机端实际调用 `express` 为最终验证。
