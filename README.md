# 企业智能体系统 · 功能快照

> 在线地址：**https://huobuzhe.github.io/showcase/**（纯静态页，打开就能看，不需要装任何东西）

## 一、这个网页是做什么的

这是给**招聘方 / 面试官**看的作品集展示页：把两个 Agent 应用工程项目的**本机真实运行记录**做成可点选的网页。选中一个输入，页面就展开当时系统真实返回的输出、检索引用、评测结论与压测指标。

它不是在线服务，也不连接任何后端：所有数据已经内嵌在 HTML 里，是 2026-11-13 的静态快照。因此不需要 API Key、数据库、Docker 或云主机，断网也能打开。真正可运行的工程在下面第四节的两个 GitHub 仓库里。

## 二、页面里具体有什么

页面共 4 张卡片、15 个可点选的运行实例，默认完全空白；点按钮或选下拉框才渲染「系统回答」，随时可用「清空 / 清空全部」回到默认状态。段与段之间用横线分隔，引文放在可滚动的小窗口里，表格带边框线且字号更小。

| 卡片 | 实例数 | 具体内容 |
|---|---|---|
| **循证医疗问答与证据溯源** | 5 | 正常回答（附 3 条引用）、缓存命中、语料外问题证据不足拒答、过滤器空证据拒答、引用回链（原文 + 页码 + 版面定位） |
| **食养工作流与图谱推理平台** | 6 | 子块一「LangGraph 节点式工作流」2 例：完整流式输出、无食材时的降级路径；子块二「多跳知识图谱推理」4 例：食材 + 病症的禁忌推理命中 / 未命中、知识图谱规模 |
| **评测门禁与性能回归** | 4 | 分层评测 + 门禁结论（BLOCKED）、只读门禁快照、并发压测报告（QPS / P99 表格）、只读压测快照 |
| **系统状态（本机实测）** | — | 置底，列出代理元信息、服务端口、鉴权方式、知识图谱规模等本机环境事实 |

每个实例都标注了对应的真实接口、输入参数、HTTP 状态与本机耗时；评测报告里原始文件自带的 pipeline_selfcheck 口径说明原样保留，**不把它当作系统质量结论**。

技术上是零依赖、零构建的纯 HTML / CSS / JavaScript：index.html 与 showcase.html 是同一份页面，real.css 是样式，另有一个样式已内联的单文件版 showcase-standalone.html。

## 三、别人如何在电脑上查看、使用和下载

**在线直接看**：打开 https://huobuzhe.github.io/showcase/ 即可，手机上也能看。

**下载到电脑（三种方式，任选）**：

1. 单文件版：在仓库里下载 <code>showcase-standalone.html</code>（或浏览器打开后「右键 → 另存为」），双击就能打开，样式已内联，不需要其它文件。
2. 下载整站：打开 https://github.com/huobuzhe/showcase → 绿色 <code>Code</code> 按钮 → <code>Download ZIP</code>，解压后得到 index.html / showcase.html / real.css。
3. 用 Git：运行 <code>git clone https://github.com/huobuzhe/showcase.git</code>，之后还能 <code>git pull</code> 拿更新。

**本地打开**：双击 <code>index.html</code>（file:// 直接可用）；或在该目录执行 <code>python -m http.server 8080</code> 后访问 <code>http://127.0.0.1:8080/</code>。

**怎么用**：在卡片里点一个输入的按钮，或在下拉框里选一个输入 → 页面滚动到「系统回答」，展开输出、引用明细（可上下滑动）、耗时表格 → 换一个例子继续看，或点「清空」复位。全程不需要联网、不需要登录。

需要说明：这里展示的是**历史运行快照**，不是实时问答。若想在本机跑起真实服务，请看两个项目仓库里的 README 与 .env.example（需要自备 API Key、Docker 与语料）。

## 四、真实数据来源与对应链接

15 条实例全部来自 2026-11-13 本机两个项目的真实运行，不是 mock 数据。对应关系如下：

| 展示内容 | 来源接口 / 报告 | 对应仓库（点开可看源码与证据） |
|---|---|---|
| 医疗问答 5 例（含引用回链） | MedEviRAG <code>POST /v1/ask</code>、<code>GET /v1/citations/{chunk_id}</code> | **https://github.com/huobuzhe/MedEviRAG**（docs/evidence/ 内有评测报告 JSON） |
| 食养工作流与图谱 6 例 | AI私厨 <code>POST /chat/stream</code>、<code>GET /kg/ask</code> | **https://github.com/huobuzhe/ai_chief** ← **AI私厨 的仓库链接**（reports/ 内有压测报告） |
| 评测与压测 4 例 | MedEviRAG eval 门禁报告 + AI私厨 压测报告 | **https://github.com/huobuzhe/ai_chief** 与 **https://github.com/huobuzhe/MedEviRAG** |
| 本展示页源码 | 静态 HTML / CSS / JS | **https://github.com/huobuzhe/showcase** |
| 线上快照 | GitHub Pages | **https://huobuzhe.github.io/showcase/** |

- **AI私厨（食养工作流与图谱推理平台）**：https://github.com/huobuzhe/ai_chief —— LangGraph StateGraph 节点式工作流、Neo4j 多跳图谱推理、流式问答、鉴权限流、监控与压测。
- **MedEviRAG（循证医疗问答与证据溯源）**：https://github.com/huobuzhe/MedEviRAG —— RAG 检索/重排/生成/引用校验、证据分级与拒答、分层评测与 CI 回归门禁。

诚实声明：评测报告标注的 pipeline_selfcheck / llm_mode=fake 是流水线自检口径，不代表系统质量或临床有效性；压测数字只代表本机环境；页面为静态快照，与实时演示站互不影响。项目仅供学习与工程演示，不构成医疗建议。
