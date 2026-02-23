# MON CS DOCS Style Guide

**Version**: 1.1  
**Last Updated**: 2026-02-23  
**Maintainer**: Moebius Order

---

## Purpose

This style guide ensures consistency, clarity, and professionalism across all MON CS DOCS documentation. Following these guidelines helps create a cohesive learning experience for students worldwide.

---

## File Naming Conventions

### File Names
- **Format**: `kebab-case` (all lowercase with hyphens)
- **Example**: `binary-search-trees.md`, `tcp-three-way-handshake.md`
- **Avoid**: Spaces, underscores, capital letters, special characters

### Directory Names
- **Format**: `kebab-case` (all lowercase with hyphens)
- **Example**: `data-structures/`, `operating-systems/`
- **Structure**: Organize by knowledge pillar and category

---

## YAML Frontmatter

### Required Fields
```yaml
---
title: "Topic Name"
category: "Category Name"
pillar: "Pillar Name"
difficulty: "Beginner/Intermediate/Advanced"
last_updated: "YYYY-MM-DD"
author: "GitHub Username"
---
```

### Optional Fields
```yaml
tags: ["tag1", "tag2"]
prerequisites: ["Topic 1", "Topic 2"]
estimated_time: "15 minutes"
version: "1.0"
contributors: ["user1", "user2"]
status: "Published"
```

---

## Markdown Formatting

### Headings

**Hierarchy**:
```markdown
# Article Title (H1 - only once at top)

## Main Section (H2)

### Subsection (H3)

#### Sub-subsection (H4)
```

**Rules**:
- Never skip heading levels (don't go from H2 to H4)
- Use sentence case, not title case
- Keep headings concise (< 8 words)
- No punctuation at end of headings

### Emphasis

- **Bold**: `**important terms**` for emphasis or first usage of key terms
- *Italic*: `*slight emphasis*` for de-emphasis or examples
- ***Bold Italic***: `***very important***` sparingly for critical warnings
- `Code`: Inline code for technical terms, commands, variables

### Lists

**Unordered Lists**:
```markdown
- Item 1
- Item 2
  - Sub-item (indent with 2 spaces)
- Item 3
```

**Ordered Lists**:
```markdown
1. First step
2. Second step
3. Third step
```

**Rules**:
- Use parallel structure (all items same grammatical form)
- End with period only if items are complete sentences
- Keep items concise (1-2 lines)

### Links

**Internal Links**:
```markdown
[Related Topic](../category/topic-name.md)
[Back to Index](./README.md)
```

**External Links**:
```markdown
[Article Title](https://example.com)
```

**Rules**:
- Use descriptive link text (not "click here")
- Verify all links work before submitting
- Use relative paths for internal documentation

### Images

**CDN Images**:
```markdown
![Descriptive Alt Text](https://media.moncsdocs.moebiusorder.com/data/category/image-name.svg)

> **Figure 1**: Caption explaining what the diagram shows.
```

**Rules**:
- Always include descriptive alt text
- Always include figure caption
- Reference figures in text ("as shown in Figure 1")
- Use SVG format when possible

### Code Blocks

**With Language Syntax**:
```markdown
```python
def example_function(n):
    return n * 2
```
```

**Pseudocode**:
```markdown
```
function example(input):
    // Pseudocode logic
    return result
```
```

**Rules**:
- Specify language for syntax highlighting
- Include comments explaining non-obvious logic
- Keep examples concise and focused
- Test code before including

### Tables

```markdown
| Column 1 | Column 2 | Column 3 |
|:---------|:--------:|----------:|
| Left     | Center   | Right     |
| Aligned  | Aligned  | Aligned   |
```

**Alignment**:
- `:---` = Left aligned
- `:---:` = Center aligned
- `---:` = Right aligned

### Blockquotes

```markdown
> **Definition**: A formal definition or important note.

> 💡 **Key Insight**: A crucial understanding point.
```

### Horizontal Rules

```markdown
---
```

Use to separate major sections.

---

## Mathematical Notation

### CRITICAL STANDARD: LaTeX Delimiters Only

**MANDATORY**: All mathematical expressions MUST use LaTeX-style delimiters that are compatible with our rendering engine.

### Inline Math

**Format**: Use `\( ... \)` for inline mathematical expressions.

```markdown
The time complexity is \( O(n \log n) \).
For any input size \( n \), the algorithm runs in \( O(n^2) \) time.
```

**Rendered as**: The time complexity is \( O(n \log n) \).

### Block (Display) Math

**Format**: Use `\[ ... \]` for centered, display-style equations.

```markdown
\[
f(n) = \sum_{i=1}^{n} i = \frac{n(n+1)}{2}
\]
```

**Rendered as**: 
\[
f(n) = \sum_{i=1}^{n} i = \frac{n(n+1)}{2}
\]

### Prohibited Syntax

**NEVER USE**:
- ❌ Single dollar signs: `$O(n)$`
- ❌ Double dollar signs: `$$E = mc^2$$`
- ❌ Any variation of `$...$` or `$$...$$`

**Why Dollar Signs Are Prohibited**:
1. Our rendering system does NOT support dollar-sign delimiters
2. Dollar signs will cause mathematical expressions to break on the platform
3. Our CI/CD validation workflow flags dollar-sign usage as errors
4. LaTeX-style `\(` and `\[` delimiters ensure cross-platform compatibility

### Correct vs. Incorrect Examples

| Scenario | ❌ WRONG | ✅ CORRECT |
|:---------|:---------|:-----------|
| Inline complexity | `The algorithm is $O(n)$.` | `The algorithm is \( O(n) \).` |
| Inline equation | `Let $x = 5$.` | `Let \( x = 5 \).` |
| Display equation | `$$f(x) = x^2$$` | `\[ f(x) = x^2 \]` |
| Summation | `$$\sum_{i=1}^{n} i$$` | `\[ \sum_{i=1}^{n} i \]` |
| Multiple inline | `$a$, $b$, $c$` | `\( a \), \( b \), \( c \)` |

### Additional Rules

- **Define variables clearly**: After any equation, explain what each variable represents
- **Explain equations in text**: Don't just show math—describe what it means
- **Use proper LaTeX syntax**: Ensure all braces `{}`, subscripts `_`, and superscripts `^` are correctly formatted
- **Test rendering**: Preview your markdown to ensure math displays correctly
- **Consistency**: Use the same notation throughout the entire article

---

## Writing Style

### Tone
- **Professional**: Academic but accessible
- **Clear**: Simple language over complex jargon
- **Concise**: Eliminate unnecessary words
- **Educational**: Focus on teaching, not showing off

### Voice
- Use active voice: "The algorithm processes" not "The input is processed by"
- Address reader directly: "You can see" not "One can see"
- Present tense for timeless concepts

### Terminology
- Define technical terms on first use
- Be consistent with term usage
- Use industry-standard terminology
- Avoid ambiguous pronouns ("it", "this")

### Examples
- Provide concrete examples
- Use realistic scenarios
- Progress from simple to complex
- Relate to real-world applications

---

## Content Structure

### Article Flow
1. **Problem/Motivation** - Why does this exist?
2. **Core Concept** - What is it?
3. **How It Works** - Mechanics and logic
4. **Visual Representation** - Diagrams
5. **Formalization** - Math/complexity
6. **Applications** - Real-world usage
7. **Examples** - Concrete instances
8. **Related Topics** - Connections

### Section Length
- **Paragraphs**: 3-5 sentences
- **Sections**: 2-4 paragraphs
- **Articles**: 2000-5000 words (10-25 min read)

---

## Accessibility

### Visual
- Use descriptive alt text for images
- Don't rely solely on color to convey meaning
- Ensure sufficient contrast
- Use colorblind-friendly palettes

### Cognitive
- Break complex ideas into smaller chunks
- Use progressive disclosure
- Provide clear navigation
- Summarize key points

### Language
- Define acronyms on first use
- Avoid idioms and colloquialisms
- Consider non-native English speakers
- Use clear, simple sentence structure

---

## Citations and References

### In-Text Citations
```markdown
As demonstrated by Dijkstra [1], the algorithm...

According to Knuth (1997), this approach...
```

### Reference List
```markdown
## References

1. Dijkstra, E. W. (1959). A note on two problems in connexion with graphs. *Numerische Mathematik*, 1(1), 269-271.
2. Knuth, D. E. (1997). *The Art of Computer Programming, Vol. 1*. Addison-Wesley.
```

**Rules**:
- Cite authoritative sources
- Use consistent citation format
- Include DOI or URL when available
- Prefer peer-reviewed academic sources

---

## Language and Grammar

### Spelling
- Use American English spelling
- Be consistent with technical terms

### Punctuation
- Oxford comma: "A, B, and C"
- Periods outside inline code: `variable`.
- Colons introduce lists or explanations

### Numbers
- Spell out one through nine
- Use numerals for 10 and above
- Use numerals for technical values: "5 steps", "3 iterations"

---

## Common Mistakes to Avoid

❌ **Don't**:
- Use vague language ("pretty fast", "very efficient")
- Include opinions without evidence
- Copy content without attribution
- Use first person ("I think", "we believe")
- Make unsubstantiated claims
- Use excessive exclamation points
- **Use dollar signs for math** (`$x$` or `$$x$$`)

✅ **Do**:
- Use precise technical language
- Support claims with evidence or citations
- Properly attribute all sources
- Use third person or second person
- Provide verifiable information
- Maintain professional tone
- **Use LaTeX delimiters for math** (`\( x \)` or `\[ x \]`)

---

## Quality Checklist

Before submitting:

- [ ] Spell check completed
- [ ] Grammar check completed  
- [ ] All links verified
- [ ] All images load correctly
- [ ] Math uses `\( \)` and `\[ \]` only (NO `$` or `$$`)
- [ ] Math renders properly in preview
- [ ] Code examples tested
- [ ] Consistent terminology
- [ ] Proper heading hierarchy
- [ ] Frontmatter complete
- [ ] Citations formatted correctly

---

## Questions?

If you're unsure about any style guidelines:

1. Check existing high-quality articles
2. Ask in [community channels](../README.md#community--support)
3. Open a [question issue](.github/ISSUE_TEMPLATE/question.yml)

---

<div align="center">

**[⬅️ Back to Templates](./README.md)**

Part of [MON CS DOCS](../README.md) | Maintained by [Moebius Order](https://www.moebiusorder.com)

</div>