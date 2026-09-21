# 项目进度与决策记录

功能清单看 [README.md](./README.md)，这里只记**过程**：为什么做成这样、哪些结论被推翻过、验证要靠什么手段、还剩什么没做。

最后更新：2026-09-21（深夜）。出图重做成图册（多周连排 / 按人成册 / 图纸目录 / 配平）+ 占位页，本轮前五份提交已 push 并按「比内容不比状态码」复核过；**版面留档补上了**（六张出图 + 一份版面读数 JSON），代价是装了一套无头 Chromium，收获是看图当场揪出两条观感缺陷（图签栏浮在纸中间、纸上印着编辑提示）——**这两处修复和留档图目前还在工作区，未提交**。

## 当前状态

| | |
| --- | --- |
| 线上版本 | `b466a50`（= `origin/main`，图册版出图 + 占位页 + 三份文档）。push 后轮询 Pages：前两次（约 45s 内）仍是上一版 `9fb34ddf…` / 167111 字节，第 3 次起 `e891f144f7aaf7f531433969d957ec34` / 170484 字节，与当时本地 `index.html` **逐字节一致**；这个比对口径每轮上线后都该做一次，命令见「怎么验证」。**注意**：本轮留档揪出的两条 CSS 修复让本地变成了 `cbf55842…` / 171477 字节，**线上还差这一步**（未提交） |
| 数据 schema | v3（带 `tombstones`），可读 v1/v2 并自动升级 |
| 云端数据 | 69 条任务，覆盖 2026-W21 … W29 |
| 同步 | 已打通。一次真实 PATCH 验证过非破坏性（69→69，0 条增删，只有 `order` 字段补齐、`currentWeek` W29→W39） |
| 出图 | 从「单张 A3 + 底部图签」升级为**图册**：按周连排或按人成册，1–8 周，可加图纸目录页，逐张配平缩放，零张纸时出「此页无图」占位页 |
| 待办 | 版面留档**已补**（六张出图 + `docs/sheet-facts.json`），还缺拖拽中 / 手机长版面 / 出图对话框三张；两条 CSS 修复与留档图**尚未提交**；另外三位同事还没各自配 Token（详见文末「还欠着的」） |

## 时间线

| 提交 | 日期 | 做了什么 |
| --- | --- | --- |
| `fff4ac4`…`27c9af0` | 2026-05-18 | 最初的单页周看板 |
| `57123a2` `ee212c6` | 2026-05-18 | 接上 GitHub Gist 同步，做成「零配置」——Gist ID 和 Token 直接写进源码 |
| `e13a04f` | 2026-05-18 | 悬浮保存条 + 实时状态 |
| `5bfd45d` | 2026-05-20 | 进度改成点击拖动尺寸线，不再是数字输入框 |
| `da3dca8` | 2026-05-25 | 搜索过滤、统计面板、日期编辑修复、删除撤销 |
| `91710b2` | 2026-06-03 | 手机端进度条拖动灵敏度 |
| （停摆） | 2026-07-20 → 09-21 | 源码里的 `ghp_…` 被 GitHub secret scanning 吊销，**同步静默失败约两个月**——云端 `updated_at` 停在 2026-07-20T05:26:51Z 就是证据。这四个人的本地各成一张孤本 |
| `3eaf2cc` | 2026-09-20 | 图纸化视觉重构（网格、图签、云线、剖面线、晒图术语）；打开页面默认回到本周 |
| `58f3392` | 2026-09-21 | 晒图模式：A3 横排图纸 + 图签栏 + 裁切标记 + SHT 页号 |
| `38361a5` | 2026-09-21 | 卡片拖拽排序（跨列即改派）+ 20 级撤销 |
| `9340ddc` | 2026-09-21 | 修订表、周对比云线、个人负荷条；字体离线身份与本地备份导入导出 |
| `c22070c` | 2026-09-21 | **同步改为先拉后推**，杜绝用本地孤本覆盖云端 |
| `83ec75e` | 2026-09-21 | 删除墓碑（schema v3）：删掉的任务不会被云端还回来 |
| `793b54d` | 2026-09-21 | 关页面前用 `pagehide` + `keepalive` 补发未上传的改动 |
| `744ccd2` | 2026-09-21 | 小控件点击热区放大；两处复核结论落成注释 |
| `18d9a47` | 2026-09-21 深夜 | **出图重做成图册**：`SheetSet` 模块 + 晒图设置对话框（截止周 / 连排周数 / 分册方式 / 收录范围 / 目录开关）+ 图纸目录页 + 预览层 + 逐张配平缩放与续页告警；图签栏从「屏上隐藏的单块 `#title-block`」变成每张纸都有；`?sheet&from=&count=&mode=&scope=&toc=` 直连 |
| `542a52c` `79b902d` | 2026-09-21 深夜 | 两份文档跟上；`.gitignore` 收掉 `.DS_Store` |
| `e5eca4e` | 2026-09-21 深夜 | **占位页**：零张纸时出「此页无图 · NIL」，并说清零张的原因（区间没数据 / 收录范围滤空）。线上只读冒烟撞出来的分支，离线 harness 造不出来 |
| `9c982bc` | 2026-09-21 深夜 | 这两份文档补上图册与占位页的决策、数字、自证方法；连同上一个提交一起 push，并按「比内容不比状态码」复核上线 |
| `b466a50` | 2026-09-21 21:31 | 只动文档：记下占位页在真站点的只读复核，以及 Pages 缓存翻转的实测秒数（前两次约 45s 仍是旧版） |
| （未提交） | 2026-09-21 深夜 | **版面留档 + 两条观感修复**：`.preview/shoot.py`（无头 Chromium 出图留档，仓库外）拍六张进 `docs/screenshots/`，版面读数落 `docs/sheet-facts.json`；看图当场揪出「图签栏浮在纸中间」和「纸上印着编辑提示」，`index.html` 只加 12 行 CSS（`flex:1 1 auto` 贴下边线、`.placeholder` 隐藏 + `:has()` 补 `（未命名）`），**配平数字一位没变** |

## 关键决策与被推翻的假设

### 1. 上传一律先拉后推（最重要的一条）

**发现过程**：动手接同步之前，先去看了线上那块板子的真实数据——`localStorage.renderDeptWeeklyTracker` 当时是 `null`，本地是一张**空板子**。而旧实现按「存配置 → 立刻推本地」的顺序走，点一下「保存并同步」就会用这张空板子覆盖云端 69 条任务。是读数据读出来的事故，不是跑出来的。

**现在的规矩**：任何上传路径都必须是 `pull → merge → push`，并且加了一个会话级闸门 `GistSync.reachable`：本次会话没有真的读到过云端（200）就不许推。读不到 ≠ Token 失效，所以那里的提示写的是「检查 Gist ID 是否填对」而不是「去换 Token」——**这里拦的是覆盖，不是权限**。

`pagehide` 的补发也受同一条约束：`reachable === false` 时宁可不发。

### 2. 删除必须要墓碑

v2 的 merge 是「id 取并集 + `updatedAt` 新的赢」，这个语义下**删除是不可表达的**：A 删了任务 T 并推上云，B 的本地还留着 T（且 `updatedAt` 可能更新），一合并 T 还魂。所以 v3 加 `tombstones: {id: deletedAtISO}`。

配套细节，改动时容易漏：

- 撤销/恢复删除时要把 `updatedAt` 顶到删除时刻**之后**，光清本地墓碑不够——那份墓碑可能已经传上云了。
- 撤销一次「新增」要顺手给它立墓碑，否则下次合并它又回来。
- 「复制上周未完成」整片撤销时，被移走的副本也要立墓碑。
- 任务已经不在了，墓碑要继续留着往外传，不能顺手清理。

### 3. Token 不进仓库

见 README 的硬规矩。补充一点：fine-grained PAT 的 Gist 权限在 **Account permissions** 那一栏，不在 Repository 里——只勾了仓库权限的 token 读得到仓库但写不了 Gist。这次用的 token 校验过 `/user` 身份，也只在那一次真实 PATCH 里用过。

### 4. 字号不为手指让步

复核量出工具栏按钮 26px 高、删除叉 16×16、`REV` 徽标 28×15，确实不好点。但字号是这张图纸密度的一部分，放大字就毁了版面，所以改成用一层透明 `::after` 把**可点范围**向外借已有的空白（卡片内边距、行距、工具栏 gap），墨迹一像素不动。

结论：以后遇到「不好点」，先想热区，别先想放大。

### 5. 一张 A3 装不下就明说，别硬塞（配平与 66% 下限）

**这条是老代码的账**：原来的晒图是「2×2 四张图幅 + 底部图签」，屏幕排到多高就打多高。量一个正常有 11 张卡的周：两列两行排下来自然高约 1507px，而 A3 横排可印区只有 1047px——**超 44%**。浏览器会默默把它挤到第二页，纸面上没有任何地方说「这一张没装下」。

现在：纸面固定按 **1512×1047 CSS px**（A3 可印区 @96dpi）排版，量 `scrollHeight` 等比缩到装得下，这一步叫**配平**；但**缩到 66% 就停**——再压就不是图纸，是小字报。到下限仍装不下的那张打铁锈色虚线框，摘要写「N 张压到下限仍超纸面 · 出纸会续页」，让**续页成为看得见的取舍**而不是意外。

连带改掉的一件事：版面从「屏幕密度」换成「纸面密度」——四条人列从 2×2 改成**一排四列通栏**（`.sheet-board` 四等分 grid），因为四列横排后自然高约 1000px，正好落进 A3；2×2 是屏幕的形状，不是纸的形状。看板本体保持四列不动。

### 6. 缩放只走 `transform`，占位高度要自己写回去

`transform: scale()` 不改盒子占位，纸叠纸会重叠。所以 JS 把量到的自然高写进 `--nat`，`.sheet-paper` 的高 = `nat × fit`。同理 `@media print` 里必须 `--fit: var(--fc, 1)`——屏上那条按窗口宽缩的 `--fv` **不能带进打印机**，屏上缩小 ≠ 出纸缩小。

反面教训：想纯 CSS 做屏上适配（`--fit: min(1, calc((100vw - 44px) / 1512))`）是**走不通的**——长度除长度才得数字，`min()` 里那个 `1` 和长度不是一类东西。最后只能是 JS 算 `--fv`，CSS 只负责乘。

### 7. 上限要压，但别把用户输入一起吞掉

连排周数有两个上限：8 周，和 16 张纸（按人成册时每人每周一张 → 实际只剩 3 周）。超了当然要压，但**摘要要说、下拉框要留着用户原本要的值**：`SheetSet.cfg.count` 存请求值，只有 `plan()` 拿到的副本被压。早先的实现把压后的值写回 `cfg`，于是「预览 → 改设置」重开对话框时 8 变成 3，看着像输入被吞了一次——**回显用户的意图，不是回显程序的妥协**。

### 8. 零张纸的时候，也要有一张纸可打

**这条是线上验出来的，不是离线跑出来的**：push 之后拿真站点做只读冒烟（只 GET 不 PATCH），顺手开了出图对话框——**按人成册 + 连排两周 → 预览是一片空白，摘要写「0 张」**。原因很平凡：云端那 69 条任务只到 W29，而真实本周是 W39，本周往后（以及上周）根本没数据；harness 的 seed 是照着一周 11 张卡造的，所以离线永远撞不到这个分支。

改法不是「让它出张白纸」，是出一张**「此页无图 · No Work To Plot」占位页**：张次 `NIL`，页眉右侧写「占位」，中间一个虚线框说清楚**为什么零张**——区间没数据 / 「只出未完成」把它滤空了 / 看板筛选把它滤空了，三种原因文案不同（别对着一份被筛空的数据说「四个人都排空了」），并给出该拧哪个旋钮。摘要与占位页共用 `nilReason()`，两处说法不会分叉。

顺带一条判断规矩：**空态不是错误态**。零张、零结果、零任务这类状态如果渲染出一片空白，读图的人无法区分「没东西」和「坏了」——这个项目已经因为「✓ 已同步」掩盖静默失败吃过一次两个月的大亏。

### 9. 留档改走无头 Chromium：观感的毛病只有像素能发现

前面八条都是「量出来的」，这条是「看出来的」。占位页和配平结果要留档时，In-app Browser 的面板在后台 → `take_screenshot` 直接 `NATIVE_BROWSER_VIEWPORT_UNAVAILABLE`（`viewport=0x0, visible=false`），而依赖面板前台意味着**每次留档都要用户配合点一下窗口**。于是装了 Playwright + chromium-headless-shell（系统 Python 3.9.6，`pip3 install --user`），留档改由 `.preview/shoot.py` 跑：无头、不需要交互、`--directory .preview` 起服务后一条命令出六张图加 `docs/sheet-facts.json`。

值回票价的是它当场暴露了两条**任何数值断言都测不出来的观感缺陷**：

1. **图签栏浮在纸中间**，下面留一截空白纸。之前所有测量都正常——卡数、自然高、`fc`、`spill` 全对，因为「空白在纸尾」不是布局错误，是观感缺陷——量不出来，看得出来。改法：`.sheet-page` 走 flex 列，内容块 `flex:1 1 auto` 自己吃掉剩余高度，图签栏钉在下边线；图签栏自带的 `margin-top:6mm` 就是最小间距，装不下时也不会糊住最后一张卡。**配平数字一位没变**（1450→.7221、1935→.66），这条要记下来：改的是留白归属，不是容量。
2. **纸上印着「点击输入任务名称」**。空卡在屏幕上需要提示可编辑，晒出去就成了「谁忘了填」。改成 `.sheet-page .task-name .placeholder{display:none}` + `::after{content:'（未命名）'}`——图纸的写法只陈述这张卡没名字，不教人怎么操作。这里翻过一次车：`::after` 一开始挂在 `.task-name` 上，有名字的卡也被补了一刀，晒出来全是「示例项目 B（未命名）」；必须用 `:has(> .placeholder)` 只挑那张真的挂着占位文案的卡。**同一张卡上的「备注 / NOTES」是故意留着的**：它读作字段名空着，不读作一句给不了的动作指令——只砍带动词的那句，别顺手把所有占位符一起藏掉。

两条修完都用断言钉住（`.preview/verify_sheet.py`，四种排法各跑一遍）：图签栏与纸下边线之间恒等于 page 自己的 18px 下内边距（43 / 22 / 11 / 0 张卡四种密度下都一样，多出来的空白才算浮在纸中间），编辑提示可见数恒 0，`（未命名）` 的卡数与占位卡数恒等（打码种子上分别是 5/43 与 1/22）。

**判断规矩**：`fit()`、`scrollWidth` 这类量能证明版面**没坏**，不能证明它**好看**。这个项目卖的就是图纸观感，留档因此不是收尾的仪式，是第三双眼睛。反过来也成立：**别为了凑一张图去拍一个不存在的状态**——原计划里有一张「蓝图主题下的占位页」，读完 `#print-stack` 那段令牌覆写才知道根本拍不出来（晒图一律走白，见「测量陷阱」第 8 条），于是那张图被删掉，事实改用两个 measured 颜色值记在下面的留档段里。

## 怎么验证（离线 harness）

**测试一律跑离线 harness，不要对线上 Gist 做写测试。**

harness 在仓库**外面**（仓库根就是 `weekly-tracker/`，`.preview/` 是它的同级目录，因此不受版本控制，换机器要重建）。下面 `<根>` 指 `weekly-tracker` 的上一级——别把绝对路径写死，这台机器的 `~/Documents` 会被 iCloud 整段搬走：

```bash
cd <根>
python3 .preview/build.py                        # 把 index.html + seed.json 拼成 .preview/preview.html
python3 -m http.server 8899 --bind 127.0.0.1 --directory .preview
# 打开 http://127.0.0.1:8899/preview.html
```

（**别写成 `http.server 8899 … .preview`** —— 这台机器的 Python 3.9 里那个位置参数是 `port`，
多余的路径会直接 `error: unrecognized arguments`；而 8899 上若还挂着旧服务，
`curl` 照样回 200，看起来像命令是对的。目录参数只有 `--directory` 一种写法。）

要产出**能进仓库**的东西（截图、演示）就换成打码种子，别拿 `seed.json` 拍：

```bash
python3 .preview/anonymize_seed.py                                   # → .preview/seed-anon.json
python3 .preview/build.py .preview/seed-anon.json .preview/preview-anon.html
```

push 之后确认 Pages 真的换成了新 HTML —— **别看状态码，比内容**（Pages 的 CDN 会短暂回旧版，
`200` 只说明服务活着，不说明它是你刚推的那份）：

```bash
md5 -q index.html                                    # 本地
curl -s -A 'Mozilla/5.0' https://yiyuqiao2748.github.io/weekly-tracker/ -o /tmp/p.html
grep -q SheetSet /tmp/p.html && echo LIVE            # 没换就隔 20–30s 再试，本次约 25–50s 生效
md5 -q /tmp/p.html                                   # 两个 md5 要一致
```

三种模式：

| URL | 用途 |
| --- | --- |
| `preview.html` | 默认。`GistSync` 整体 stub 掉，`api.github.com` 的 fetch 被拦截并计数（`window.__net`，正常应始终为 0） |
| `preview.html?sync=1` | 挂一个**假 GitHub**。`window.__fake = {authGET, anonGET, patch}` 可控返回码，`window.__remote` 是可控的云端数据，`window.__calls` 记录调用序列，PATCH 的 body 解析进 `window.__pushed` |
| `preview.html?sheet&…` | 出图。两件事同时发生：harness 把 `@media print` 规则原样复制成 screen 媒体（`window.__sheetRules` 是条数），页面自己按 URL 铺一册纸。参数：`from=2026-W36`（截止周）、`count=1..8`、`mode=weeks\|persons`、`scope=all\|open\|filtered`、`toc=0` 关目录 |

出图那条最适合直接当回归用，不用点对话框：

```
http://127.0.0.1:8899/preview.html?sheet&from=2026-W38&count=3&mode=persons
```

在 DevTools 里可以直接调 `SheetSet.preview({from:'2026-W37',count:2,mode:'persons',toc:true})` 拿 `SheetSet.lastPlan` / `SheetSet.fit()` 断言；**注意 `SheetSet` 是顶层 `const`，不是 `window` 属性**，在别的 frame 里驱动它要用 `iframe.contentWindow.eval('SheetSet.fit()')`。

已经跑通并验证过的矩阵（改同步相关代码后应重跑）：

- 有效 token → 序列 `GET → PATCH`，推上去的 70 = 本地 69 + 云端独有 1，一条没丢；
- 只读 token → `GET auth → GET anon → PATCH`，提示「Token 无写入权限 · 需 Gists: Read and write」；
- 云端读不到 → 两次 GET、**0 次 PATCH**；
- v2 的 localStorage 自动升到 v3，69 条完好；已删任务不会被陈旧的云端副本还魂；恢复 / Toast 撤销 / 撤销复制三条路都对；
- 上传 payload 里带 `tombstones` 且不含被删 id；待存状态下关页面恰好补发 1 次 keepalive PATCH，空闲 0 次，够不着云端 0 次；
- 离线回归：11 张卡 / 4 条负荷条 / 3 枚 REV / 编辑 + 撤销 / `__net === 0` / 控制台无输出。

出图这一轮跑过并记下来的数字（`git diff` 确认没有一行碰到 `GistSync`，所以上面那半张矩阵不需要重跑）：

- 按周连排 4 周 + 目录 → 5 张，图号依次 `WTP-2026-W36–39`（图册号）、`WTP-2026-W36`…`WTP-2026-W39`（各张），目录张次写 `INDEX`；
- 按人成册 3 周 → 13 张（12 卷页 + 目录），`VOL 01…04` 各 3 页**连在一起**、卷内周从旧到新，图号 `WTP-2026-W35-01` 这种「周 + 人序号」；目录 12 行、4 道换卷横线（首行那道由 `:first-child` 抹掉）；
- 收录范围三档都改纸面不改看板：本周 11 张卡 → 只出未完成 7 张 → 搜「改图」沿用筛选 1 张（且卡片标题全部命中）；筛选后一张不剩时按周模式仍出一张空周页，按人模式直接没这一页；
- 上限：请求 8 周 + 按人成册 → 排到 3 周，摘要「13 张 · A3 横排 · WTP-2026-W37–39 · 按人成册 · 周数已压到 3（上限 16 张）」并标 `is-capped`，**只说一次**；重开对话框下拉仍是 8；
- 配平：塞 24 条压力任务后单张自然高 1900px → `--fc` 落在下限 `0.6600`、`is-spill` 命中 1 张、摘要「配平 66% · 1 张压到下限仍超纸面 · 出纸会续页」；正常密度 13 张全 `worst=1, spill=0`；
- 屏上适配（1440×900 同源 iframe）：`--fv≈0.9233`，纸张盒 1396×967，`documentElement.scrollWidth === clientWidth`（无横向溢出），看板被预览层遮住；
- `beforeprint` 兜底：堆栈为空时自动铺一张本周；预览条「改设置 / 晒图 / 回到看板」和 `Esc`（对话框 → 预览 → 设置）都走通；`__net` 全程 0，控制台无 error/warn。

占位页那一轮（补在 push 之后）：

- 区间没数据 + 按人成册 → 1 张占位页，图名「此页无图 · No Work To Plot」、张次 `NIL`、页眉右侧「占位」，`fit()` 仍 `worst=1, spill=0`；同一区间换成按周连排 → 2 张空周页 + 目录，**不出占位页**（空周页本身就是内容）；
- 筛选滤空 → 占位页文案说「看板当前的搜索与筛选把这一段全滤掉了」，不再误报「四个人都排空了」；
- 正常路径不变：按人成册两周仍是 9 张（8 卷页 + 目录）、看板 11 张卡、`__net` 0；
- 顶栏摘要 65 字在一行内不截断（`scrollWidth === clientWidth`）。

留档这一轮顺手把**密度 → 配平**的曲线扫了出来（单张、按周连排、灌合成任务，`fc` 就是 `min(1, 1047 / 自然高)`）：

| 卡数 | 15 | 19 | 21 | 23 | 25 | 29 | 33 | 51 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 自然高 px | 1138 | 1294 | 1450 | 1450 | 1623 | 1779 | 1935 | 2591 |
| `--fc` | .92 | .81 | **.72** | .72 | .66 | .66 | **.66** | .66 |
| `is-spill` | 0 | 0 | 0 | 0 | 1 | 1 | **1** | 1 |

三个读数：**约 13 项**开始掉出 100%（真实板上最满的一周是 11 项，所以日常永远配平 100%，这条曲线只能靠合成任务拍到）；**25 项**撞下限 `0.66`；**66% 能吞下的最大自然高是 1586px**（= 1047 ÷ 0.66），超过就是「压不动了，出纸会续页」——留档那两张分别停在曲线的 21 项和 33 项上。

**线上只读冒烟是可以做的**：`https://yiyuqiao2748.github.io/weekly-tracker/` 打开后只发生匿名 GET，`reachable` 闸门保证不会盲推；但**别在真站点上改数据或点「保存并同步」**，要验证上传路径仍然回 `?sync=1`。

push 完在真站点上复核过两件事（全程只读，控制台零条消息）：

- `/?sheet&from=2020-W01&count=2&mode=persons&scope=open` → 1 张纸、`.sheet-nil` 存在、图签栏读作「图名 …此页无图 / 张次 NIL / 周期 12.23 — 01.05 / 图号 WTP-2019-W52 – WTP-2020-W01」——占位页在部署产物里是活的，不只是本地那份 HTML；
- 裸 URL `https://yiyuqiao2748.github.io/weekly-tracker/` → 板子正常（第 39 周、四条人列 `SHT 01…04`、顶栏摘要齐全）。这台浏览器在 `github.io` 源下没存 Token，所以是 0 条任务的空板子——**这正好是占位页的来路**：空板子不崩、不出一堆白纸，只说清楚为什么没图。要看真数据那一侧仍然是各人自己 ⚙ 里配 Token。

## 测量陷阱（我在这儿翻过车，别再来一次）

1. **In-app Browser 面板在后台时，Chrome 不走动画时钟**，`transition` 的颜色会冻结在中间值。做任何颜色/对比度测量前，先注入 `*,*::before,*::after{transition:none !important;animation:none !important}`。曾经因此报出「83 处对比度不达标」和一个「蓝图下白字压白底」的假 bug——实际卡片背景早就正确切到了 `rgb(19,40,55)`。
2. **主题是从 localStorage 恢复的**。首选项没存过时按系统深浅色决定，所以点 `◐` 是「切换」而不是「设为蓝图」。要测某个主题就直接设 `document.body.dataset.theme` 并**断言令牌取值**（例如 `--paper-raised` 应为 `#132837`），别拿点击当事实。我曾有一轮「日览 + 蓝图各审一遍」其实两遍都在日览下跑的。
3. **对比度脚本要自己做 alpha 合成**（前景 alpha、逐层向上叠背景），并且跳过 `aria-hidden` 的子树；纯 `min/max` 写法会把所有比值算成 1。
4. **自动「横向溢出」扫描会被热区伪元素骗到**：`.chip` 的 `scrollWidth > clientWidth` 是那层向外扩的透明 `::after` 计入的，不是排版问题（chip 自然宽 = 盒宽，文字 = 内容盒）。
5. **拿不到像素时的替代手段够用**：`elementFromPoint` 逐点采样能验命中区域与误抢，`getBoundingClientRect` 能验版面，iframe（同源、给定 390×844）能验窄屏。In-app Browser 截图必须面板在前台（`visible=true, attached=true`）；后台就直接 `NATIVE_BROWSER_VIEWPORT_UNAVAILABLE`。**2026-09-21 起有兜底了**：Playwright 的 chromium-headless-shell（装在 `~/Library/Caches/ms-playwright/`），见「关键决策」第 9 条。
6. **`git` 的仓库根是 `weekly-tracker/`**，在上一级跑 `git status` 会报 not a repository；同时 `.preview/`、云端快照 JSON 都在仓库外，属于故意不外传的东西。
7. **内联 `<script>` 语法错误不会有人告诉你**：表现是 `SheetSet is not defined`、板子空白、`window.__net` undefined，看起来像「模块没加载」而不是「整个脚本没编译」。这台机器**没有 `node` 在 PATH 上**，所以编译检查两条路：改完先在 iframe 里 `eval('typeof SheetSet')` 一眼定生死；要精确定位就用 node-repl 把 `<script>` 段抽出来 `new vm.Script(src)`，错误行号是**相对脚本段**的（`index.html` 的行号 = 段内行号 + `<script>` 所在行 − 1）。这次翻车的原因很典型：往 `return \`<tr>\`…` 这种**跨行模板字符串**里插 `${}` 时把结尾的反引号留下了，字符串就地截断。
8. **纸面令牌在 `#print-stack` 上就地覆盖，读 `body` 会读到假值**。晒图无视主题：`#print-stack` 自己覆盖了一整套 `--paper*` / `--ink*`（强制白底黑字，打印机给不出深蓝底），所以蓝图主题下 `getComputedStyle(document.body).getPropertyValue('--paper-raised')` 仍是 `#132837`，而纸上那一格实测 `rgb(255,255,255)`。**要量纸面颜色就量 `.sheet-page` 或 `.sheet-card` 自己的 computed style**，别从 `body` 上取令牌再推断——我曾据此报出一个「蓝图出图会变深蓝底」的不存在缺陷。
9. **`?sheet` 直链页面里没有预览条**，因为它被 print 规则一起复制过来了。harness 把 `@media print` 的整段规则改成 screen 媒体（这是让 `?sheet` 能直接截图的机制），而 `@media print { #sheet-preview-bar { display:none } }` 也在其中，并带 `!important`。所以拍「配平 72%」那类要含预览条的图，**只能走不带 `?sheet` 的路**：`SheetSet.preview(cfg)` 从 JS 里铺纸（`shoot.py` 的 STRESS 那两类就是这么拍的）。同理别用 `#print-stack` 之外的元素判断预览是否生效。
10. **预览层是自滚动容器，截图的 clip 不能按页面坐标算**。`#print-stack` 是 `position:fixed; inset:0; overflow:auto`：`window.scrollY` **永远是 0**，要拍第 N 张纸必须滚 `#print-stack.scrollTop` 本身，坐标才是视口相对的；`full_page:true` 在这里只会拿到一屏。另外 clip 越界 Chromium 直接报 `Clipped area is either once outside the resulting image`（不是截断，是失败），所以 clip 的 `y+height` 要 `min(…, viewportHeight)` 夹一道，预览条这种 fixed 通栏元素得按**整个视口宽**裁（按纸的 x 裁会把「N 张 · A3 横排」那半句切掉）。
11. **`/tmp` 下的脚本别用 stdlib 模块名**：那份探针写了 `/tmp/struct.py`，`import` 时把标准库 `struct` 顶掉，报错是别处的 `ImportError`/循环导入，看起来像环境问题。同理 `.preview/` 里的文件名会进 `sys.path[0]`，别起名叫 `types.py` / `json.py`。

## 版面留档（截图）

`docs/screenshots/` 十一张，分两批。19:00 那批五张拍的是**看板**（日览 / 蓝图 / 修订表 / 手机 390），仍然有效；其中 `2026-09-21-print-sheet-a3.png` **已过期**（`744ccd2` 的旧 2×2 单张版面），只留着跟新出图图对照。22:00 那批六张是本轮的**图册版出图**。

**图里的项目名是假的。** 板子上跑的是打码种子：`.preview/anonymize_seed.py` 把 `seed.json` 的 `name` / `notes` 换成「示例项目 A…U」「对接人 A…G」（长度尽量与原句相当，免得换行位置变了），真实客户名、分店地名、对接人姓名只存在于云端 Gist 和各自浏览器的 localStorage，不进仓库。备注里的纯工作描述（`第4稿`、`换场地`、`明档修改中`）不含客户信息，原样留着。

**配平那两张还多了一层假**：板上最满的一周只有 11 项，纸面装得下，配平永远是 100% —— 想拍到「配平 72%」和「压到下限仍超纸面」，必须往内存里灌合成任务（`shoot.py` 的 STRESS 类，id 一律 `stress-*`，只活在临时 profile 里，`__net` 全程 0）。所以那两张图上的卡片密度**不代表任何真实的一周**，用来看观感和读数，不是用来看工作量。

```bash
python3 .preview/anonymize_seed.py                                   # → .preview/seed-anon.json
python3 .preview/build.py .preview/seed-anon.json .preview/preview-anon.html
python3 -m http.server 8899 --bind 127.0.0.1 --directory .preview &  # 服务起着
python3 .preview/shoot.py                                            # → docs/screenshots/ + docs/sheet-facts.json
python3 .preview/verify_sheet.py                                     # 改 CSS 后跑它，别只信眼睛
```

`shoot.py` 走的是无头 Chromium（Playwright，`chromium_headless_shell`），**不依赖 In-app Browser 面板在前台**——这是这轮换的手段，理由见「关键决策」第 9 条。它只打打码版：脚本开头有一句 `if "preview-anon" not in base: sys.exit(...)`，防止手滑拿真种子出图。重跑一次 `sheet-facts.json` 逐字节一致（版面读数确定），所以它是可以当回归用的。

| 图 | 看什么 |
| --- | --- |
| ![nil page](./docs/screenshots/2026-09-21-sheet-nil-page.png) | **占位页**：页眉「此页无图 · No Work To Plot」+ 右侧「占位」，图面正中虚线框写清为什么没图（这一段里没有未完成任务…），图签栏张次 `NIL`。纸面 1512×1047 一格未缩 |
| ![toc](./docs/screenshots/2026-09-21-sheet-toc-volumes.png) | **图纸目录**（按人成册两周，9 张）：`01…08` 张次、`WTP-2026-W38-01` 图号、`VOL 01…04` 卷号，卷与卷之间断一行（首卷不断），张次 `INDEX` |
| ![volume](./docs/screenshots/2026-09-21-sheet-volume-page.png) | **一卷的内页**：一个人一周的卡片走多列流（`sparse` 两列），页眉右侧「第 06 / 09 张」，图签栏带 `册` 一格 |
| ![weeks suite](./docs/screenshots/2026-09-21-sheet-weeks-suite.png) | **按周连排最满的一张**：四人四列通栏、每列一个 `分图 01…04` 图框带角裁切标记、图签栏贴住纸的下边线 |
| ![fit strip](./docs/screenshots/2026-09-21-sheet-fit-strip.png) | **配平读数**：预览条 `1 张 · A3 横排 · WTP-2026-W39 · 配平 72%`，下面整张纸等比缩到 72%（21 项 / 自然高 1450px）。这条只在非 `?sheet` 路径拍得到，原因见「测量陷阱」第 9 条 |
| ![spill](./docs/screenshots/2026-09-21-sheet-fit-spill.png) | **压到下限仍超纸面**：33 项、自然高 1935px，`fc` 卡在 `0.66` 不再压，纸外一圈锈色虚线（`.is-spill`），读数会写「1 张压到下限仍超纸面 · 出纸会续页」 |

| 图 | 看什么 |
| --- | --- |
| ![paper board](./docs/screenshots/2026-09-21-paper-board.png) | 日览配色整体版面：图签头、统计条、四条人列、已完成卡片上的 45° 剖面线、`新增` 卡片的内侧虚线（修订云线轻量版） |
| ![blueprint board](./docs/screenshots/2026-09-21-blueprint-board.png) | 蓝图夜览同一版面；`SHT 01…04` 图幅号、列头负荷迷你格、尺寸线进度条在深色下的读法 |
| ![blueprint revision](./docs/screenshots/2026-09-21-blueprint-revision-table.png) | 修订表展开态（版次 / 时间 / 修改 三栏，四行真实变更：优先级、两次进度、备注），`REV 4` 徽标与 `P1 高` 一起看 |
| ![print sheet](./docs/screenshots/2026-09-21-print-sheet-a3.png) | **已过期**：拍的是 `744ccd2` 的旧晒图版面（2×2 图幅 + 底部单块图签）。现在的出图是四列通栏 + 每张纸各自带图签，还多了目录页与连排/分册两种排法，看上面那批 |
| ![mobile 390](./docs/screenshots/2026-09-21-mobile-390.png) | 390×844 真实手机版面（同源 iframe 拍的，见 `.preview/mobile-frame.html`）：工具栏换行、人列纵向堆叠、`scrollWidth` 390 = 视口宽，无横向溢出 |

拍摄时统一注入 `transition:none;animation:none`（理由见上面「测量陷阱」第 1 条）。每轮的版面数字（张数、每页卡数、自然高、`fc`、`spill`、摘要原文、纸面/条底色）随图落在 `docs/sheet-facts.json`，比逐张肉眼读图可靠。

**蓝图主题下纸面仍然是白的，这是设计不是 bug**：`#print-stack` 就地覆盖了一整套纸面令牌（打印机给不出深蓝底，屏上预览与出纸因此同一份观感）。实测：`theme=blueprint` 时预览条 `rgb(19,40,55)`、纸面 `rgb(255,255,255)`。**别去读 `body` 上的 `--paper-raised`**，它照样是 `#132837`，读了会以为图拍错了。


## 还欠着的

1. **留档还剩的缺口**：拖拽进行中的版面（CAD 选择集观感）没拍；手机版只有一张首屏，长版面没连拍；出图预览层的**对话框**（晒图设置那五格）没拍；`?sheet` 页面上拍不到预览条（见「测量陷阱」第 9 条），要拍得走 STRESS 那条不带 `?sheet` 的路。占位页与配平两端（72% / 66% 下限）本轮已补齐。
2. **harness 的依赖没纳管**：`shoot.py` 与 `verify_sheet.py` 要 `pip3 install --user playwright` + `python3 -m playwright install chromium`（约 120MB，装在 `~/Library/Caches/ms-playwright`）。`.preview/` 整个目录仍在仓库外，换机器要重建（本轮已经见过一次 iCloud 搬目录）。要不要纳管，用户明确说这轮先改功能。
3. **团队配 Token**：另外三位同事各刷一次页面，然后各自在 ⚙ 设置里贴 Token 点「保存并同步」（每台浏览器单独配，Token 不共享）。
4. 未排期的候选方向（四条轨道里「出图模式」这轮落地，剩下的）：
   - 负荷条只有任务数，没有工时维度；
   - 修订表按任务卡展开，还没有按周汇总的全局修订页；
   - 配平只到「提示续页」，没有真正的**跨页续排**（同一人列自动分到两张纸、第二张标 `SHT 03/13 (续)`）；
   - 目录页只列到「张」，没有按人汇总的横表（谁在哪周有几项没完成）；
   - 墓碑连「谁删的」都不记，若要图纸级的签核链得先给墓碑加字段。

