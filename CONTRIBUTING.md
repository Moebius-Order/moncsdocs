# Contributing to MON CS DOCS

Thank you for your interest in contributing to **MON CS DOCS**! We're building the world's most comprehensive open Computer Science documentation, and your expertise helps make quality CS education accessible to everyone.

---

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
- [Getting Started](#getting-started)
- [Content Guidelines](#content-guidelines)
- [Using Templates](#using-templates)
- [Submission Process](#submission-process)
- [Review Process](#review-process)
- [Style Guide](#style-guide)
- [Media Contributions](#media-contributions)
- [Licensing](#licensing)
- [Community](#community)
- [Questions?](#questions)

---

## Code of Conduct

This project adheres to the [Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code. Please report unacceptable behavior to [moncsdocs@moebiusorder.com](mailto:moncsdocs@moebiusorder.com).

---

## How Can I Contribute?

There are many ways to contribute to MON CS DOCS:

### 📝 Content Contributions

- **Write New Articles**: Create documentation for topics not yet covered
- **Improve Existing Content**: Enhance clarity, add examples, fix errors
- **Add Practical Examples**: Provide code examples, use cases, or worked problems
- **Update Outdated Information**: Keep content current with latest research and practices
- **Expand Coverage**: Add more depth to existing topics

### 🎨 Visual Contributions

- **Create Diagrams**: Design educational diagrams, flowcharts, and visualizations
- **Improve Existing Visuals**: Enhance clarity or accessibility of diagrams
- **Contribute to Media Repository**: Add assets to [moncsdocs-media](https://github.com/Moebius-Order/moncsdocs-media)

### 🐛 Quality Improvements

- **Report Issues**: Flag errors, typos, or unclear explanations
- **Fix Bugs**: Correct technical inaccuracies or formatting issues
- **Improve Navigation**: Suggest better organization or cross-references

### 🌍 Community Support

- **Answer Questions**: Help others in community channels
- **Review Pull Requests**: Provide feedback on contributions
- **Spread the Word**: Share MON CS DOCS with students and educators

### 💡 Ideas & Feedback

- **Suggest Topics**: Identify gaps in coverage
- **Propose Improvements**: Share ideas for better documentation
- **User Experience**: Suggest navigation or structural improvements

---

## Getting Started

### Prerequisites

Before contributing, ensure you have:

- A [GitHub account](https://github.com/signup)
- Basic knowledge of Git and Markdown
- Understanding of the Computer Science topic you're contributing to
- Familiarity with our [templates](templates/) and [style guide](templates/style-guide.md)

### Setting Up Your Environment

1. **Fork the Repository**
   ```bash
   # Click the "Fork" button on GitHub, then clone your fork
   git clone https://github.com/YOUR-USERNAME/moncsdocs.git
   cd moncsdocs
   ```

2. **Create a Branch**
   ```bash
   # Use a descriptive branch name
   git checkout -b add/topic-name
   # or
   git checkout -b fix/issue-description
   # or
   git checkout -b improve/existing-topic
   ```

3. **Keep Your Fork Updated**
   ```bash
   # Add upstream remote
   git remote add upstream https://github.com/Moebius-Order/moncsdocs.git
   
   # Fetch and merge updates
   git fetch upstream
   git merge upstream/main
   ```

---

## Content Guidelines

### Quality Standards

All contributions must meet these standards:

#### Accuracy
- ✅ Technically correct and factually accurate
- ✅ Based on authoritative sources (textbooks, papers, standards)
- ✅ Citations provided for non-original content
- ✅ Mathematical notation is precise and conventional

#### Clarity
- ✅ Written for the target audience (students, engineers, researchers)
- ✅ Complex concepts broken down into understandable parts
- ✅ Jargon explained when first introduced
- ✅ Examples provided to illustrate abstract concepts

#### Completeness
- ✅ Covers fundamentals through practical applications
- ✅ Includes worked examples where appropriate
- ✅ Addresses common misconceptions
- ✅ Links to related topics for deeper understanding

#### Structure
- ✅ Follows our templates (see [templates/](templates/))
- ✅ Consistent formatting and organization
- ✅ Proper heading hierarchy (H1 → H2 → H3)
- ✅ Clear navigation and cross-references

### Target Audience

Write for:
- **Students**: High school through university level
- **Self-learners**: Motivated individuals learning independently
- **Engineers**: Professionals seeking theoretical foundations
- **Educators**: Those teaching or creating curricula

### Tone & Style

- **Educational but approachable**: Not condescending or overly academic
- **Clear and direct**: Avoid unnecessary complexity
- **Engaging**: Use examples, analogies, and real-world applications
- **Objective**: Present facts and established theory

---

## Using Templates

We provide templates to ensure consistency across all documentation:

### Available Templates

| Template | Purpose | When to Use |
|:---------|:--------|:------------|
| [category-index-template.md](templates/category-index-template.md) | Category overview and topic index | Creating a new category folder |
| [article-template.md](templates/article-template.md) | Full CS theory article | Writing comprehensive topic documentation |
| [topic-template.md](templates/topic-template.md) | Quick topic reference | Creating shorter, focused explanations |

### How to Use Templates

1. **Copy the appropriate template** from `templates/` directory
2. **Rename the file** with your topic name (use lowercase and hyphens)
   - Example: `binary-search-tree.md`
3. **Fill in the YAML frontmatter** (metadata at the top)
4. **Replace placeholder text** with your content
5. **Follow the structure** provided by the template
6. **Remove sections** that aren't applicable (mark as "N/A" if required)

### Template Guidelines

- **Don't skip sections**: Each section serves a pedagogical purpose
- **Maintain formatting**: Use the same heading levels and structure
- **Update metadata**: Ensure YAML frontmatter is accurate and complete
- **Cross-reference**: Link to related topics within the documentation

---

## Submission Process

### Step-by-Step Workflow

#### 1. Prepare Your Contribution

- ✅ Content follows our [templates](templates/)
- ✅ Writing adheres to [style guide](templates/style-guide.md)
- ✅ All code examples are tested and functional
- ✅ Mathematical notation renders correctly (see below)
- ✅ Links to other pages work correctly
- ✅ Images are hosted on [moncsdocs-media CDN](https://github.com/Moebius-Order/moncsdocs-media)

#### 2. Commit Your Changes

```bash
# Stage your files
git add docs/category/your-topic.md

# Write a descriptive commit message
git commit -m "Add: [Topic Name] - Brief description"

# Examples of good commit messages:
# "Add: Binary Search Trees with complexity analysis"
# "Fix: Correct Big-O notation in Merge Sort article"
# "Improve: Add practical examples to Dijkstra's Algorithm"
# "Update: Refresh outdated information in Cache Coherence"
```

**Commit Message Format**:

```
[Type]: [Subject] - [Optional: Brief description]

Types:
- Add: New content
- Fix: Error corrections
- Improve: Enhancements to existing content
- Update: Information refresh
- Refactor: Reorganization without content changes
- Docs: Documentation-only changes
```

#### 3. Push to Your Fork

```bash
git push origin your-branch-name
```

#### 4. Create a Pull Request

1. Go to your fork on GitHub
2. Click **"Compare & pull request"**
3. Fill out the PR template (see below)
4. Submit the pull request

### Pull Request Template

```markdown
## Description
Brief description of what this PR adds or changes.

## Type of Contribution
- [ ] New article
- [ ] Content improvement
- [ ] Error correction
- [ ] Visual/diagram addition
- [ ] Documentation update

## Topic Details
- **Category**: [e.g., Data Structures, Algorithms, Operating Systems]
- **Pillar**: [Foundational Theory, Hardware & Architecture, Software Paradigms, Systems & Networking]
- **Difficulty**: [Beginner/Intermediate/Advanced]

## Checklist
- [ ] Followed appropriate template
- [ ] Content is technically accurate
- [ ] Writing follows style guide
- [ ] All links are functional
- [ ] Mathematical notation uses supported formats (see style guide)
- [ ] Examples are tested and correct
- [ ] Citations provided for non-original content
- [ ] Commit messages are descriptive

## Related Issues
Closes #[issue number] (if applicable)

## Additional Notes
Any additional context or information for reviewers.

## License Confirmation
I confirm that:
- [ ] I am the original author of this content OR have permission to contribute it
- [ ] I agree to license this contribution under CC BY-SA 4.0
- [ ] This content does not infringe on any third-party intellectual property
```

---

## Review Process

### What Happens After Submission?

1. **Initial Review** (1-3 days)
   - Maintainers check if PR follows guidelines
   - Basic technical accuracy verification
   - Style and formatting review

2. **Technical Review** (3-7 days)
   - Subject matter experts review content accuracy
   - Mathematical/logical correctness verification
   - Pedagogical effectiveness assessment

3. **Feedback & Iteration**
   - Reviewers provide comments and suggestions
   - Author makes requested changes
   - Discussion and refinement

4. **Approval & Merge**
   - Once approved, content is merged
   - Contributor credited in article metadata
   - Content goes live on the platform

### Review Criteria

Reviewers evaluate:

✅ **Technical Accuracy**: Is the content correct?
✅ **Clarity**: Is it understandable to the target audience?
✅ **Completeness**: Does it cover the topic adequately?
✅ **Structure**: Does it follow our templates?
✅ **Style**: Does it match our writing standards?
✅ **Citations**: Are sources properly credited?
✅ **Links**: Do all cross-references work?

### Response Time

- **Simple fixes**: 1-3 days
- **New articles**: 5-10 days
- **Major contributions**: 10-14 days

Larger contributions may take longer due to thorough review requirements.

---

## Style Guide

For detailed style guidelines, see [templates/style-guide.md](templates/style-guide.md).

### Quick Reference

#### Markdown Formatting

- **Headings**: Use `##` for main sections, `###` for subsections
- **Bold**: Use for emphasis and key terms: `**important**`
- **Italics**: Use for definitions: `*definition*`
- **Code**: Use backticks for inline code: `` `variable` ``
- **Code Blocks**: Use triple backticks with language specification

#### Mathematical Notation

**Supported Formats**: We support multiple LaTeX-style delimiters for mathematical expressions.

**Inline Math** (within sentences):
- ✅ Option 1: `\( O(n \log n) \)` → Renders as \( O(n \log n) \)
- ✅ Option 2: `$O(n \log n)$` → Renders as $O(n \log n)$

**Block (Display) Math** (centered equations):
- ✅ Option 1:
  ```
  \[
  f(n) = \sum_{i=1}^{n} i
  \]
  ```
- ✅ Option 2:
  ```
  $$
  f(n) = \sum_{i=1}^{n} i
  $$
  ```

**Best Practices**:
- Use consistent notation throughout a single article
- Either style is acceptable, but don't mix both in the same document
- Test rendering in preview before submitting
- Ensure all braces, subscripts, and superscripts are properly formatted

**Examples**:
```markdown
The time complexity is \( O(n^2) \) in the worst case.
The time complexity is $O(n^2)$ in the worst case.

The summation formula:
$$
S = \sum_{i=1}^{n} i = \frac{n(n+1)}{2}
$$
```

#### Lists

- Use `-` for unordered lists
- Use `1.` for ordered lists
- Indent sublists with 2 spaces

#### Links

- **Internal**: `[Topic Name](../category/topic-file.md)`
- **External**: `[Text](https://example.com)`
- **Media**: `![Alt Text](https://media.moncsdocs.moebiusorder.com/data/...)`

#### File Naming

- Use lowercase
- Use hyphens for spaces: `binary-search-tree.md`
- Be descriptive: `hash-table-collision-resolution.md`
- Avoid abbreviations unless standard: `tcp-ip-protocol.md` ✅, `ht-cr.md` ❌

---

## Media Contributions

Visual assets (diagrams, illustrations, SVGs) are maintained in a separate repository.

### Contributing Diagrams

1. **Visit**: [moncsdocs-media repository](https://github.com/Moebius-Order/moncsdocs-media)
2. **Read**: Media contribution guidelines
3. **Follow**: Asset naming and format standards
4. **Submit**: Pull request to media repository
5. **Reference**: Use CDN URLs in documentation

### Image Guidelines

- **Format**: SVG preferred (infinitely scalable)
- **Fallback**: PNG for complex illustrations
- **Avoid**: JPEG, GIF, BMP
- **Accessibility**: Ensure colorblind-friendly palettes
- **Naming**: Descriptive, lowercase, hyphenated

### CDN Usage

Reference media assets using CDN URLs:

```markdown
![Diagram Description](https://media.moncsdocs.moebiusorder.com/data/category/diagram-name.svg)
```

**Never**:
- ❌ Upload images directly to this repository
- ❌ Use external image hosting services
- ❌ Include base64-encoded images

---

## Licensing

### Your Rights

By contributing to MON CS DOCS, you:

- **Retain copyright** to your original work
- **Grant permission** for MON CS DOCS to distribute your content
- **Agree to license** your contribution under CC BY-SA 4.0

### CC BY-SA 4.0 License

All content is licensed under [Creative Commons Attribution-ShareAlike 4.0 International](https://creativecommons.org/licenses/by-sa/4.0/).

**This means**:
- ✅ Anyone can use, share, and adapt your contribution
- ✅ You will be credited as the author
- ✅ Derivatives must use the same license
- ✅ Commercial use is permitted with attribution

### What You Must Confirm

When contributing, you represent that:

1. You are the **original author** OR have **permission** to contribute
2. Your contribution **does not infringe** on third-party intellectual property
3. You have the **legal authority** to license under CC BY-SA 4.0
4. You **agree to indemnify** Moebius Order against claims arising from your contribution

See [LICENSE](LICENSE) for complete terms.

---

## Community

Join our community to discuss contributions, ask questions, and collaborate:

### Communication Channels

- **Telegram Channel**: [t.me/moncsdocs](https://t.me/moncsdocs) — Announcements
- **Telegram Chat**: [t.me/moncsdocschat](https://t.me/moncsdocschat) — Discussions
- **Discord**: [discord.gg/yb6XgkhBXU](https://discord.gg/yb6XgkhBXU) — Real-time collaboration
- **Reddit**: [r/moncsdocs](https://www.reddit.com/r/moncsdocs) — Long-form discussions
- **GitHub Discussions**: [moncsdocs/discussions](https://github.com/Moebius-Order/moncsdocs/discussions)

### Getting Help

**Questions about contributions?**
- Post in [GitHub Discussions](https://github.com/Moebius-Order/moncsdocs/discussions)
- Ask in our [Telegram Chat](https://t.me/moncsdocschat)
- Join our [Discord server](https://discord.gg/yb6XgkhBXU)

**Found a bug or issue?**
- Check [existing issues](https://github.com/Moebius-Order/moncsdocs/issues)
- Open a [new issue](https://github.com/Moebius-Order/moncsdocs/issues/new) if not already reported

---

## Questions?

Still have questions? We're here to help!

### Contact

- **Email**: [moncsdocs@moebiusorder.com](mailto:moncsdocs@moebiusorder.com)
- **Community**: [Telegram](https://t.me/moncsdocs) | [Discord](https://discord.gg/yb6XgkhBXU)
- **Issues**: [GitHub Issues](https://github.com/Moebius-Order/moncsdocs/issues)

### Useful Links

- **Main Repository**: [github.com/Moebius-Order/moncsdocs](https://github.com/Moebius-Order/moncsdocs)
- **Media Repository**: [github.com/Moebius-Order/moncsdocs-media](https://github.com/Moebius-Order/moncsdocs-media)
- **Website**: [mcdocs.moebiusorder.com](https://mcdocs.moebiusorder.com)
- **Organization**: [Moebius Order](https://www.moebiusorder.com)

---

<div align="center">

## Thank You for Contributing! 🎉

Your contributions make Computer Science education accessible to everyone.

Together, we're building the most comprehensive open CS documentation.

**[⬅️ Back to README](README.md)** | **[📚 View Templates](templates/)** | **[🌐 Visit Website](https://mcdocs.moebiusorder.com)**

---

Managed by [Moebius Order](https://www.moebiusorder.com) | Licensed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)

</div>