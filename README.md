# Word Effect Studio

HyperGlow 单词效果包编辑器：DSL 轨道、沙箱字节码、实时预览、LRC 时间轴、辉光预设、程序调试。

- 编辑器：[tools/word-effect-editor/](tools/word-effect-editor/)（直接打开其中的 `index.html`）
- 规格：[docs/WORD_EFFECT_PACKS.md](docs/WORD_EFFECT_PACKS.md)
- 样例：[samples/word-effect-pack.json](samples/word-effect-pack.json)、
  [samples/word-effect-program-pack.json](samples/word-effect-program-pack.json)
- 程序组装工具：[tools/assemble_effect_program.py](tools/assemble_effect_program.py)

## Gitee Pages

仓库 → **服务 → Gitee Pages** → 部署分支 `master` / 目录 `/` → 启动。

根目录的 `index.html` 会跳转到 `tools/word-effect-editor/`。Gitee Pages 可能要求仓库公开并完成
实名；如果入口不可用，先在仓库设置里把仓库改为公开再试。

## GitHub Pages

见 [tools/word-effect-editor/DEPLOY_GITHUB_PAGES.md](tools/word-effect-editor/DEPLOY_GITHUB_PAGES.md)。
仓库里的 `.github/workflows/pages-word-effect-editor.yml` 会把 `tools/word-effect-editor`
发布到站点根。
