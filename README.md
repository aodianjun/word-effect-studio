# Word Effect Studio(含 Motion 编排)

HyperGlow 单词效果包编辑器 + 歌词动态排版编排器(参考 [JIZURA](https://github.com/852wa/JIZURA)
创作流,MIT)。本仓库自带 GitHub Pages,推送 `main` 后 Actions 自动把
`tools/word-effect-editor/` 发布到站点根。

- 在线地址:`https://aodianjun.github.io/word-effect-studio/`
- 主编辑器:站点根的 `index.html`
- Motion 编排:主编辑器顶栏「Motion 编排」(即 `motion.html`)

## 仓库结构

```
index.html                              根跳转页 → tools/word-effect-editor/
docs/WORD_EFFECT_PACKS.md               效果包规格(含 §11 盒模型输出模式)
samples/                                两个官方样例效果包
.github/workflows/pages-word-effect-editor.yml   Pages 发布工作流
tools/word-effect-editor/               编辑器全部源码
  index.html / app.js / engine.js / templates.js   主编辑器
  motion.html / motion.js                          Motion 编排器(新)
  test_engine.js / test_motion.js                  回归测试(node 直接跑)
  make_site.py / README.md / DEPLOY_GITHUB_PAGES.md
```

## 更新站点(纯网页操作)

1. 打开 `tools/word-effect-editor/` 目录页 → **Add file → Upload files** →
   拖入要更新的文件 → Commit changes;
2. **第一次启用 Motion 必须改一次工作流**:打开
   `.github/workflows/pages-word-effect-editor.yml` → 铅笔编辑 → 把 Stage static site
   一段的 `cp` 列表加上两行(`motion.html` / `motion.js`,见下方完整段) → Commit;
3. 推送后 Actions 自动重新部署,1–2 分钟后刷新站点(Ctrl+F5)。

`.github/workflows/pages-word-effect-editor.yml` 的发布段:

```yaml
      - name: Stage static site
        run: |
          set -euo pipefail
          mkdir -p _site
          cp tools/word-effect-editor/index.html              tools/word-effect-editor/engine.js              tools/word-effect-editor/templates.js              tools/word-effect-editor/app.js              tools/word-effect-editor/motion.html              tools/word-effect-editor/motion.js              _site/
          ls -l _site
```

> 以后站点文件有增删,改这一段 `cp` 列表即可。

## 本地回归测试

```bash
node test_engine.js     # 编辑器 68 项
node test_motion.js     # Motion 14 项
```

## Motion 编排是什么

把整首歌的动态排版一次性编排成**一个 HyperGlow 盒模式效果**(`outputMode: "boxes"`):
JIZURA 式轻量歌词语法(`/` 镜头、`*强调*`、行末 `!` 闪光、`歌词|注音`、`[间奏 8]`)→
BPM 铺底 / 点击同步(空格打点)/ LRC 时间戳 → 主题 + seed 驱动的四手法编排(波浪 /
弹跳 / 滑入 / 强调脉冲)→ 导出效果包 JSON 导入 HyperGlow。预览与实机共用同一 VM,
所见即所得;生成器保证落在 512 指令 / 12 KiB / 4096 绘制每帧的预算内。

详见 `tools/word-effect-editor/README.md` 与主仓 `docs/WORD_EFFECT_PACKS.md` §11。
