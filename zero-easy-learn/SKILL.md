---
name: zero-easy-learn
description: Generate concise beginner-friendly tutorials from an elementary-school perspective. Use when the user wants to learn any concept, tool, framework, workflow, or technical topic in simple plain language, especially requests like “小学生也能懂”, “大白话教程”, “入门到进阶”, “帮我生成学习教程”, or asks to create/save such a tutorial.
---

# Easy Learn

## Goal

Create tutorials that explain a topic as if teaching a smart elementary-school student: concrete, simple, patient, and useful. Keep the writing concise. Prefer clear examples over long theory.

## First Clarify

Before writing a tutorial, ask clarifying questions unless the user already provided enough detail. Keep this to 1-3 short questions.

Ask about:

- Learning goal: what they want to do after learning it.
- Current level: complete beginner, used it a little, or wants deeper understanding.
- Output form: chat answer or article-style tutorial.
- Length mode: default to `full` if the user does not choose.

Question budget:

- Ask 1 question when the topic and goal are mostly clear.
- Ask 2-3 questions when the topic is broad, ambiguous, or could be taught in very different ways.
- Do not ask more than 3 questions before producing useful progress.
- If the user explicitly asks to start immediately, proceed with reasonable assumptions and state them briefly.

Good clarification format:

```text
我先确认 3 点，这样教程不会写偏：
1. 你学这个主要是为了做什么？
2. 你现在是完全没接触过，还是用过一点？
3. 默认我按 full 完整文章来写，可以吗？
```

If the user says “随便”, “你决定”, or gives no extra detail, choose `full`, assume beginner level, and focus on practical understanding.

## Plan the Teaching Focus

Before writing, analyze the topic and decide what the learner most needs. Do not force the topic into a fixed category.

Think through:

- What problem this topic solves.
- Which 5-8 concepts are truly foundational.
- What must be learned first to avoid confusion.
- What examples make the idea real.
- What beginners usually misunderstand.
- Which advanced parts are useful now, and which should be deferred.

When useful, briefly show the planned focus before generating the tutorial and ask for confirmation.

## Plan Article Images

For `standard` and `full` article-style tutorials, automatically plan useful image insertion points after the article structure is clear. Images should explain the topic, not decorate the page.

Image planning rules:

- Pick only places where a visual would make the concept easier: overview maps, process flows, comparison tables, architecture diagrams, request/response paths, troubleshooting decision trees, or before/after examples.
- Do not force one image per section. Use as many as are genuinely helpful, usually 3-8 for a full technical article and 1-3 for a compact article.
- Avoid vague hero art, stock-like pictures, decorative banners, or repeated concept images.
- For each image slot, define the exact insertion point, teaching purpose, visual content, suggested filename, alt text, and a concise generation prompt seed.
- If the tutorial is only returned in chat, add a short `配图位置建议` table after the article.
- If the tutorial is saved to Markdown and images are not generated yet, insert invisible placeholders at the exact positions:

```markdown
<!-- image-slot: <slug>; purpose: <what this image teaches>; alt: <alt text> -->
```

These placeholders mark where generated images should be inserted later without showing unfinished content to readers.

## Length Modes

Use these modes:

- `quick`: short explanation for fast understanding.
- `standard`: complete but compact tutorial.
- `full`: default mode; article-style tutorial with table of contents, basics, advanced parts, examples, mistakes, cheat sheet, and learning order.

Mode guidance:

- Use `quick` for “一句话讲明白”, “快速解释”, or simple chat answers.
- Use `standard` when the user wants a tutorial but not a long article.
- Use `full` when the user says “完整”, “入门到进阶”, “生成文章”, “保存到项目”, or gives no mode.

If the topic is broad enough that one article would become shallow or too long, suggest splitting it into multiple articles. Give a proposed series list and ask which one to start with. If the user wants everything, create the series plan first, then write article one.

Split when at least one is true:

- The topic contains many independent subtopics.
- A beginner would need multiple learning sessions.
- The tutorial would need more than one major practical workflow.
- The topic mixes concepts, tools, architecture, and real project practice.

## Output Style

- Use plain language first; introduce technical names only after the idea is understandable.
- Use one main life analogy that fits the topic, then reuse it lightly.
- Avoid childish tone. The perspective is simple, not babyish.
- Avoid long motivational openings, repeated explanations, and decorative filler.
- Prefer short paragraphs, lists, tables, and small examples.
- Explain “what it is”, “why it exists”, “how to use it”, and “common mistakes”.
- Include a table of contents for medium or long tutorials.
- Keep the tutorial complete enough to learn from, but trim anything that does not help the learner act.

## Tutorial Structure

Use this default structure unless the user asks otherwise:

1. Title: `大白话讲解——<topic>`
2. One-sentence core idea.
3. Table of contents.
4. Simple analogy.
5. What problem this thing solves.
6. Core concepts with “small child view” explanations.
7. Basic tutorial with concrete steps.
8. Practical example.
9. Advanced tutorial, only the most useful parts.
10. Common mistakes and troubleshooting.
11. Command/API/concept cheat sheet when relevant.
12. Recommended learning order.
13. Final summary table mapping terms to simple meanings.

For short answers, compress this structure instead of forcing every section.

## Series Structure

For a broad topic, create a series plan before writing the article. The plan should keep each article focused enough that a beginner can finish it in one learning session.

Use a series when:

- The topic has multiple independent skill layers, such as basics, real project workflow, deployment, debugging, and advanced design.
- One article would need to explain too many new words before the learner can act.
- The user asks for “入门到进阶”, “完整路线”, “系列”, or wants multiple related articles.
- The article would become shallow if everything were compressed into one page.

Series planning rules:

- Give each article a clear job: one main question it answers or one practical outcome it teaches.
- Mark the current article position, such as `第 1 篇 / 共 5 篇`.
- Add a short “本篇学完你会什么” line near the top of each article.
- At the end, add `上一篇/下一篇建议` when there is a clear learning sequence.
- Avoid repeating the same intro in every article. Later articles should briefly link back to earlier concepts instead of re-explaining them from scratch.
- If saving multiple articles, use consistent filenames and keep their order obvious, for example `01-大白话讲解——<主题>.md`.

Example series format:

```text
这个主题比较大，建议拆成几篇：
1. <topic> 是什么：先建立整体地图
2. 核心概念：把最容易混淆的词讲清楚
3. 第一个实战：做出一个最小可用例子
4. 常见问题：排查和避坑
5. 进阶路线：下一步该学什么
```

Adjust the article list to the actual topic. Do not use this exact list blindly.

If the user asks to write everything immediately, still create the series plan first, then begin with article one unless they explicitly choose another article.

## Depth Rules

- For “基础教程”, cover only must-know ideas and the first usable workflow.
- For “进阶教程”, cover practical next steps, not rare edge cases.
- For technical topics, include runnable commands or code when useful.
- For non-technical topics, include realistic scenarios and decision examples.
- When explaining a risky command or operation, say what it changes and what to check first.

## File Creation Rules

When the user asks to save the tutorial:

- If they specify a project or folder, inspect the project first and choose a fitting location.
- If there is a `content/learn` folder in the project, use it.
- If there is a `zero-easy-learn` folder in the project, use it.
- If the user approves creating one, prefer `content/learn/` for monorepo projects and `zero-easy-learn/` for simple projects.
- Name files using this format: `大白话讲解——<主题>.md`.
- Do not overwrite unrelated existing documents unless the user clearly asks.
- If replacing an earlier draft created in the same task, update that draft directly.

When the user did not ask to save the tutorial, end by asking whether they want it saved locally. If they say yes, ask for the target project or folder unless it is already clear from the conversation.

Save question format:

```text
要不要我把这篇教程保存到本地？如果要，我可以放到项目的 content/learn/ 目录里。
```

If the tutorial is generated in a known project that already has `content/learn/` or `zero-easy-learn/`, offer that exact path.

## Infographic Generation

After creating an article-style tutorial and planning image slots, ask whether the user wants matching infographics generated.

Ask in this format:

```text
我已经整理了配图位置。要不要我用 gpt-image-2 为这些位置生成信息图，并插入到文章里？
```

If the user says yes, or the original request already asks for images:

- Use the `gpt-image-2` skill/script when available.
- Before each generation batch, show the exact prompt(s) that will be sent. If the user is reviewing quality, generate the first image only and wait for approval before continuing.
- Prefer information-rich educational infographics: structured blocks, arrows, timelines, layered diagrams, clear labels, and concrete examples from the article.
- Keep prompts tied to the article's plain-language explanation and examples. Do not generate generic diagrams that could fit any article.
- Avoid requiring lots of tiny text inside the image. Use short labels in the image and keep detailed explanation in the article caption/body.
- Choose sizes that fit the article layout and are accepted by the image tool. Use existing project conventions first; otherwise default to a wide infographic size such as `1536x1024`.
- Save images in the project's existing article image location when one exists, such as `apps/website/public/images/learn/articles/<article-slug>/`. Otherwise create a local image folder beside the article, such as `content/learn/images/` or `zero-easy-learn/images/`.
- Use descriptive lowercase filenames, for example `<topic-slug>-request-flow.png`.
- Replace the matching `image-slot` placeholder with a Markdown image:

```markdown
![<alt text>](<relative-or-site-image-path>)
```

- If image generation fails, keep the placeholders and report which prompts failed, without deleting the article.

## Article QA

Before finalizing any `standard` or `full` tutorial, run a short internal quality review and revise the article if needed. Do not print a long review unless the user asks; use it to improve the draft.

Review for:

- **No filler**: remove repeated encouragement, generic openings, and paragraphs that do not teach a usable idea.
- **No concept jumps**: make sure every technical term is introduced before it is used heavily.
- **Beginner path**: confirm the article moves from “what it is” to “why it exists” to “how to use it” to “common mistakes”.
- **Example quality**: examples should be concrete enough to follow, not only abstract metaphors.
- **Code/command clarity**: if commands or code appear, explain what they change and what the learner should see after running them.
- **Analogy accuracy**: keep the main analogy helpful, but remove it if it starts to distort the technical idea.
- **Visual usefulness**: image slots should teach a concrete relationship, sequence, or comparison. Delete decorative or redundant image slots.
- **Series fit**: if this is part of a series, verify it does not steal too much content from the previous or next article.

For saved articles, silently fix issues before writing the final file. If a major scope issue remains, briefly tell the user and suggest splitting or narrowing the article.

## Quality Checklist

Before finalizing, check:

- The opening explains the topic in one simple idea.
- The analogy helps instead of becoming a long story.
- The tutorial has a clear path from beginner to advanced.
- Important terms are defined in plain language.
- Examples are concrete enough to follow.
- The article is not padded with repeated “不用怕” style filler.
- The tutorial reflects the user's goal and level, not only a generic template.
- Article QA was applied: no concept jumps, no decorative filler, examples are actionable, and commands/code are explained.
- For series articles, the current article position and previous/next learning suggestions are included when useful.
- For article-style tutorials, image insertion points are planned and placed where they teach something concrete.
- If infographics were requested, prompts were shown before generation and generated images were inserted in the planned locations.
- If saved to a file, the final reply links to the file path.
