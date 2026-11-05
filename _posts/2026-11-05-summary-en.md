---
layout: default
title: "Horizon Summary: 2026-11-05 (EN)"
date: 2026-11-05
lang: en
---

> From 48 items, 14 important content pieces were selected

---

**Technology News**
1. [Go Proposes JSON API Rework With encoding/json/v2 and jsontext](#item-tech-news-1) ⭐️ 8.0/10
2. [Anthropic reports progress on provable LLM inference](#item-tech-news-2) ⭐️ 8.0/10
3. [Reverse-engineering brings co-op multiplayer to DOS Wing Commander](#item-tech-news-3) ⭐️ 8.0/10
4. [Moonshot open-sources Kimi K3.1 Pro weights with ~1M-token context](#item-tech-news-4) ⭐️ 8.0/10
5. [Bluetooth HDT raises LE peak throughput to 7.5 Mbps for lossless audio](#item-tech-news-5) ⭐️ 8.0/10
6. [OpenAI pipeline reportedly finds 948 Linux privilege-escalation exploits](#item-tech-news-6) ⭐️ 8.0/10
7. [USTC&\#x27;s structRFM structure-guided RNA foundation model published in Nature](#item-tech-news-7) ⭐️ 8.0/10
8. [Tencent announces Hy4 open-weight LLM tuned for game development](#item-tech-news-8) ⭐️ 7.0/10
9. [IEEE Spectrum: AI Bug Hunting Exposes Decades of Security Debt](#item-tech-news-9) ⭐️ 7.0/10
10. [OpenAI to acquire Pierre Computer Company](#item-tech-news-10) ⭐️ 7.0/10
11. [Huginn weight sharing cuts storage but not HBM reads on B200](#item-tech-news-11) ⭐️ 7.0/10
12. [Huawei Said Ascend 960DT Customers Must Source Samsung, SK Hynix HBM](#item-tech-news-12) ⭐️ 7.0/10
13. [Apple to scan iCloud &\#x27;anyone with link&\#x27; shares starting in 27.3](#item-tech-news-13) ⭐️ 7.0/10
14. [Xiaomi trials Xiaomi-Robotics-1 agent in youth apartments](#item-tech-news-14) ⭐️ 7.0/10

---

## Technology News

<a id="item-tech-news-1"></a>
### [Go Proposes JSON API Rework With encoding/json/v2 and jsontext](https://go.dev/blog/jsonv2) ⭐️ 8.0/10

Go&\#x27;s official blog announced a proposed new JSON API built around encoding/json/v2 and the jsontext package. The redesign targets Go developers using the standard library&\#x27;s JSON handling, and the post presents design details for the new packages rather than a shipped replacement for the existing API. Because the supplied material is an announcement and proposal summary, no release date or migration guarantee is established.

hackernews · olexsmir · Nov 4, 17:52 · [Discussion](https://news.ycombinator.com/item?id=50369106)

**「Background」** Go&\#x27;s standard library has long handled JSON through encoding/json, and its MarshalIndent helper is a common way to emit readable JSON. The new proposal revisits that baseline with encoding/json/v2 and a separate jsontext package, so existing v1 code and habits are the reference point for judging migration costs.

**「Migration overhead」** Applications upgrading to Go 1.27 and adopting \`encoding/json/v2\` will need to audit their JSON output, since v2 changes several default encodings relative to v1; the published migration guide documents the per-scenario options and tags that restore or adjust the previous behavior. Teams that need custom error reporting or schema-specific parsing can use the lower-level \`encoding/json/jsontext\` package, which the proposal describes as operating purely at the syntactic layer without reflection.

**「Community Discussion」** One commenter said they generally like encoding/json/v2 but objected that dropping MarshalIndent makes migration and quick readable JSON output harder because the replacement code is complicated. Another reported using jsontext successfully for a parser that needed client-specific error messages while keeping strong performance, and a separate comment discussed schema-specialized SIMD parser generation as a performance direction.

<details><summary>References</summary>
<ul>
<li><a href="https://go.dev/blog/jsonv2">A new Go API for JSON - The Go Programming Language</a></li>
<li><a href="https://importstatic.com/go/go-json-v2-migration">Go JSON v 2 Migration : What Breaks in Go 1.27 | ImportStatic</a></li>
<li><a href="https://github.com/golang/go/issues/71497">encoding / json / v 2 : new API for encoding / json · Issue #71497...</a></li>

</ul>
</details>

**Tags**: `#Go`, `#JSON`, `#standard library`, `#API design`, `#parsing`

---

<a id="item-tech-news-2"></a>
### [Anthropic reports progress on provable LLM inference](https://www.anthropic.com/research/provable-inference) ⭐️ 8.0/10

Anthropic has published a research update on provable inference for large language models, aimed at letting a client verify that a provider actually ran a specified model on its request, particularly when the client cannot inspect the provider&\#x27;s weights. The work is presented as research progress, not a shipped production service; discussion of it cites roughly 90–100× compute overhead, a commitment of about 6.5 MB that covers some 16 million requests before renewal, and per-request proof verification taking 17 seconds on 24 threads or 21 seconds on a single thread. Those operating figures come from community analysis of the work, not an independent benchmark in the supplied material.

hackernews · ltononro · Nov 4, 17:17 · [Discussion](https://news.ycombinator.com/item?id=50368626)

**「Background」** Provable inference is meant to let a client check that a model provider actually ran a specified model on a given input. Anthropic&\#x27;s post frames its progress as work on a zkSNARK, a cryptographic proof that can attest to a computation without revealing the underlying data; an earlier open-source project, VerInf, had demonstrated zero-knowledge proofs for a 400B-parameter model on a single consumer DGX Spark using only hash-based commitments, with no trusted setup.

**「Impact」** For closed-model providers, proof-backed serving would be more practical for audit or offline verification than for latency-sensitive, high-volume inference if the cited 17–21 second verification times and 90–100× overhead hold; clients would also need the provider to refresh its commitment after roughly 16 million requests.

**「Community discussion」** Commenters weighed the cryptographic approach against cheaper alternatives: vessenes called it a good start and a significant improvement on prior zk results but argued that four independent inference providers running the same non-batched prompt could produce a probabilistic proof more cheaply, while nemo1618 noted that open-weight models can be verified by simply recomputing the output. Separately, neuwirth said the work builds on their VerInf project and accused Anthropic of providing &quot;very little attribution,&quot; a commenter claim rather than confirmed fact.

<details><summary>References</summary>
<ul>
<li><a href="https://github.com/JamesPetrie/VerInf">GitHub - JamesPetrie/VerInf</a></li>
<li><a href="https://github.com/JamesPetrie/VerInf/blob/main/README.md">VerInf/README.md at main · JamesPetrie/VerInf · GitHub</a></li>
<li><a href="https://www.anthropic.com/research/provable-inference">Progress on provable inference for large language models</a></li>

</ul>
</details>

**Tags**: `#provable inference`, `#LLM verification`, `#cryptography`, `#zero-knowledge proofs`, `#AI trust`

---

<a id="item-tech-news-3"></a>
### [Reverse-engineering brings co-op multiplayer to DOS Wing Commander](https://fireflyk64.github.io/wcmulti/) ⭐️ 8.0/10

A decade-long reverse-engineering project has brought co-op multiplayer to DOS Wing Commander, according to the author. The author says the work involved locating game-state variables, injecting calls into the game&\#x27;s functions, and synchronizing state over the network so players can fly the story missions together. The effort began in 2015, when the author noticed that the game state fit within the 64K data segment, and continued through memory-probing experiments. The item does not state a release version, distribution method, or compatibility beyond DOS.

hackernews · daniel\_rh · Nov 4, 18:51 · [Discussion](https://news.ycombinator.com/item?id=50369895)

**「Background」** Wing Commander&\#x27;s original DOS build stores its gameplay state in a single 64 KB data segment, a constraint the author began probing in 2015 while playing the game in DOSBox. That compact memory layout let the author and his brother locate state variables and inject calls into existing game functions, which became the foundation for synchronizing game state over a network.

**「Community discussion」** A commenter reports a related decompilation project that runs without DOSBox and produces native ARM64 and WASM builds, but says its multiplayer is still very basic. Another commenter describes using similar memory-location hunting to alter inventory, stats, and quest state in older games.

**Tags**: `#reverse engineering`, `#DOS games`, `#game modding`, `#multiplayer networking`, `#Wing Commander`

---

<a id="item-tech-news-4"></a>
### [Moonshot open-sources Kimi K3.1 Pro weights with ~1M-token context](http://platform.kimi.ai/) ⭐️ 8.0/10

Moonshot AI published open weights for Kimi K3.1 Pro on Hugging Face, described as the first model in the K3.1 family: a natively multimodal agent model with 2.8T total parameters, 104B active parameters and roughly 1M-token context, released in MXFP4 quantized form. The company also opened an API at platform.kimi.ai, where the model is selected as kimi-k3.1-pro and is compatible with OpenAI and Anthropic interfaces. These details come from a single Telegram post; no independent benchmark results or license terms were included, so how usable the weights are outside large-scale infrastructure is unconfirmed.

telegram · zaihuapd · Nov 4, 15:47

**「Background」** Moonshot&\#x27;s preceding open-weight release, Kimi K3, was already a 2.8T-parameter native multimodal agentic model built on Kimi Delta Attention \(KDA\) and Attention Residuals \(AttnRes\), with native vision and a 1-million-token context window. K3.1 Pro sits in that same 2.8T-parameter class and is described as the first model in the K3.1 series, with its weights published on Hugging Face in MXFP4 quantized form rather than at full precision.

**「Self-hosting hurdle pushes users to hosted APIs」** With 2.8T total parameters \(104B active\) released as MXFP4 weights, self-hosting Kimi K3.1 Pro requires a very large multi-GPU deployment, so most teams will reach it through the OpenAI/Anthropic-compatible kimi-k3.1-pro endpoint or third-party hosts. OpenRouter already lists multiple providers for the model and lets callers route by price, speed, or fastest provider, so throughput and cost can vary by provider at the same model ID.

**「Community discussion」** Hacker News commenters were divided: one argued the model is effectively out of reach for individuals because running it would take something like an 8x B300 node, while others called it &quot;benchmaxxed&quot; relative to DeepSeek V4.1-Flash and a competing Hy4 release. Another commenter said their own testing did not support the benchmaxxed characterization, describing a strong open model that is &quot;a bit off the frontier,&quot; and noted third-party providers already serving it through OpenRouter at higher throughput than Moonshot&\#x27;s own endpoint.

<details><summary>References</summary>
<ul>
<li><a href="https://huggingface.co/moonshotai/Kimi-K3">moonshotai/Kimi-K3 · Hugging Face</a></li>
<li><a href="https://phemex.com/news/article/moonshot-ai-opensources-kimi-k31-pro-weights-on-hugging-face-102388">Moonshot AI Releases Kimi K3.1 Pro Open Weights | Phemex News</a></li>
<li><a href="https://openrouter.ai/moonshotai/kimi-k3.1-pro">Kimi K 3 . 1 Pro - API Pricing &amp; Benchmarks | OpenRouter</a></li>

</ul>
</details>

**Tags**: `#open-weight LLMs`, `#multimodal AI`, `#Moonshot AI`, `#Kimi`, `#model releases`

---

<a id="item-tech-news-5"></a>
### [Bluetooth HDT raises LE peak throughput to 7.5 Mbps for lossless audio](https://www.bluetooth.com/press/bluetooth-high-data-throughput-opens-a-new-chapter-in-wireless-performance/) ⭐️ 8.0/10

The Bluetooth SIG announced on November 4 that it has adopted Bluetooth HDT \(High Data Throughput\), raising Bluetooth LE peak throughput from 2 Mbps to 7.5 Mbps—nearly four times—while improving capacity, energy efficiency, and reliability. HDT is an optional feature in Bluetooth Core 7.0 and is designed to coexist with older devices. Its first standardized application is high-end wireless audio supporting lossless and high-resolution formats, with initial products expected in 2027.

telegram · zaihuapd · Nov 5, 01:39

**「Background」** Bluetooth LE&\#x27;s previous maximum bit rate was 2 Mbps through its 2M PHY, the baseline against which the Bluetooth SIG describes Bluetooth HDT as nearly four times faster. HDT is an optional feature in Bluetooth Core 7.0, allowing coexistence with older devices, and its first standardized application is high-end wireless audio supporting lossless and high-resolution formats.

**「Impact」** For hardware makers and buyers, the 7.5 Mbps rate and lossless-audio benefits apply only to products that implement the optional Core 7.0 feature; HDT is intended to coexist with older Bluetooth devices, but support must be checked rather than assumed from Bluetooth LE alone.

<details><summary>References</summary>
<ul>
<li><a href="https://www.techpowerup.com/354478/bluetooth-sig-announces-bluetooth-high-data-throughput">Bluetooth SIG Announces Bluetooth High Data Throughput</a></li>
<li><a href="https://www.bluetooth.com/blog/bluetooth-le-will-soon-get-a-major-boost-in-speed-introducing-bluetooth-high-data-throughput-hdt/">Bluetooth ® connectivity will soon... | Bluetooth ® Technology Website</a></li>

</ul>
</details>

**Tags**: `#Bluetooth HDT`, `#wireless standards`, `#Bluetooth LE`, `#lossless audio`, `#hardware`

---

<a id="item-tech-news-6"></a>
### [OpenAI pipeline reportedly finds 948 Linux privilege-escalation exploits](https://openai.com/index/a-thousand-fewer-paths-to-root/) ⭐️ 8.0/10

OpenAI says its autonomous vulnerability-research pipeline reproduced 1,724 Linux kernel vulnerabilities in a single October 2026 scan and generated 948 working local-privilege-escalation exploits, plus 291 information-leak proofs of concept. The company put total API cost at $1,213,430, or about $1,279 per successful LPE exploit, with a lower effective figure of about $359 for actual exploit development. OpenAI also said third-party experts confirmed at least 10 novel exploitation techniques, including new page-grooming and data-only privilege-escalation methods. These are vendor claims reported in a brief secondary Telegram summary and have not been independently verified.

telegram · zaihuapd · Nov 5, 03:04

**「Why reproduction and exploit generation are separate hurdles」** Kernel vulnerability work is usually split into stages: automated discovery flags candidate bugs, a reproducer must then show the bug actually triggers, and only after that does someone attempt to turn it into a working exploit — with prioritization and validation remaining operational bottlenecks even as discovery gets cheaper to scale. OpenAI describes its system as a prototype run inside a controlled research environment that started from 2,308 candidate Linux kernel findings, of which 1,724 were dynamically reproduced before any exploits were generated.

**「Patch triage, not bounty revenue」** For Linux kernel maintainers and downstream distributions, the practical consequence is a validation and remediation workload: the 948 working LPEs would need confirmation and fixes, and the $1,279 average covers exploit generation only, not patching or deployment. The cited $18.9M–$66.3M bounty comparison is hypothetical, based on historical Pwn2Own and TyphoonPWN awards of $20,000–$70,000 per Linux kernel LPE, not payments OpenAI received.

**「Community discussion」** Commenters asked for the affected kernel subsystems, median age of the vulnerable code, and vulnerability types to judge how well the result would generalize beyond this scan. One skeptical commenter argued that the 948 exploits may collapse into far fewer root-cause vulnerabilities and cautioned that the post lacks supporting data.

<details><summary>References</summary>
<ul>
<li><a href="https://openai.com/index/a-thousand-fewer-paths-to-root/">A thousand fewer paths to root - OpenAI</a></li>
<li><a href="https://x.com/0xine/status/2118123220159410469">Isaac Evans on X: &quot;&quot;Historically, Pwn2Own and TyphoonPWN ...</a></li>
<li><a href="https://finance.biggo.com/news/d006d9a9-9bae-4c0a-8677-f89edd8cdb57">OpenAI&#x27;s AI Pipeline Uncovers 948 Linux Kernel Privilege ...</a></li>

</ul>
</details>

**Tags**: `#AI security`, `#vulnerability research`, `#Linux kernel`, `#exploit generation`, `#autonomous agents`

---

<a id="item-tech-news-7"></a>
### [USTC&\#x27;s structRFM structure-guided RNA foundation model published in Nature](https://news.ustc.edu.cn/info/1048/96798.htm) ⭐️ 8.0/10

University of Science and Technology of China researchers have built structRFM, a structure-guided RNA foundation model published online in Nature on November 5. The model incorporates base-pairing information from RNA secondary structure into sequence pretraining and was trained on roughly 21 million sequence-structure pairs; the team reports frontier-level results across multiple tasks. A companion MUSES method combines multiple secondary-structure predictions to reduce bias, and the Zfold 3D-structure module is reported to perform comparably to AlphaFold 3. The data, model weights and code have all been released.

telegram · zaihuapd · Nov 5, 04:49

**「Background」** structRFM’s approach was described earlier in an August 2025 bioRxiv preprint, which proposed integrating RNA base-pairing interactions into masked-language-model pretraining through a pair-matching operation. A companion GitHub repository describes the MUSES component as an ensemble of thermodynamics-, probability-, and deep-learning-based secondary-structure predictors intended to reduce annotation bias. The Nature paper reports the peer-reviewed publication of that framework.

**「Impact」** RNA researchers and developers can run, reproduce and adapt structRFM using the released data, weights and code, rather than treating the Nature paper as a closed result. The AlphaFold 3 comparison for Zfold remains a team-reported result, so users should validate 3D-structure accuracy on their own targets before relying on it.

<details><summary>References</summary>
<ul>
<li><a href="https://www.biorxiv.org/content/10.1101/2025.08.06.668731v2">A fully open structure-guided RNA foundation model for... | bioRxiv</a></li>
<li><a href="https://github.com/heqin-zhu/structRFM">heqin-zhu/ structRFM : structRFM : A fully open structure-guided RNA ...</a></li>

</ul>
</details>

**Tags**: `#RNA foundation models`, `#AI for science`, `#structural biology`, `#open source`, `#Nature publication`

---

<a id="item-tech-news-8"></a>
### [Tencent announces Hy4 open-weight LLM tuned for game development](https://hy.tencent.ai/research/hy4) ⭐️ 7.0/10

Tencent has announced Hy4, an open-weight LLM whose headline adaptation is game development: according to the announcement quoted by commenters, Tencent worked with developers at its Interactive Entertainment Group to curate training data and build evaluations covering feature implementation, gameplay logic, state tracking and asset pipelines, and adapted the model for Unreal Engine, Unity and Godot as well as multiplayer development. The same announcement concedes a &quot;notable gap&quot; to top proprietary models on challenging internal benchmarks for research-level mathematics, long-horizon coding, model self-improvement and advanced visual question answering, and says Tencent will keep scaling pre- and post-training to narrow it. Pricing is part of the pitch, with commenters citing a current 50% promotion and a Tencent promise of lower prices once the model goes open-weight; the supplied material gives no release date or license terms.

hackernews · Philpax · Nov 4, 14:11 · [Discussion](https://news.ycombinator.com/item?id=50365780)

**「Background」** Tencent previously released and open-sourced the Hy4 preview in August 2026 with 770B total parameters, 49B active parameters, and a context window exceeding 1M tokens, establishing the model family ahead of the full Hy4 announcement. Tencent&\#x27;s current release post says model weights and system cards are planned for release &quot;in the coming days,&quot; so open availability is an announced plan rather than a completed download at publication.

**「API cost and availability」** Developers can call the full Hy4 release through Tencent Cloud and OpenRouter, but the API list price—¥6 per million input tokens, ¥0.3 per million cached input tokens, and ¥18 per million output tokens—is estimated at roughly 5–6× the outgoing Hy3, so teams should model higher inference costs before migrating.

**「Community discussion」** Plotly&\#x27;s chriddyp reported that on a data-analytics benchmark Hy4 landed between GPT-6.1 Sol and GPT-6.1 Terra on the cost/accuracy frontier but was &quot;verrrry slow&quot;, running about 26 queries per question and up to 64 on some, with one query taking roughly an hour. minimaxir judged it slightly worse than Kimi 3.1M Pro, which he said released open weights the same day, yet much cheaper even excluding the promotion, while frangonf singled out Tencent&\#x27;s explicit acknowledgment of the proprietary-model gap as a point in its favor for using open models as tools.

<details><summary>References</summary>
<ul>
<li><a href="https://www.tencent.com/tencent-launches-hy4-joining-the-ranks-of-the-worlds-leading-open-source-ai-models/">Tencent Launches Hy4, Joining the Ranks of the World&#x27;s ...</a></li>
<li><a href="https://www.tencent.com/tencent-releases-and-open-sources-tencent-hy4-preview/">Tencent Releases and Open-Sources Tencent Hy4 preview</a></li>
<li><a href="https://www.eesel.ai/blog/tencent-hy4-pricing">Tencent Hy4 pricing 2026: API rates, hardware cost, rivals ...</a></li>
<li><a href="https://teamorouter.com/blogs/tencent-hy4-api">Tencent Hy4 API: Price, Specs and How to Call Hunyuan&#x27;s New ...</a></li>

</ul>
</details>

**Tags**: `#open-weight models`, `#Tencent`, `#LLM`, `#game development`, `#benchmarks`

---

<a id="item-tech-news-9"></a>
### [IEEE Spectrum: AI Bug Hunting Exposes Decades of Security Debt](https://spectrum.ieee.org/ai-in-cybersecurity-php2shell-vulnerability) ⭐️ 7.0/10

An IEEE Spectrum analysis argues that AI-assisted vulnerability discovery is forcing software maintainers and security teams to confront decades of accumulated security debt, with the PHP2Shell vulnerability as its hook. The piece is an argument about industry practice, not a report of new tooling, a measured breakthrough, or a shipped capability. It contends that the current wave of AI-found bugs is less a novel crisis than a long-standing backlog coming due.

hackernews · pseudolus · Nov 4, 11:52 · [Discussion](https://news.ycombinator.com/item?id=50364336)

**「Background」** PHP2Shell, the case used to frame the IEEE Spectrum argument, is a pair of memory-safety vulnerabilities tracked as CVE-2026-109618 and CVE-2026-109619 that affect PHP 5.4 through 8.5 and permit remote code execution. The attention around AI-assisted discovery of that bug is new, but major vulnerabilities predated modern AI; the operational problem remains locating affected systems and patching them in time.

**「Impact」** For maintainers and security teams, the practical burden is a larger set of vulnerabilities to triage in code that may have gone years without scrutiny; one commenter reports using AI to address five to seven years of technical debt, but says fixes still require substantial research and testing.

**「Community Discussion」** Commenters dispute the article&\#x27;s choice of PHP2Shell as the worst case: one argues HTTP2Shell/Brotli2Shell was arguably worse, citing a timeline of eight years in code, eight months with a fix in Git but no release, and at least four independent researchers finding it, which they say shows humans still sit on vulnerabilities. Others describe AI as lowering the cost of paying down five to seven years of technical debt, while cautioning that fixes still take time to research and test.

<details><summary>References</summary>
<ul>
<li><a href="https://en.wikipedia.org/wiki/PHP2Shell">PHP2Shell - Wikipedia</a></li>
<li><a href="https://www.pentestpartners.com/security-blog/php2shell-and-what-the-ai-headlines-are-missing/">PHP2Shell and what the AI headlines are missing | Pen Test ...</a></li>

</ul>
</details>

**Tags**: `#ai-cybersecurity`, `#vulnerability-discovery`, `#technical-debt`, `#security`, `#open-source-security`

---

<a id="item-tech-news-10"></a>
### [OpenAI to acquire Pierre Computer Company](https://openai.com/index/openai-to-acquire-pierre/) ⭐️ 7.0/10

OpenAI announced it will acquire Pierre Computer Company, according to a post on OpenAI&\#x27;s site. The available announcement contains no deal terms, price, closing timeline, or regulatory conditions, so the acquisition should be treated as announced rather than completed. Community commenters describe Pierre as the company behind Code.Storage, a git-based store for agent-generated code and artifacts, and a diffs library at diffs.com, with commenters naming Lovable, Bolt, Amp, and others as users; those product and customer details come from the discussion, not from the linked announcement.

hackernews · itunpredictable · Nov 4, 15:21 · [Discussion](https://news.ycombinator.com/item?id=50366863)

**「Background」** Pierre Computer Company is the startup behind Code Storage, a Git-based repository system for storing generated code and other machine-generated artifacts and tracking their history. OpenAI had already integrated Pierre tools into its Codex coding platform, and it frames the acquisition as improving Git workflows for developers and AI agents working in parallel.

**「Impact」** Teams that store generated code and artifacts on Pierre&\#x27;s git-based infrastructure, or depend on its diff tooling, face uncertainty about whether those products will continue independently, be folded into OpenAI&\#x27;s own git work, or change terms after the deal closes; the announcement as supplied gives no continuity or migration commitments.

**「Community Discussion」** Commenters connected the deal to OpenAI&\#x27;s earlier &quot;Scaling Git at OpenAI&quot; post and noted that HashiCorp founder Mitchell H. is described as a fan and possible investor in Pierre, while another commenter identified Pierre&\#x27;s founders as Jacob Thornton and Mark Otto, original Bootstrap developers. A recurring skeptical thread, voiced by one commenter, was that large AI labs may be acquiring successful developer-tool teams partly to capture how their products are built rather than only the products themselves.

<details><summary>References</summary>
<ul>
<li><a href="https://openai.com/index/openai-to-acquire-pierre/">OpenAI to acquire Pierre Computer Company , Inc. | OpenAI</a></li>
<li><a href="https://the-decoder.com/">Artificial Intelligence: News, Business, Science | THE DECODER</a></li>
<li><a href="https://www.theverge.com/openai">OpenAI | The Verge</a></li>

</ul>
</details>

**Tags**: `#openai`, `#acquisitions`, `#developer-tools`, `#git`, `#ai-coding-agents`

---

<a id="item-tech-news-11"></a>
### [Huginn weight sharing cuts storage but not HBM reads on B200](https://www.reddit.com/r/MachineLearning/comments/1xnskvt/do_looped_transformers_save_hbm_traffic_profiling/) ⭐️ 7.0/10

A new empirical profile of Huginn-style looped transformers on an Nvidia B200 finds that reusing one weight tensor across iterations cuts storage but does not by itself eliminate per-iteration HBM reads. In a chain of eight matmuls, one shared 72 MiB weight ran 24% faster than eight identical copies and read almost nothing from HBM; at 288 MiB, above L2 capacity, that advantage disappeared. In a full Huginn Core teaching implementation with random weights, eight iterations took about 8x as long as one and read about 8x as much HBM data. The author published code and raw Nsight Compute data and asks whether persistent kernels could keep recurrent weights on chip across iterations.

reddit · r/MachineLearning · /u/2dayyy6 · Nov 4, 16:26

**「Background」** Huginn is a looped transformer in which a single tied iterative block sits between untied prelude and coda stacks and is applied repeatedly, injecting the prelude representation at each iteration. The Geiping et al. work behind it trained the model on up to 32 loops and scaled it to 64 loops at test time, so the same recurrent weights are exercised many times per forward pass — the property that makes weight reuse in HBM an interesting question.

**「Impact」** Developers evaluating weight-tied or looped architectures cannot assume parameter sharing lowers HBM bandwidth; the measurements indicate they would need on-chip weight residency or other kernel-level reuse to avoid repeated reads. This finding is limited to the teaching implementation with random weights and does not establish trained-model or end-to-end performance.

<details><summary>References</summary>
<ul>
<li><a href="https://www.lesswrong.com/posts/PLisnSFir8y5AHkmP/how-concerned-should-we-be-about-astra-s-recurrent">How concerned should we be about Astra&#x27;s recurrent architecture ?</a></li>
<li><a href="https://huskydoge.github.io/husky-blog/posts/recursive_models/towards-looped-models-done-right/">Towards Looped Models Done Right | Husky&#x27;Log</a></li>

</ul>
</details>

**Tags**: `#looped-transformers`, `#hbm-bandwidth`, `#gpu-profiling`, `#weight-sharing`, `#nsight-compute`

---

<a id="item-tech-news-12"></a>
### [Huawei Said Ascend 960DT Customers Must Source Samsung, SK Hynix HBM](https://thenextweb.com/news/huawei-hbm-smuggling-samsung-sk-hynix-ascend-960dt) ⭐️ 7.0/10

Huawei has reportedly told some customers that its next flagship AI chip, Ascend 960DT, will mainly use Samsung and SK hynix HBM and that customers must source the memory themselves, according to The Information as summarized by The Next Web. The report attributes the arrangement to insufficient Chinese HBM capacity. It also describes HBM being soldered onto low-performance processors, declared under processor codes and shipped to Hong Kong, then carried into mainland China and removed; a Shenzhen chip broker said a single HBM3E chip now costs about $4,000, up from hundreds of dollars a year earlier. These claims come from a secondhand Telegram summary and were not independently corroborated in the supplied material.

telegram · zaihuapd · Nov 4, 14:52

**「Background」** US export rules bar Samsung and SK hynix from supplying advanced HBM to Chinese customers, while domestic Chinese HBM suppliers are reportedly struggling to meet demand \(tool-2-1, tool-2-2\). Those restrictions make HBM a scarce, separately sourced component for Chinese AI accelerators such as Huawei&\#x27;s Ascend line.

**「Impact」** Customers named in the report would have to secure their own Samsung or SK hynix HBM rather than receiving a complete memory-integrated system from Huawei, adding procurement and cost exposure; the cited roughly $4,000 per HBM3E price illustrates that risk, though Huawei has not publicly confirmed the sourcing requirement.

<details><summary>References</summary>
<ul>
<li><a href="https://thenextweb.com/news/huawei-hbm-smuggling-samsung-sk-hynix-ascend-960dt">Huawei tells some clients to source their own HBM, report says</a></li>
<li><a href="https://www.trendforce.com/news/2026/11/03/news-china-reportedly-obtains-smuggled-hbm-via-server-packages-huawei-960dt-faces-domestic-hbm-shortage/">[News] China Reportedly Obtains Smuggled HBM via Server ...</a></li>

</ul>
</details>

**Tags**: `#Huawei`, `#AI chips`, `#HBM`, `#semiconductor supply chain`, `#export controls`

---

<a id="item-tech-news-13"></a>
### [Apple to scan iCloud &\#x27;anyone with link&\#x27; shares starting in 27.3](https://9to5mac.com/2026/11/04/with-ios-27-3-apple-will-start-checking-icloud-public-links-for-harmful-content/) ⭐️ 7.0/10

Apple says that starting with iOS, iPadOS, macOS and visionOS 27.3, iCloud content shared through “anyone with a link” links will be checked for harmful material. Content shared only with specified people is outside the described scope. If Apple deems content harmful, it reserves the right to move, refuse, modify or delete it, and may restrict or disable uploaders’ accounts or refer cases to law enforcement. The source does not define “harmful” or describe appeal procedures, and the scanning is an announced plan for version 27.3 rather than a shipped capability.

telegram · zaihuapd · Nov 5, 02:11

**「How public iCloud links differ」** iCloud lets users share files and photos either with specified people or through an “Anyone with the Link” URL that opens without naming recipients. Apple’s policy applies specifically to that public-link mode, a distinction that matters because such URLs can circulate beyond the original sharer’s intended audience.

**「Impact」** For affected users, public-link sharing carries content-review and account-restriction risk, while Apple describes named-recipient sharing as outside this scope.

**Tags**: `#Apple`, `#iCloud`, `#content moderation`, `#privacy`, `#platform policy`

---

<a id="item-tech-news-14"></a>
### [Xiaomi trials Xiaomi-Robotics-1 agent in youth apartments](https://weibo.com/1749127163/5361796274981767) ⭐️ 7.0/10

Xiaomi has begun trialing a robotics agent system in its youth apartments, using the Xiaomi-Robotics-1 embodied foundation model as the base for a closed loop that spans data collection, model inference and task execution. The company says the agent can autonomously plan and complete desktop tidying, trash cleanup, sorting and returning items, room inspection and whole-apartment rechecks. Xiaomi reports that a long-horizon validation ran continuously for more than 30 minutes, covered three rooms and included more than 50 tasks; the disclosure is a social-media post and does not give failure rates, hardware details, pricing or availability.

telegram · zaihuapd · Nov 5, 08:19

**「The model behind the trial」** The trial runs on Xiaomi-Robotics-1, which Xiaomi released on July 16 as an embodied foundation model for real-world mobile manipulation tasks. Per its paper page and model listing, it was trained in two stages: large-scale embodiment-free \(UMI\) pre-training across more than 1,700 scenarios, followed by post-training on cross-embodiment data that included 7,200+ hours of in-house real-robot demonstrations, which the authors describe as allowing efficient fine-tuning on complex dexterous tasks.

**「Impact」** For developers and prospective users, the pilot is confined to Xiaomi youth apartments, and the post discloses no failure rate, hardware configuration, availability date or price, so the 30-minute, three-room, 50-task run is not yet an accessible or independently verified product capability.

<details><summary>References</summary>
<ul>
<li><a href="https://huggingface.co/papers/2607.15330">Paper page - Xiaomi - Robotics - 1 : Scaling Vision-Language-Action...</a></li>
<li><a href="https://www.aibase.com/news/29652">Xiaomi Launches Embodied Intelligence Base Model ...</a></li>
<li><a href="https://theresanaiforthat.com/model/xiaomi-robotics-1/">Xiaomi - Robotics - 1 | AI Model | There&#x27;s An AI For That</a></li>

</ul>
</details>

**Tags**: `#robotics`, `#embodied AI`, `#AI agents`, `#Xiaomi`, `#consumer robotics`

---