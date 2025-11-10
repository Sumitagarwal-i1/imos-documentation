# Complete Command Reference

This guide covers every IMOS command with detailed explanations, examples, and advanced usage patterns.

## Overview

IMOS commands fall into four main categories:
- **[Content Management](#content-management)**: Add and import memories
- **[Search & Chat](#search-chat)**: Find and interact with your knowledge
- **[Organization](#organization)**: Manage memories and connections
- **[Action Tracking](#action-tracking)**: Handle tasks and TODOs

## Content Management

### `imos add`

Add a memory manually from the command line.

**Syntax:**
```bash
imos add "memory text" [--source SOURCE]
```

**Options:**
- `--source`: Specify where this memory comes from (default: "manual")

**Examples:**
```bash
# Basic memory
imos add "React hooks simplify state management in functional components"

# With source attribution  
imos add "Meeting with client about new features" --source "2024-11-09-client-call"

# Multi-line with quotes
imos add "Key insights from today's research:
- Users prefer simple interfaces
- Performance is critical
- Mobile-first design wins"
```

**Pro Tips:**
- Use descriptive, complete sentences
- Include context and dates when relevant
- Break complex ideas into multiple memories for better searchability

---

### `imos addfile`

Import a single file into your knowledge base.

**Syntax:**
```bash
imos addfile PATH_TO_FILE
```

**Supported Formats:**
- `.txt` - Plain text files
- `.pdf` - PDF documents  
- `.docx` - Microsoft Word documents

**Examples:**
```bash
# Import a text file
imos addfile ~/Documents/project-notes.txt

# Import a research paper
imos addfile ~/Research/machine-learning-survey.pdf

# Import meeting notes
imos addfile "~/Meeting Notes/2024-11-09 Client Discussion.docx"
```

**What Happens:**
1. IMOS extracts all text from the file
2. Creates a memory with the file path as source
3. Generates AI embeddings for semantic search
4. Automatically links to related existing memories
5. Scans for action items (TODOs, tasks, etc.)

**Error Handling:**
- Unsupported file types show helpful error messages
- Corrupted files are skipped with warnings
- Permission issues are clearly reported

---

### `imos import-folder`

Recursively import all supported files from a directory.

**Syntax:**
```bash
imos import-folder PATH_TO_DIRECTORY
```

**Examples:**
```bash
# Import entire notes folder
imos import-folder ~/Documents/Notes

# Import research papers
imos import-folder "~/Research Papers"

# Import with absolute path
imos import-folder /Users/username/Knowledge-Base
```

**What Gets Imported:**
- All `.txt`, `.pdf`, and `.docx` files
- Files in subdirectories (recursive search)
- Only files you have read permission for

**Progress Tracking:**
```bash
IMOS: Importing files from '~/Documents/Notes'...
  ✓ Imported: ~/Documents/Notes/ideas.txt
  ✓ Imported: ~/Documents/Notes/research.pdf
  ✗ Error with ~/Documents/Notes/corrupted.docx: File appears corrupted

IMOS: Import complete! 15 files imported, 1 failed
```

**Performance Notes:**
- Large files (>10MB) may take longer to process
- First import downloads AI models (~100MB one-time setup)
- Subsequent imports are much faster due to model caching

---

## Search & Chat

### `imos ask`

Ask a question and get relevant memories with AI-powered responses.

**Syntax:**
```bash
imos ask "YOUR QUESTION" [--top-k K] [--include-links/--no-include-links]
```

**Options:**
- `--top-k`: Number of memories to consider (default: 3)
- `--include-links`: Include automatically linked memories (default: true)

**Examples:**
```bash
# Basic question
imos ask "What do I know about Python?"

# More specific search
imos ask "How can I improve my React performance?"

# Adjust search depth
imos ask "Tell me about my research" --top-k 5

# Exclude linked memories
imos ask "What are my main projects?" --no-include-links
```

**Response Format:**
```bash
IMOS Memory Search
Loading embedding model (one-time setup)...

IMOS> Based on your notes, you know Python is excellent for data science, 
web development with Django/Flask, and automation scripting. Your recent 
projects include a data analysis tool and a web scraper...

Primary sources:
  • ~/Documents/python-learning.txt
  • ~/Projects/data-analysis/README.md

Related memories (auto-linked):
  • ~/Documents/programming-tips.txt
```

**Search Intelligence:**
- **Semantic Understanding**: Finds meaning, not just keywords
- **Context Awareness**: Considers relationships between concepts
- **Source Attribution**: Always shows where information came from
- **Relevance Ranking**: Most relevant memories appear first

---

### `imos chat`

Start an interactive conversation with your knowledge base.

**Syntax:**
```bash
imos chat [--top-k K] [--include-links/--no-include-links]
```

**Examples:**
```bash
# Start basic chat
imos chat

# Adjust memory depth
imos chat --top-k 5
```

**Chat Session Example:**
```bash
 ██╗███╗   ███╗ ██████╗ ███████╗
 ██║████╗ ████║██╔═══██╗██╔════╝
 ██║██╔████╔██║██║   ██║███████╗
 ██║██║╚██╔╝██║██║   ██║╚════██║
 ██║██║ ╚═╝ ██║╚██████╔╝███████║
 ╚═╝╚═╝     ╚═╝ ╚═════╝ ╚══════╝
   IMOS: Solo Pro Memory OS

IMOS Chat Mode Active
Type your question; type 'exit' to leave.

imos> What are my current projects?

You: What are my current projects?

IMOS> Based on your notes, you have three main projects:
1. A customer feedback analysis tool using Python
2. Website redesign focusing on mobile experience  
3. Research into AI-powered productivity tools

Primary sources:
  • ~/Projects/feedback-tool/notes.txt
  • ~/Work/website-project.md

imos> Tell me more about the feedback tool

You: Tell me more about the feedback tool

IMOS> Your feedback analysis tool processes customer reviews using 
sentiment analysis. You've noted it should integrate with existing 
CRM systems and provide real-time dashboards...

imos> exit
```

**Chat Features:**
- **Context Memory**: Remembers conversation within the session
- **Follow-up Questions**: Ask related questions naturally
- **Source Tracking**: Every response includes source citations  
- **Conversation Flow**: See both your questions and IMOS responses
- **Exit Commands**: Use 'exit', 'quit', or 'bye' to leave

**Advanced Chat Techniques:**
```bash
# Exploration workflow
imos> What themes appear in my research?
imos> How do these relate to my current projects?
imos> What gaps do I see in my knowledge?
imos> What should I focus on next?

# Project planning
imos> What resources do I have for the web project?
imos> What challenges did I identify?
imos> What's my timeline looking like?
imos> Who are my key stakeholders?
```

---

## Organization

### `imos list`

Display all memories with IDs and previews.

**Syntax:**
```bash
imos list
```

**Output Format:**
```bash
IMOS: Your Memory Library
============================================================
[  1] Python is excellent for data science, web development...
      Source: manual
[  2] Meeting notes from client discussion about new feat...
      Source: ~/Documents/meeting-notes.txt
[  3] Research findings on user experience design principle...
      Source: ~/Research/ux-research.pdf
```

**Usage:**
- Get overview of your knowledge base
- Find memory IDs for other commands
- Check what's been imported
- Verify memory content

---

### `imos links`

Show memories automatically linked to a specific memory.

**Syntax:**
```bash
imos links MEMORY_ID
```

**Examples:**
```bash
# Show what's linked to memory #5
imos links 5
```

**Output:**
```bash
IMOS: Memories linked to #5
  Linked to #12 (similarity: 0.87)
  Linked to #8 (similarity: 0.85)
  Linked to #23 (similarity: 0.86)
```

**Understanding Links:**
- **Similarity Score**: 0.85+ means strong conceptual relationship
- **Automatic Creation**: Links form when importing related content
- **Bidirectional**: If A links to B, B links to A
- **Context Enhancement**: Linked memories provide additional context in searches

---

### `imos rebuild-links`

Recalculate all memory connections based on similarity.

**Syntax:**
```bash
imos rebuild-links [--threshold THRESHOLD]
```

**Options:**
- `--threshold`: Minimum similarity for linking (default: 0.85)

**Examples:**
```bash
# Standard rebuild
imos rebuild-links

# More sensitive linking
imos rebuild-links --threshold 0.80

# Less sensitive linking  
imos rebuild-links --threshold 0.90
```

**When to Use:**
- After importing large amounts of content
- When you notice missing connections
- To update links with new similarity thresholds
- Periodically for maintenance (monthly)

**Performance:**
- Shows progress bar for large memory collections
- Can take several minutes with 1000+ memories
- Results in better search and chat experiences

---

## Action Tracking

### `imos actions`

List all open action items found in your memories.

**Syntax:**
```bash
imos actions
```

**Output Example:**
```bash
IMOS: Open Action Items
==================================================
[1] Review quarterly performance metrics
    Source: ~/Notes/q4-review.txt | Added: 2024-11-09

[2] Follow up with client about project timeline
    Source: manual | Added: 2024-11-08

[3] Research competitor pricing strategies
    Source: ~/Business/market-analysis.pdf | Added: 2024-11-07
```

**What Gets Detected:**
IMOS automatically finds action items in these formats:
- `TODO: Task description`
- `Action: What needs to be done`
- `Follow up: Next steps`
- `- [ ] Markdown checkbox`
- `* [ ] Bullet checkbox`
- `TASK: Something to complete`

---

### `imos done`

Mark an action item as completed.

**Syntax:**
```bash
imos done ACTION_ID
```

**Examples:**
```bash
# Mark action #1 as complete
imos done 1

# Response
IMOS: Action 1 marked as done!
```

**What Happens:**
- Action status changes from "open" to "done"
- Removed from future `imos actions` lists
- Preserved in database for historical tracking
- No changes made to source files

---

## Advanced Usage Patterns

### Workflow Integration

**Daily Review Workflow:**
```bash
# Check new action items
imos actions

# Review recent memories
imos list | tail -10

# Explore connections
imos chat
imos> What did I learn today?
imos> What should I prioritize tomorrow?
imos> exit
```

**Research Workflow:**
```bash
# Import new research
imos import-folder ~/Downloads/NewPapers

# Rebuild connections
imos rebuild-links

# Explore insights
imos ask "What patterns do I see in recent research?"

# Deep dive
imos chat
imos> How does this new research relate to my thesis?
imos> What questions does this raise?
imos> What should I investigate next?
```

**Project Planning Workflow:**
```bash
# Gather project information
imos ask "What do I know about Project X?"

# Identify action items
imos actions

# Strategic discussion
imos chat
imos> What resources do I need for Project X?
imos> What are the biggest risks?
imos> Who should I involve?
```

### Power User Tips

**Batch Operations:**
```bash
# Import multiple folders
for folder in ~/Docs ~/Research ~/Projects; do
  imos import-folder "$folder"
done

# Multiple questions
imos ask "Current projects" > projects.txt
imos ask "Open research questions" > research.txt
imos ask "Key contacts" > contacts.txt
```

**Integration with Other Tools:**
```bash
# Export memory list
imos list > my-knowledge-overview.txt

# Pipe search results
imos ask "Python tips" | grep -i "performance"

# Combine with file operations
find ~/NewNotes -name "*.txt" -exec imos addfile {} \;
```

## Error Handling & Troubleshooting

### Common Error Messages

**"IMOS Setup Required!"**
- Cause: Missing GROQ_API_KEY
- Solution: Set your API key ([installation guide](installation.md))

**"No memories found"**
- Cause: Empty knowledge base
- Solution: Use `imos add` or `imos import-folder` to add content

**"File not found"**
- Cause: Invalid file path
- Solution: Check path exists and you have read permissions

**"Unsupported file type"**
- Cause: File format not supported
- Solution: Convert to .txt, .pdf, or .docx

### Performance Optimization

**Speed Up Searches:**
- Reduce `--top-k` value for faster results
- Use `--no-include-links` for simpler searches
- Keep memory database size reasonable (<10,000 memories)

**Manage Memory Usage:**
- Restart IMOS periodically to refresh model cache
- Consider splitting very large knowledge bases
- Monitor disk space (models + database + caches)

---

**Need more help?** Check the [FAQ](faq.md) or visit our [community](community.md) for support!