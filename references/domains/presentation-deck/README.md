# 领域:投屏分享 deck

**适用:** 单文件 Vue 3 / 单 HTML 的可投屏分享 web deck——既不是 PPT 那种一屏一标题加几个 bullet,也不是滚动长文。每屏即一个完整论点,信息饱满,远距离可读,演讲者键盘驱动。

## 锚点配方

| 维度 | 人名 | facet |
|---|---|---|
| 自适应布局架构(前置约束) | Heydon Pickering & Andy Bell《Every Layout》 | 用 axiomatic CSS primitives(Cover / Stack / Frame / Box)替代手动 padding/margin;布局问题在架构层一次解决,不在 case 层反复修;先定义布局 primitives,再用其他锚点填充内容 |
| 信息密度 | Edward Tufte《Envisioning Information》 | data-ink ratio 最大化;关键数字字号 ≥ 屏内最大;饱满不等于拥挤,靠分组而非空白;拒绝装饰性留白;组件类型多样(整 deck 至少 5-6 种,单一类型不超过 2 屏) |
| 视觉层次 / 远距离可读 | Adam Wathan & Steve Schoger《Refactoring UI》 | 投屏正文 ≥ 20px;WCAG AAA 对比度(正文 7:1);灰阶严格 4 档;每屏一个 accent 色仅用于 hero 和 takeaway;spacing scale 严格 8 的倍数 |
| 微互动 / 渐进披露 | Josh Comeau | 演讲者驱动而非用户驱动(键盘控制,不依赖 hover,禁用 autorun / 滚动劫持 / 视差);分步披露要可控;过渡曲线 `cubic-bezier(.2,.8,.2,1)` 280ms;`prefers-reduced-motion` 强制降级 |
| 演示叙事 / 单屏自洽 | Nancy Duarte《Slide:ology》 | 每屏一个 big idea + 一个 hero number;对比并置制造张力;屏内自洽即"只看这一屏也成立";5 act 叙事弧(起源 / 实证 / 洞察 / 落地 / takeaway) |

## 必要规则

- 单 HTML 文件 + Vue 3 CDN,无构建工具,无第三方图表 / UI 库(SVG 内联 + Vue 模板即可)
- 1920×1080 固定画布 + transform scale 自适应:`.stage { position: fixed; inset: 0 }`,`.deck { position: absolute; top: 50%; left: 50%; transform: translate(-50%,-50%) scale(...) }`
- HUD(keymap / overview)必须放在 `.stage` **外**,否则 `position: fixed` 会降级为相对 transformed 父元素的 absolute
- 字号用固定 px,不用 vw/vh(避免与 transform scale 双重缩放)
- `screen-head` / `big-idea` / `takeaway` 必须加 `flex-shrink: 0`,让中间 body 承担压缩成本
- 每屏内容总高度 ≤ 画布 85%(~920px)
- 键盘 ←→ 切屏;点击下一屏;右键上一页;Esc 进入 overview;F 全屏
