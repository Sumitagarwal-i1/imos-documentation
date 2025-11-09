# Getting Started with IMOS

Welcome to IMOS! This guide will walk you through your first 10 minutes with your new memory assistant. By the end, you'll have a working knowledge base and understand how to use IMOS effectively.

## Your First 10 Minutes

### Step 1: Verify Installation (30 seconds)

```bash
imos --help
```

You should see the IMOS command menu. If not, check the [installation guide](installation.md).

### Step 2: Add Your First Memory (1 minute)

Let's start with a simple memory:

```bash
imos add "Python is a versatile programming language great for data science"
```

You should see: `IMOS: Added memory #1`

### Step 3: Import Some Files (2 minutes)

If you have existing notes, let's import them:

```bash
# Import a single file
imos addfile path/to/your/notes.txt

# Import an entire folder
imos import-folder ~/Documents/Notes
```

IMOS will process each file and show you the progress.

### Step 4: List Your Memories (30 seconds)

See what's in your knowledge base:

```bash
imos list
```

You'll see a numbered list of all your memories with previews.

### Step 5: Search Your Memories (1 minute)

Try asking IMOS a question:

```bash
imos ask "What do I know about Python?"
```

IMOS will find relevant memories and show you the sources.

### Step 6: Start a Conversation (5 minutes)

Now for the fun part - chat with your memories:

```bash
imos chat
```

You'll see the IMOS logo and enter interactive mode. Try these example conversations:

```
imos> What programming languages do I know?
imos> Tell me about my project ideas
imos> What are my recent TODO items?
imos> exit
```

### Step 7: Check for Actions (30 seconds)

IMOS automatically finds action items in your notes:

```bash
imos actions
```

If IMOS found any TODOs or action items, you'll see them listed.

## Understanding IMOS Workflow

### The Basic Cycle

1. **Import** content (files, manual entries)
2. **Search** or **chat** to find information
3. **Take action** on insights discovered
4. **Add more** content as you work

### Key Concepts

#### Memories
Everything in IMOS is a "memory" - a piece of text with:
- **Content**: The actual text
- **Source**: Where it came from (file path or "manual")
- **Embedding**: AI representation for smart search
- **Links**: Connections to related memories

#### Semantic Search
Unlike traditional search, IMOS understands meaning:
- Search "programming" and find "coding", "development", "software"
- Ask "project ideas" and find relevant concepts even without exact words

#### Memory Linking
IMOS automatically connects similar memories:
- Related concepts get linked together
- Chat mode shows both primary and linked sources
- Helps discover connections you might miss

## Common First Tasks

### For Researchers
```bash
# Import your paper collection
imos import-folder ~/Research/Papers

# Find papers on a topic
imos ask "What papers do I have about machine learning?"

# Start exploring connections
imos chat
imos> How do my ML papers relate to my data science notes?
```

### For Writers
```bash
# Import your writing folder
imos import-folder ~/Writing

# Find character notes
imos ask "Tell me about my main character"

# Explore themes
imos chat
imos> What themes appear across my stories?
```

### For Students
```bash
# Import course materials
imos import-folder ~/School/CourseNotes

# Study for exams
imos ask "What did I learn about calculus?"

# Make connections
imos chat
imos> How does calculus relate to my physics notes?
```

### For Entrepreneurs
```bash
# Import business notes
imos import-folder ~/Business

# Review ideas
imos ask "What business opportunities have I identified?"

# Strategic thinking
imos chat
imos> What trends do I see across my industry research?
```

## Best Practices

### Organizing Your Content

#### File Structure
Keep your files organized before importing:
```
~/Knowledge/
├── Projects/
├── Research/
├── Meeting-Notes/
├── Ideas/
└── Learning/
```

#### Naming Conventions
Use descriptive filenames:
- `2024-11-09-client-meeting.txt` instead of `notes.txt`
- `ml-research-summary.md` instead of `summary.md`

#### Content Quality
- **Be descriptive**: Write complete thoughts, not just keywords
- **Add context**: Include dates, sources, and background
- **Use your own words**: IMOS works better with your natural language

### Effective Searching

#### Ask Good Questions
Instead of keywords, use natural language:
- **Good**: "What did I learn about customer feedback?"
- **Better**: "How can I improve my product based on user input?"

#### Use Chat Mode for Exploration
- Start broad, then get specific
- Ask follow-up questions
- Let IMOS guide you to related content

#### Check Sources
Always review the source files IMOS references to get full context.

### Building Your Knowledge Base

#### Start Small
- Begin with 10-20 important files
- Get comfortable with basic commands
- Gradually import more content

#### Regular Maintenance
- Add new content regularly
- Use `imos rebuild-links` after bulk imports
- Review and complete action items

#### Backup Your Data
Your `memory.db` file contains all your processed memories:
```bash
# Find your database
ls -la memory.db

# Back it up regularly
cp memory.db backup-$(date +%Y%m%d).db
```

## Quick Reference

| Task | Command |
|------|---------|
| Add manual memory | `imos add "your text here"` |
| Import single file | `imos addfile path/to/file.txt` |
| Import folder | `imos import-folder path/to/folder` |
| Search memories | `imos ask "your question"` |
| Start conversation | `imos chat` |
| List all memories | `imos list` |
| View action items | `imos actions` |
| Mark action complete | `imos done 1` |
| Show linked memories | `imos links 1` |
| Rebuild connections | `imos rebuild-links` |

## Common First Questions

**Q: How much content should I import initially?**
A: Start with 10-50 files to get a feel for IMOS. Quality beats quantity.

**Q: Can I edit memories after adding them?**
A: Currently, memories are read-only. Add new, updated content and IMOS will link related information.

**Q: How accurate is the AI search?**
A: Very accurate for conceptual searches. IMOS excels at finding meaning, not just keywords.

**Q: What happens to my data?**
A: Everything stays local except chat queries sent to Groq for AI responses.

## Next Steps

Now that you're familiar with the basics:

1. **[Command Reference](commands.md)** - Learn advanced features
2. **[Use Cases](use-cases.md)** - See detailed workflows
3. **[FAQ](faq.md)** - Get answers to common questions

## Getting Help

- **Quick Help**: `imos command --help`
- **Community**: Join our [community](community.md)
- **Issues**: Report bugs on [GitHub](https://github.com/Sumitagarwal-i/IMOS_terminal/issues)

---

*Ready to unlock the full potential of your knowledge? Let's dive deeper into IMOS!*