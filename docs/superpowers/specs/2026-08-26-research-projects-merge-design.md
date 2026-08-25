# Research and Projects Merge Design

## Goal

Consolidate the homepage's Research and Projects content into one four-item `Research / 研究方向` section near the top of the page, with the transportation image immediately after it.

## Confirmed structure

The existing top Research section remains in its current position and keeps the `research` anchor. Its list is replaced by these four items, in order:

1. Multi-agent social simulation
2. Distributed artificial intelligence
3. Computational social science / Computable Social Analytics
4. Mo platform

The separate Projects section after Teaching is removed completely. No visible Projects heading or second copy of the four-item list remains.

## Content design

### Multi-agent social simulation

Retain the approved bilingual GAWorld and FOS summary and links. GAWorld remains described as the controllable, replayable generative multi-agent environment; FOS remains described as the social-system experiment platform for branching, observation, comparison, and intervention.

### Distributed artificial intelligence

Retain the approved publication-derived bilingual summary covering data pricing, contribution evaluation, heterogeneous federated learning, decentralized or personalized collaboration, privacy, robustness, and model fusion.

### Computational social science / Computable Social Analytics

Use a linked bilingual title:

- English: `Computational Social Science (Computable Social Analytics)`
- Chinese: `计算社会科学（可计算社会分析）`
- URL: `https://mo.zju.edu.cn/css`

Merge both bodies of content rather than adding a fifth item. The English and Chinese summaries will include:

- government-attention allocation and evolution;
- policy evaluation, group interaction, and social behavior;
- data-driven social-science applications including intelligent transportation, smart cities, and neuro-management;
- [ZJUCCS](https://mo.zju.edu.cn/css/#/pub) as the research hub.

Correct the supplied legacy typo `smart cites` to `smart cities`.

### Mo platform

Retain the approved bilingual description and links for AI modelling, experimentation, education, and the existing platform variants.

## Transportation image placement

Move the existing `images/ZJUCSS-transportation.jpeg` element from the lower Projects section to immediately after the consolidated Research list. The image remains unchanged at height 400. Recent publications follow the image.

## Backup page

Apply the same structure and English content to `index_backup.html`: a four-item Research list, merged Computable Social Analytics content, the transportation image immediately below it, and no later Projects section.

## Change boundaries

- Do not alter publication entries, teaching content, navigation, language switching, or unrelated layout.
- Do not introduce cards, new CSS, or new JavaScript.
- Preserve the existing uncommitted publication-list work in both HTML files.

## Verification

After implementation, both pages must satisfy all of the following:

- exactly one visible Research heading;
- no visible Projects heading;
- exactly four direct Research list items in the confirmed order;
- Computational Social Science contains the Computable Social Analytics and ZJUCCS links;
- exactly one transportation image, positioned after the Research list and before Recent publications;
- no project list remains after Teaching;
- HTML parsing, inline JavaScript syntax checks, and `git diff --check` pass.

