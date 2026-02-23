# MON CS DOCS Templates

**Standardized templates for consistent, high-quality documentation.**

---

## Available Templates

### Content Templates

#### 1. **[Article Template](./article-template.md)**
**Purpose**: Comprehensive, in-depth topic coverage

**Use for**:
- Full explanations of CS concepts
- Detailed algorithm analyses
- Complete system overviews
- Research-level topics

**Length**: 2000-5000 words (10-25 min read)

**Sections**: 
- Problem motivation
- Core concept explanation
- Mechanics and logic
- Visual representations
- Mathematical formalization
- Real-world applications
- Examples and exercises
- Related topics and references

---

#### 2. **[Topic Template](./topic-template.md)**
**Purpose**: Focused, short-form concept explanations

**Use for**:
- Quick concept definitions
- Specific algorithm explanations
- Targeted theory discussions
- Reference-style entries

**Length**: 500-1500 words (5-10 min read)

**Sections**:
- Core idea
- How it works
- Visual representation
- Key properties
- When to use
- Related concepts

---

#### 3. **[Category Index Template](./category-index-template.md)**
**Purpose**: Directory-level organization and navigation

**Use for**:
- Category README files
- Learning path guidance
- Topic overviews
- Directory indexes

**Sections**:
- Overview
- Prerequisites
- Learning path
- Topics table with status
- Key concepts
- Related categories

---

### Style & Guidelines

#### 4. **[Style Guide](./style-guide.md)**
**Purpose**: Formatting and writing standards

**Covers**:
- File naming conventions
- Markdown formatting rules
- Writing style and tone
- Mathematical notation
- Code formatting
- Citations and references
- Accessibility standards

---

## How to Use Templates

### Step 1: Choose the Right Template

**Decision Flow**:

```
What are you creating?

├── Full topic explanation?
│   └── Use: article-template.md
│
├── Quick concept definition?
│   └── Use: topic-template.md
│
├── Category overview?
│   └── Use: category-index-template.md
│
└── Not sure?
    └── Ask in community channels
```

### Step 2: Copy the Template

```bash
# Navigate to appropriate directory
cd docs/[pillar]/[category]/

# Copy template
cp ../../../templates/article-template.md ./new-topic.md

# Or for topic template
cp ../../../templates/topic-template.md ./quick-concept.md
```

### Step 3: Fill in the Content

1. **YAML Frontmatter**: Complete all required fields
2. **Replace Placeholders**: Search for `[...]` and replace
3. **Follow Structure**: Use template sections as guide
4. **Apply Style Guide**: Reference style-guide.md
5. **Add Visuals**: Link to moncsdocs-media assets

### Step 4: Quality Check

- [ ] All placeholders replaced
- [ ] Frontmatter complete
- [ ] Headings follow hierarchy
- [ ] Links verified
- [ ] Images load correctly
- [ ] Math renders properly
- [ ] Code examples tested
- [ ] Style guide followed
- [ ] Spell check done
- [ ] Grammar check done

### Step 5: Submit

1. Create pull request
2. Use [PR template](../.github/PULL_REQUEST_TEMPLATE.md)
3. Request review from maintainers
4. Address feedback
5. Merge when approved

---

## Template Philosophy

### Why Templates?

**Consistency**: Readers know what to expect across all topics

**Quality**: Built-in structure ensures comprehensive coverage

**Efficiency**: Contributors don't start from scratch

**Accessibility**: Standard format aids navigation and learning

### Flexibility

Templates are **guidelines, not rigid rules**:

✅ **Do**:
- Adapt sections to fit your topic
- Add sections if truly necessary
- Skip sections that don't apply
- Focus on clarity over conformity

❌ **Don't**:
- Ignore the general structure
- Remove critical sections
- Deviate without good reason
- Sacrifice quality for brevity

---

## Content Quality Standards

### Required Elements

**All content must have**:
- ✅ Clear problem motivation
- ✅ Accurate technical information
- ✅ Concrete examples
- ✅ Visual representations (when appropriate)
- ✅ Real-world applications
- ✅ Related topic links
- ✅ Proper citations

### Excellence Criteria

**High-quality content**:
- ⭐ Explains "why" not just "what"
- ⭐ Progresses logically from simple to complex
- ⭐ Includes multiple examples
- ⭐ Addresses common misconceptions
- ⭐ Provides practice exercises
- ⭐ Cites authoritative sources
- ⭐ Accessible to target audience

---

## Getting Help

### Questions About Templates?

**Before asking**:
1. Read the template comments
2. Check the style guide
3. Review existing high-quality articles
4. Search previous issues/discussions

**Where to ask**:
- [Telegram Chat](https://t.me/moncsdocschat)
- [Discord Server](https://discord.gg/yb6XgkhBXU)
- [GitHub Issues](https://github.com/Moebius-Order/moncsdocs/issues/new/choose)

### Suggest Template Improvements

Templates evolve based on community feedback:

1. Open a [feature request](../.github/ISSUE_TEMPLATE/feature_request.yml)
2. Explain the improvement
3. Show examples of how it helps
4. Maintainers will review and discuss

---

## Version History

**v1.0** (2026-02-23):
- Initial template release
- Article, topic, and category index templates
- Comprehensive style guide

---

<div align="center">

**[⬅️ Back to Main](../README.md)** | **[📚 Read Contributing Guide](../CONTRIBUTING.md)**

Managed by [Moebius Order](https://www.moebiusorder.com) | Licensed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)

</div>