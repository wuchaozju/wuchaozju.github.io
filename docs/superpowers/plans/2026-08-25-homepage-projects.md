# Homepage Projects Update Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace the homepage Projects list with four evidence-bounded research/platform summaries while retaining the transportation image.

**Architecture:** Keep the existing static unordered-list presentation. Update the bilingual live page and English backup page in parallel, then remove only the unused duplicate project-grid markup and renderer from the live page.

**Tech Stack:** Static HTML, vanilla JavaScript, Ruby/Python command-line structural checks, Node.js syntax checking.

---

### Task 1: Establish failing content checks

**Files:**
- Test: `index.html`
- Test: `index_backup.html`

- [ ] **Step 1: Run the approved-project contract check before editing**

```bash
ruby -e '
files = %w[index.html index_backup.html]
files.each do |file|
  html = File.read(file)
  projects = html.match(/<h2[^>]*>.*?Projects.*?<\/h2>\s*<ul>(.*?)<\/ul>/m)&.[](1) || abort("#{file}: Projects list missing")
  %w[GAWorld FOS Distributed Computational Mo].each { |term| abort("#{file}: missing #{term}") unless projects.include?(term) }
  abort("#{file}: standalone Intelligent Transportation remains") if projects.match?(/<b[^>]*>.*?Intelligent Transportation.*?<\/b>/m)
  abort("#{file}: transportation image missing") unless html.include?("images/ZJUCSS-transportation.jpeg")
end
abort("index.html: duplicate projects grid remains") if File.read("index.html").include?("projects-grid")
'
```

Expected: FAIL because GAWorld/FOS summaries are absent, Intelligent Transportation remains, and `projects-grid` remains.

### Task 2: Update the bilingual live Projects section

**Files:**
- Modify: `index.html:371-393`
- Modify: `index.html:556-587`

- [ ] **Step 1: Replace the existing project list with the approved four-item bilingual list**

Use four direct `<li>` elements in this exact order: Multi-agent Social Simulation, Distributed Artificial Intelligence, Computational Social Science, Mo Platform. Include:

```html
<li><b><span class="en">Multi-agent Social Simulation</span><span class="zh">多智能体社会仿真</span></b>: <span class="en"><a href="https://github.com/wuchaozju/GAWorld">GAWorld</a> provides a controllable and replayable generative multi-agent environment for urban social-behavior experiments; <a href="https://mo.zju.edu.cn/css/fos/">FOS</a> supports social-system experiment design, branching, observation, comparison, and intervention evaluation.</span><span class="zh"><a href="https://github.com/wuchaozju/GAWorld">GAWorld</a> 提供面向城市社会行为实验的可控制、可回放生成式多智能体环境；<a href="https://mo.zju.edu.cn/css/fos/">FOS</a> 支持社会系统实验设计、分支推演、过程观测、对比分析与干预评估。</span></li>
<li><b><span class="en">Distributed Artificial Intelligence</span><span class="zh">分布式人工智能</span></b>: <span class="en">Research on data pricing and contribution evaluation; federated learning under non-IID data, heterogeneous models, and changing participation; and decentralized or personalized collaboration, privacy, robustness, and model fusion.</span><span class="zh">围绕数据定价与贡献评估，研究非独立同分布数据、模型异构和动态参与条件下的联邦学习，以及去中心化与个性化协同、隐私保护、鲁棒性和模型融合。</span></li>
<li><b><span class="en">Computational Social Science</span><span class="zh">计算社会科学</span></b>: <span class="en">Data-driven and computational approaches to public policy and social systems, including the allocation and evolution of government attention, policy evaluation, group interaction and social behavior, and urban-governance applications such as intelligent transportation.</span><span class="zh">以数据驱动和计算方法研究公共政策与社会系统，包括政府注意力的配置与演化、政策评估、群体互动与社会行为，以及智能交通等城市治理应用。</span></li>
<li><b><span class="en">Mo Platform</span><span class="zh">Mo 平台</span></b>: <span class="en"><a href="https://momodel.ai">Mo</a> is an online platform for AI modelling, experimentation, and education, with public, <a href="http://mo.zju.edu.cn">ZJU</a>, <a href="https://uni.momodel.cn">university</a>, <a href="https://hv.momodel.cn">higher vocational education</a>, <a href="https://edu.momodel.cn">high school</a>, and <a href="https://k12.momodel.cn">K-12</a> versions.</span><span class="zh"><a href="https://momodel.ai">Mo</a> 是一个面向人工智能建模、实验与教育的在线平台，提供公开版、<a href="http://mo.zju.edu.cn">浙大版</a>、<a href="https://uni.momodel.cn">高校版</a>、<a href="https://hv.momodel.cn">高职版</a>、<a href="https://edu.momodel.cn">高中版</a>和<a href="https://k12.momodel.cn">K-12版</a>。</span></li>
```

- [ ] **Step 2: Preserve the transportation image immediately after the list**

Keep this line unchanged:

```html
<IMG BORDER=20 ALIGN="center" SRC="images/ZJUCSS-transportation.jpeg" height=400>
```

- [ ] **Step 3: Remove the second empty Projects heading and `projects-grid` block**

Delete the markup from `<a name="projects"></a>` through the following `<hr>` at the old lines 386-393.

- [ ] **Step 4: Remove the unused `renderProjects` script**

Delete the complete inline `<script>` block containing `var projects`, `renderProjects`, and the `projects-grid` lookup at the old lines 556-587.

### Task 3: Synchronize the English backup Projects section

**Files:**
- Modify: `index_backup.html:332-340`

- [ ] **Step 1: Replace the backup project list with equivalent English content**

Use this exact list and retain the same transportation image line directly below it:

```html
<li><b>Multi-agent Social Simulation</b>: <a href="https://github.com/wuchaozju/GAWorld">GAWorld</a> provides a controllable and replayable generative multi-agent environment for urban social-behavior experiments; <a href="https://mo.zju.edu.cn/css/fos/">FOS</a> supports social-system experiment design, branching, observation, comparison, and intervention evaluation.</li>
<li><b>Distributed Artificial Intelligence</b>: Research on data pricing and contribution evaluation; federated learning under non-IID data, heterogeneous models, and changing participation; and decentralized or personalized collaboration, privacy, robustness, and model fusion.</li>
<li><b>Computational Social Science</b>: Data-driven and computational approaches to public policy and social systems, including the allocation and evolution of government attention, policy evaluation, group interaction and social behavior, and urban-governance applications such as intelligent transportation.</li>
<li><b>Mo Platform</b>: <a href="https://momodel.ai">Mo</a> is an online platform for AI modelling, experimentation, and education, with public, <a href="http://mo.zju.edu.cn">ZJU</a>, <a href="https://uni.momodel.cn">university</a>, <a href="https://hv.momodel.cn">higher vocational education</a>, <a href="https://edu.momodel.cn">high school</a>, and <a href="https://k12.momodel.cn">K-12</a> versions.</li>
```

### Task 4: Verify structure and behavior

**Files:**
- Verify: `index.html`
- Verify: `index_backup.html`

- [ ] **Step 1: Re-run the project contract check**

Run the Task 1 Ruby command.

Expected: PASS with exit status 0.

- [ ] **Step 2: Parse both pages and verify exactly four project items**

```bash
python3 -c 'from lxml import html; from pathlib import Path; [(_ for _ in ()).throw(AssertionError(f"{p}: expected four project items")) if len(html.fromstring(Path(p).read_text()).xpath("//h2[contains(., 'Projects')]/following-sibling::ul[1]/li")) != 4 else None for p in ("index.html", "index_backup.html")]; print("four project items verified")'
```

Expected: `four project items verified`.

- [ ] **Step 3: Check inline JavaScript and whitespace**

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

Expected: both HTML files remain modified but unstaged. Do not commit them because they already contain pre-existing uncommitted publication-list changes; report the combined working-tree result to the user instead.
