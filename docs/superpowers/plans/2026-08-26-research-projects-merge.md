# Research and Projects Merge Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Consolidate the homepage's Research and Projects lists into one four-item Research section and place the transportation image directly below it.

**Architecture:** Reuse the approved static HTML list and bilingual spans in the existing top Research location. Merge Computable Social Analytics into the computational-social-science item, then delete the lower duplicate Projects block without touching publications, Teaching, or scripts.

**Tech Stack:** Static HTML, lxml structural checks, Node.js syntax checking, Git whitespace validation.

---

### Task 1: Establish the failing merge contract

**Files:**
- Test: `index.html`
- Test: `index_backup.html`

- [ ] **Step 1: Run the structural contract before editing**

```bash
python3 - <<'PY'
from lxml import html
from pathlib import Path

for path in ("index.html", "index_backup.html"):
    doc = html.fromstring(Path(path).read_text())
    research = doc.xpath('//h2[contains(normalize-space(string(.)), "Research")]')
    projects = doc.xpath('//h2[contains(normalize-space(string(.)), "Projects")]')
    assert len(research) == 1, (path, "Research headings", len(research))
    assert len(projects) == 0, (path, "Projects headings", len(projects))
    items = research[0].xpath('following-sibling::ul[1]/li')
    assert len(items) == 4, (path, "Research items", len(items))
    third = items[2]
    assert third.xpath('.//a[@href="https://mo.zju.edu.cn/css"]')
    assert third.xpath('.//a[@href="https://mo.zju.edu.cn/css/#/pub"]')
    images = doc.xpath('//img[@src="images/ZJUCSS-transportation.jpeg"]')
    assert len(images) == 1, (path, "transportation images", len(images))
    publications = doc.xpath('//*[@id="publications-list"]')[0]
    assert items[-1].sourceline < images[0].sourceline < publications.sourceline
print("research merge contract verified")
PY
```

Expected: FAIL because each page still has a separate Projects heading and the top Research list has only two items.

### Task 2: Merge the bilingual live page

**Files:**
- Modify: `index.html:114-122`
- Modify: `index.html:371-384`

- [ ] **Step 1: Replace the current top Research list with the approved four-item list**

```html
<a name="research"></a>
<h2><span class="en">Research</span><span class="zh">研究方向</span></h2>
<ul>
<li><b><span class="en">Multi-agent Social Simulation</span><span class="zh">多智能体社会仿真</span></b>: <span class="en"><a href="https://github.com/wuchaozju/GAWorld">GAWorld</a> provides a controllable and replayable generative multi-agent environment for urban social-behavior experiments; <a href="https://mo.zju.edu.cn/css/fos/">FOS</a> supports social-system experiment design, branching, observation, comparison, and intervention evaluation.</span><span class="zh"><a href="https://github.com/wuchaozju/GAWorld">GAWorld</a> 提供面向城市社会行为实验的可控制、可回放生成式多智能体环境；<a href="https://mo.zju.edu.cn/css/fos/">FOS</a> 支持社会系统实验设计、分支推演、过程观测、对比分析与干预评估。</span></li>
<li><b><span class="en">Distributed Artificial Intelligence</span><span class="zh">分布式人工智能</span></b>: <span class="en">Research on data pricing and contribution evaluation; federated learning under non-IID data, heterogeneous models, and changing participation; and decentralized or personalized collaboration, privacy, robustness, and model fusion.</span><span class="zh">围绕数据定价与贡献评估，研究非独立同分布数据、模型异构和动态参与条件下的联邦学习，以及去中心化与个性化协同、隐私保护、鲁棒性和模型融合。</span></li>
<li><b><a href="https://mo.zju.edu.cn/css"><span class="en">Computational Social Science (Computable Social Analytics)</span><span class="zh">计算社会科学（可计算社会分析）</span></a></b>: <span class="en">Data-driven and computational approaches to public policy and social systems, including government-attention allocation and evolution, policy evaluation, group interaction and social behavior, and applications such as intelligent transportation, smart cities, and neuro-management. We established <a href="https://mo.zju.edu.cn/css/#/pub">ZJUCCS</a> as a hub for this research.</span><span class="zh">以数据驱动和计算方法研究公共政策与社会系统，包括政府注意力的配置与演化、政策评估、群体互动与社会行为，以及智能交通、智慧城市和神经管理等应用。我们建立了 <a href="https://mo.zju.edu.cn/css/#/pub">ZJUCCS</a>，作为该研究领域的枢纽。</span></li>
<li><b><span class="en">Mo Platform</span><span class="zh">Mo 平台</span></b>: <span class="en"><a href="https://momodel.ai">Mo</a> is an online platform for AI modelling, experimentation, and education, with public, <a href="http://mo.zju.edu.cn">ZJU</a>, <a href="https://uni.momodel.cn">university</a>, <a href="https://hv.momodel.cn">higher vocational education</a>, <a href="https://edu.momodel.cn">high school</a>, and <a href="https://k12.momodel.cn">K-12</a> versions.</span><span class="zh"><a href="https://momodel.ai">Mo</a> 是一个面向人工智能建模、实验与教育的在线平台，提供公开版、<a href="http://mo.zju.edu.cn">浙大版</a>、<a href="https://uni.momodel.cn">高校版</a>、<a href="https://hv.momodel.cn">高职版</a>、<a href="https://edu.momodel.cn">高中版</a>和<a href="https://k12.momodel.cn">K-12版</a>。</span></li>
</ul>
<IMG BORDER=20 ALIGN="center" SRC="images/ZJUCSS-transportation.jpeg" height=400>
```

- [ ] **Step 2: Delete the lower Projects block**

Delete the later block beginning with the `<P>` immediately before `<h2><span class="en">Projects</span>` and ending with its trailing `<hr>`. This removes the duplicate four-item list, its old copy of the image, and the local `top` link.

After deletion, the Teaching section's existing trailing rule must be followed directly by the pre-existing commented research-projects block:

```html
<hr>

<!--
<a name="research-projects"></a>
```

### Task 3: Merge the English backup page

**Files:**
- Modify: `index_backup.html:75-83`
- Modify: `index_backup.html:332-345`

- [ ] **Step 1: Replace the backup Research list with the English equivalent**

```html
<a name="research"></a>
<h2>Research</h2>
<ul>
<li><b>Multi-agent Social Simulation</b>: <a href="https://github.com/wuchaozju/GAWorld">GAWorld</a> provides a controllable and replayable generative multi-agent environment for urban social-behavior experiments; <a href="https://mo.zju.edu.cn/css/fos/">FOS</a> supports social-system experiment design, branching, observation, comparison, and intervention evaluation.</li>
<li><b>Distributed Artificial Intelligence</b>: Research on data pricing and contribution evaluation; federated learning under non-IID data, heterogeneous models, and changing participation; and decentralized or personalized collaboration, privacy, robustness, and model fusion.</li>
<li><b><a href="https://mo.zju.edu.cn/css">Computational Social Science (Computable Social Analytics)</a></b>: Data-driven and computational approaches to public policy and social systems, including government-attention allocation and evolution, policy evaluation, group interaction and social behavior, and applications such as intelligent transportation, smart cities, and neuro-management. We established <a href="https://mo.zju.edu.cn/css/#/pub">ZJUCCS</a> as a hub for this research.</li>
<li><b>Mo Platform</b>: <a href="https://momodel.ai">Mo</a> is an online platform for AI modelling, experimentation, and education, with public, <a href="http://mo.zju.edu.cn">ZJU</a>, <a href="https://uni.momodel.cn">university</a>, <a href="https://hv.momodel.cn">higher vocational education</a>, <a href="https://edu.momodel.cn">high school</a>, and <a href="https://k12.momodel.cn">K-12</a> versions.</li>
</ul>
<IMG BORDER=20 ALIGN="center" SRC="images/ZJUCSS-transportation.jpeg" height=400>
```

- [ ] **Step 2: Delete the later backup Projects block**

Delete the block beginning with the `<P>` immediately before `<h2> Projects</h2>` and ending with its trailing `<hr>`.

The resulting boundary must be:

```html
<hr>

<!--
<a name="projects"></a>
```

### Task 4: Verify the merged pages

**Files:**
- Verify: `index.html`
- Verify: `index_backup.html`

- [ ] **Step 1: Re-run the Task 1 structural contract**

Expected: `research merge contract verified`.

- [ ] **Step 2: Verify bilingual and backup English content match**

```bash
python3 - <<'PY'
from lxml import html
from pathlib import Path

norm = lambda value: " ".join(value.split())
main = html.fromstring(Path("index.html").read_text())
backup = html.fromstring(Path("index_backup.html").read_text())
main_items = main.xpath('//h2[contains(normalize-space(string(.)), "Research")]/following-sibling::ul[1]/li')
backup_items = backup.xpath('//h2[contains(normalize-space(string(.)), "Research")]/following-sibling::ul[1]/li')
for live, saved in zip(main_items, backup_items):
    spans = live.xpath('.//span[@class="en"]')
    title = norm(spans[0].text_content())
    body = norm(spans[1].text_content())
    backup_title = norm(saved.xpath('./b')[0].text_content())
    assert title == backup_title, (title, backup_title)
    assert norm(saved.text_content()) == f"{backup_title}: {body}"
print("English Research content synchronized")
PY
```

Expected: `English Research content synchronized`.

- [ ] **Step 3: Validate scripts and whitespace**

```bash
node -e 'const fs=require("fs"),vm=require("vm"); for(const f of ["index.html","index_backup.html"]){const s=fs.readFileSync(f,"utf8"); [...s.matchAll(/<script(?:\s[^>]*)?>([\s\S]*?)<\/script>/gi)].map(m=>m[1]).filter(x=>x.trim()).forEach((x,i)=>new vm.Script(x,{filename:`${f}:${i+1}`}));} console.log("inline scripts parsed")'
git diff --check
```

Expected: `inline scripts parsed`; `git diff --check` exits 0.

- [ ] **Step 4: Preserve the existing dirty-worktree boundary**

```bash
git status --short
git diff -- index.html index_backup.html
```

Expected: both HTML files remain modified but unstaged. Do not commit them because they include pre-existing uncommitted publication-list changes.
