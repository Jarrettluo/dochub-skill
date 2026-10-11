# DocHub 文档发布技能

> 将 Markdown 文档发布到 DocHub 文档中心

## 触发指令

- "写一篇 xxx 文档发给我"
- "发布到 dochub"
- "帮我写一篇 xxx 并发布到 DocHub"
- "上传到 dochub 文档"

## 工作流程

1. 解析用户需求，写成 Markdown 文档
2. 转换为 PDF（使用 weasyprint）
3. 复制到 `/var/www/dochub/docs/` 或通过 nginx alias 路径
4. 更新 DocHub 前端的文件列表（`app.js`）
5. 返回文档链接

## 输出

- Markdown 源文件：`~/.openclaw/workspace/docs/<标题>.md`
- PDF 文件：`.workspace/docs/<标题>.pdf`
- 在线访问：
  - MD: `http://your-docs-host.example.com/docs/<标题>.md`
  - PDF: `http://your-docs-host.example.com/docs/<标题>.pdf`
- DocHub: `http://your-docs-host.example.com/dochub/`

## 依赖

- Python: markdown, weasyprint
- nginx: `/docs` alias 到 `~/.openclaw/workspace/docs`
- DocHub 前端: `/var/www/dochub/js/app.js`

## 更新文件列表

当新增文档后，需要更新 `app.js` 中的文件列表：

```javascript
const files = [
    'dochub-intro.md',
    'openclaw使用技巧.md',  // 新增文件加这里
    // ...
];
```

## 使用示例

```
用户: 写一篇 openclaw 使用技巧发给我
→ Coda: 好的，我来写一篇...
→ 生成 MD + PDF
→ 更新 app.js
→ 返回链接
```