# Homepage Projects Update Design

## Goal

Replace the homepage's current project list with four current research and platform themes while preserving the page's compact academic style, bilingual presentation, and existing transportation image.

## Confirmed scope

The Projects section will contain these items, in this order:

1. Multi-agent social simulation
2. Distributed artificial intelligence
3. Computational social science
4. Mo platform

The standalone Intelligent Transportation project entry will be removed. The transportation image immediately below the list will remain and transportation will be mentioned as an application within computational social science.

## Content design

### Multi-agent social simulation

Link to [GAWorld](https://github.com/wuchaozju/GAWorld) and [FOS](https://mo.zju.edu.cn/css/fos/). Describe GAWorld as a controllable and replayable generative multi-agent environment for urban social-behavior experiments. Describe FOS as a social-system simulation platform for experimental design, branching, observation, comparison, and intervention evaluation. Do not collapse the two platforms into one product.

### Distributed artificial intelligence

Summarize the publication record at the research-program level: data pricing and contribution evaluation; federated learning under non-IID data, model heterogeneity, and changing participation; decentralized and personalized collaboration; privacy, robustness, and model fusion. Avoid claiming that every listed topic belongs to one system or paper.

### Computational social science

Describe data-driven and computational research on public policy and social systems, including the allocation and evolution of government attention, policy evaluation, group interaction, social behavior, and urban governance. Mention intelligent transportation as one application area so the retained image remains contextually connected to this item.

### Mo platform

Retain the existing links and describe Mo as an online platform for AI modelling, experimentation, and education, including its Zhejiang University and education-oriented versions. Correct the existing English typo `eduction` to `education`.

## Page structure

- Keep the current unordered-list presentation; do not introduce cards or new visual styling.
- `index.html` will provide equivalent English and Chinese text through the existing `.en` and `.zh` spans.
- `index_backup.html` will carry the same four items in English, matching its existing non-bilingual structure.
- Remove the second empty Projects heading and empty `projects-grid` from `index.html`.
- Remove the unused JavaScript renderer for that empty grid so no dead project-rendering code remains.
- Preserve `images/ZJUCSS-transportation.jpeg` and its current placement below the project list.

## Evidence boundaries

- GAWorld capabilities will be summarized from its repository documentation.
- FOS capabilities will be summarized from its public product page at `https://mo.zju.edu.cn/css/fos/`.
- Distributed-AI and computational-social-science text will synthesize themes represented in the publication list and the user's requested research framing. It will remain a thematic summary rather than attributing unsupported results to individual papers.

## Verification

After implementation:

- both pages must contain the same four project themes in the confirmed order;
- GAWorld, FOS, and Mo links must resolve to their intended public URLs;
- no standalone Intelligent Transportation list item may remain;
- the transportation image must remain present;
- `index.html` must have only one visible Projects section;
- HTML parsing, inline JavaScript syntax checks, and `git diff --check` must pass.

