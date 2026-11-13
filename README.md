# 企业智能体系统 · 功能快照

> **在线地址（推荐）**：[https://huobuzhe.github.io/showcase/](https://huobuzhe.github.io/showcase/) —— 纯静态页，打开就能看，不需要装任何东西
>
> 备用入口：[index.html](https://huobuzhe.github.io/showcase/index.html) · [showcase.html](https://huobuzhe.github.io/showcase/showcase.html) · [单文件版 showcase-standalone.html](https://huobuzhe.github.io/showcase/showcase-standalone.html) · [源码仓库 huobuzhe/showcase](https://github.com/huobuzhe/showcase)

> **链接怎么点**：本页所有链接都是标准 Markdown 链接（[文字](网址)），请点文字，不要复制整行；网址末尾停在 <code>/</code> 或 <code>.html</code>，不要把星号、括号或中文说明一起粘进地址栏。若在线地址偶尔返回 404（网络 / CDN 波动），按第三节把仓库下载到本机双击打开，内容完全一致。

## 一、这个网页是做什么的

这是给**招聘方 / 面试官**看的作品集展示页：把两个 Agent 应用工程项目的**本机真实运行记录**做成可点选的网页。选中一个输入，页面就展开当时系统真实返回的输出、检索引用、评测结论与压测指标。

它不是在线服务，也不连接任何后端：所有数据已经内嵌在 HTML 里，是 2026-11-13 的静态快照。因此不需要 API Key、数据库、Docker 或云主机，断网也能打开。真正可运行的工程在下面第四节的两个 GitHub 仓库里，各自 README 写了完整的前置条件、知识点、技术栈与启动命令。

## 二、页面里具体有什么

页面共 4 张卡片、15 个可点选的运行实例，默认完全空白；点按钮或选下拉框才渲染「系统回答」，随时可用「清空 / 清空全部」回到默认状态。段与段之间用横线分隔，引文放在可滚动的小窗口里，表格带边框线且字号更小。

| 卡片 | 实例数 | 具体内容 |
|---|---|---|
| **循证医疗问答与证据溯源** | 5 | 正常回答（附 3 条引用）、缓存命中、语料外问题证据不足拒答、过滤器空证据拒答、引用回链（原文 + 页码 + 版面定位） |
| **食养工作流与图谱推理平台** | 6 | 子块一「LangGraph 节点式工作流」2 例：完整流式输出、无食材时的降级路径；子块二「多跳知识图谱推理」4 例：食材 + 病症的禁忌推理命中 / 未命中、知识图谱规模 |
| **评测门禁与性能回归** | 4 | 分层评测 + 门禁结论（BLOCKED）、只读门禁快照、并发压测报告（QPS / P99 表格）、只读压测快照 |
| **系统状态（本机实测）** | — | 置底，列出代理元信息、服务端口、鉴权方式、知识图谱规模等本机环境事实 |

每个实例都标注了对应的真实接口、输入参数、HTTP 状态与本机耗时；评测报告里原始文件自带的 <code>pipeline_selfcheck</code> 口径说明原样保留，**不把它当作系统质量结论**。

技术上是零依赖、零构建的纯 HTML / CSS / JavaScript：[index.html](index.html) 与 [showcase.html](showcase.html) 是同一份页面，[real.css](real.css) 是样式，[showcase-standalone.html](showcase-standalone.html) 是样式已内联的单文件版。

## 三、别人如何在电脑上查看、使用和下载

### 3.1 在线直接看（最快）

打开 [https://huobuzhe.github.io/showcase/](https://huobuzhe.github.io/showcase/) 即可，手机、平板、电脑浏览器都能看，不用注册、不用装东西。若这个地址打不开，换 [index.html 入口](https://huobuzhe.github.io/showcase/index.html) 或 [showcase.html 入口](https://huobuzhe.github.io/showcase/showcase.html)。

### 3.2 下载到电脑（三种方式，任选一种）

**方式 A · 只下一个文件（最省事）**：打开 [showcase-standalone.html](https://github.com/huobuzhe/showcase/blob/main/showcase-standalone.html) → 点 <code>Raw</code> → 右键「另存为」保存为 <code>showcase-standalone.html</code>。这个文件把 CSS 全部内联，双击即可打开，不需要其它文件、不需要联网。

**方式 B · 下载整站**：打开 [https://github.com/huobuzhe/showcase](https://github.com/huobuzhe/showcase) → 绿色 <code>Code</code> 按钮 → <code>Download ZIP</code> → 解压，得到 <code>index.html</code> / <code>showcase.html</code> / <code>real.css</code> / <code>showcase-standalone.html</code> / <code>README.md</code>。

**方式 C · 用 Git（方便以后拿更新）**：

~~~bash
git clone https://github.com/huobuzhe/showcase.git
cd showcase
~~~

以后更新只需在该目录执行 <code>git pull</code>。

### 3.3 打开哪个文件、怎么打开

- **双击打开**：解压（或 clone）后双击 <code>index.html</code>，<code>file://</code> 协议下全部功能可用；也可以双击 <code>showcase.html</code>（同一份页面）或 <code>showcase-standalone.html</code>（单文件）。
- **用本地小服务器打开（可选）**：在文件所在目录执行下面这条命令，然后浏览器访问 [http://127.0.0.1:8080/](http://127.0.0.1:8080/)：

~~~bash
python -m http.server 8080
~~~

（Windows PowerShell 与 Linux/macOS 终端命令相同；若 <code>python</code> 不可用，试 <code>py -m http.server 8080</code> 或 <code>python3 -m http.server 8080</code>。这只是为了用 http 打开，双击 <code>index.html</code> 效果一样。）

### 3.4 页面怎么用（一步一步）

1. 打开页面后默认是**完全空白**的，这是正常状态。
2. 在任意卡片里点一个输入按钮（例如「高血压患者日常食养」），或在下拉框里选一条输入。
3. 页面自动滚动到「系统回答」，展开当时的输出、引用明细（长引文在小窗口里上下滑动）、链路耗时与各节点耗时表格。
4. 换一个例子继续看；点卡片右上「清空」或导航「清空全部」回到默认空白状态。
5. 顶部导航可直接跳到「循证医疗问答与证据溯源」「食养工作流与图谱推理平台」「评测门禁与性能回归」「系统状态（本机实测）」。

全程不需要联网、不需要登录、不需要 API Key。需要说明：这里展示的是**历史运行快照**，不是实时问答。若想在本机跑起真实服务，请打开下面两个项目仓库的 README，按其中的「运行前置做法」和「快速开始」逐条执行命令。

## 四、真实数据来源与对应链接

15 条实例全部来自 2026-11-13 本机两个项目的真实运行，不是 mock 数据。对应关系如下（链接均可直接点开）：

| 展示内容 | 来源接口 / 报告 | 对应仓库（点开可看源码与证据） |
|---|---|---|
| 医疗问答 5 例（含引用回链） | MedEviRAG <code>POST /v1/ask</code>、<code>GET /v1/citations/{chunk_id}</code> | [MedEviRAG 仓库](https://github.com/huobuzhe/MedEviRAG)（<code>docs/evidence/</code> 内有评测报告 JSON） |
| 食养工作流与图谱 6 例 | AI私厨 <code>POST /chat/stream</code>、<code>GET /kg/ask</code> | [AI私厨仓库](https://github.com/huobuzhe/ai_chief)（<code>reports/</code> 内有压测报告） |
| 评测与压测 4 例 | MedEviRAG eval 门禁报告 + AI私厨 压测报告 | [AI私厨仓库](https://github.com/huobuzhe/ai_chief) 与 [MedEviRAG 仓库](https://github.com/huobuzhe/MedEviRAG) |
| 本展示页源码 | 静态 HTML / CSS / JS | [showcase 仓库](https://github.com/huobuzhe/showcase) |
| 线上快照 | GitHub Pages | [在线展示页](https://huobuzhe.github.io/showcase/) |

两个项目的仓库（导入 PR 描述里也写了包含 / 不包含哪些内容）：

- [AI私厨 · 食养工作流与图谱推理平台](https://github.com/huobuzhe/ai_chief) —— LangGraph StateGraph 节点式工作流、Neo4j 多跳图谱推理、流式问答、鉴权限流、监控与压测；[导入 PR #1](https://github.com/huobuzhe/ai_chief/pull/1)。
- [MedEviRAG · 循证医疗问答与证据溯源](https://github.com/huobuzhe/MedEviRAG) —— RAG 检索 / 重排 / 生成 / 引用校验、证据分级与拒答、分层评测与 CI 回归门禁；[导入 PR #1](https://github.com/huobuzhe/MedEviRAG/pull/1)。

诚实声明：评测报告标注的 <code>pipeline_selfcheck</code> / <code>llm_mode=fake</code> 是流水线自检口径，不代表系统质量或临床有效性；压测数字只代表本机环境；页面为静态快照，与实时演示站互不影响。项目仅供学习与工程演示，不构成医疗建议。
