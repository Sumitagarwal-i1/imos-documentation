# Frequently Asked Questions

## Installation & Setup

### Q: What versions of Python does IMOS support?
**A:** IMOS requires Python 3.8 or higher. It's tested on Python 3.8, 3.9, 3.10, 3.11, and 3.12. We recommend using the latest stable Python version for best performance.

### Q: Do I need to install anything besides IMOS?
**A:** No! `pip install imos` handles all dependencies automatically. The first time you use AI features, IMOS will download the required models (~100MB), but this happens automatically.

### Q: The installation seems slow. Is this normal?
**A:** Yes, especially on first install. IMOS installs several AI libraries including PyTorch and sentence-transformers. The initial model download also takes time. Subsequent use is much faster.

### Q: Can I use IMOS without the API key?
**A:** Partially. You can add memories, search, and list content without an API key. However, the `ask` and `chat` commands require a Groq API key for AI-powered responses. The API key is free at [console.groq.com](https://console.groq.com).

### Q: Is my API key safe?
**A:** Yes. Your API key is stored locally in environment variables or .env files. IMOS only sends chat queries to Groq - never your API key itself. All your memories stay on your device.

---

## Using IMOS

### Q: What file formats can IMOS import?
**A:** Currently:
- **Text files** (.txt): Full support
- **PDF files** (.pdf): Text extraction via PyMuPDF
- **Word documents** (.docx): Content extraction via python-docx

Coming soon: Markdown (.md), PowerPoint (.pptx), and web page imports.

### Q: How accurate is IMOS search compared to traditional search?
**A:** IMOS uses semantic search, which understands meaning rather than just matching keywords. For example:
- Search "programming" → finds "coding", "development", "software engineering"
- Search "customer issues" → finds "user complaints", "client feedback", "support tickets"

This typically provides much more relevant results than keyword search, especially for conceptual queries.

### Q: Can I edit or delete memories after importing them?
**A:** Currently, memories are read-only to maintain data integrity and source attribution. If you need to update information:
1. Add a new, updated memory with `imos add`
2. IMOS will automatically link related content
3. The chat system will consider both old and new information

Delete functionality is planned for a future release.

### Q: How much storage space does IMOS use?
**A:** Storage depends on your content:
- **AI models**: ~500MB (downloaded once)
- **Database**: ~1KB per memory on average
- **Cache files**: ~50MB typical

For reference: 1,000 text files ≈ 1GB total; 10,000 memories ≈ 600MB total.

### Q: Can I use IMOS with multiple knowledge bases?
**A:** Currently, IMOS uses a single database per directory. You can work around this by:
1. Using different directories for different projects
2. Running IMOS from different working directories
3. Using source tags to organize content

Multi-database support is planned for v0.2.0.

---

## Performance & Limits

### Q: How many memories can IMOS handle?
**A:** IMOS has been tested with:
- **10,000+ memories**: Good performance
- **50,000+ memories**: Slower but functional
- **100,000+ memories**: May need optimization

Performance depends on your hardware. For very large collections, consider organizing into separate knowledge bases by topic.

### Q: Why is the first search slow but later ones fast?
**A:** IMOS loads the AI model into memory on first use (called "lazy loading"). This takes 5-10 seconds initially but then stays loaded, making subsequent searches nearly instantaneous.

### Q: Can I run IMOS on older computers?
**A:** Minimum requirements:
- **RAM**: 2GB available (4GB recommended)
- **CPU**: Any 64-bit processor from 2010+
- **Storage**: 1GB free space

IMOS will work on older hardware but may be slower during model loading and large imports.

### Q: Does IMOS work offline?
**A:** Mostly yes:
- **Full offline**: `add`, `list`, `import-folder`, `links`, `actions`, `done`
- **Requires internet**: `ask`, `chat` (these use Groq's API)

All your memories and search capabilities work offline. Only AI-powered responses need internet.

---

## Privacy & Security

### Q: What data does IMOS send to external services?
**A:** Only the specific questions you ask in `chat` and `ask` commands are sent to Groq for AI responses. Your memories, files, and API key stay local. IMOS never sends:
- Your file contents
- Your memory database
- Your API key
- Any analytics or usage data

### Q: Can I use IMOS in a corporate environment?
**A:** Yes, but check your company policies:
- **Data stays local**: Your files never leave your computer
- **AI queries**: Chat questions are sent to Groq (consider content sensitivity)
- **No telemetry**: IMOS doesn't collect usage data

Many companies allow tools like IMOS. When in doubt, consult your IT security team.

### Q: What happens if I lose my computer?
**A:** Your IMOS data is stored locally:
- **Memory database**: `memory.db` file in your working directory
- **Models**: Downloaded to your Python environment

**Backup recommendations**:
```bash
# Backup your database
cp memory.db ~/Backups/imos-backup-$(date +%Y%m%d).db

# Backup your source files too
tar -czf ~/Backups/knowledge-base-$(date +%Y%m%d).tar.gz ~/Documents/Notes
```

### Q: Is IMOS open source?
**A:** Yes! IMOS is MIT licensed. You can:
- View source code on [GitHub](https://github.com/Sumitagarwal-i/IMOS_terminal)
- Modify it for your needs
- Contribute improvements
- Audit security and privacy practices

---

## Troubleshooting

### Q: IMOS says "command not found" after installation
**A:** Try these solutions in order:
1. Restart your terminal
2. Check installation: `pip show imos`
3. Try: `python -m imos --help`
4. Reinstall: `pip install --user imos`
5. Check PATH includes pip's script directory

### Q: "No module named 'sentence_transformers'" error
**A:** This indicates incomplete installation. Try:
```bash
pip uninstall imos
pip install imos
```

If that fails:
```bash
pip install sentence-transformers torch transformers
pip install imos
```

### Q: IMOS is very slow on my computer
**A:** Performance optimization steps:
1. **First run**: Wait for model download to complete
2. **RAM**: Close other applications, ensure 2GB+ available
3. **Search**: Use lower `--top-k` values (e.g., `--top-k 3`)
4. **Database**: Run `imos rebuild-links` if you have many memories

### Q: "API rate limit" errors in chat mode
**A:** Groq's free tier has rate limits. Solutions:
1. **Wait**: Limits reset quickly (usually 1 minute)
2. **Slower pace**: Don't rapid-fire questions
3. **Upgrade**: Consider Groq's paid tiers for heavy use

### Q: File import failed with "Permission denied"
**A:** Check file permissions:
```bash
# On macOS/Linux
ls -la /path/to/file

# Make readable if needed
chmod 644 /path/to/file
```

On Windows, ensure you have read access to the file.

### Q: PDF import shows garbled text
**A:** Some PDFs don't extract cleanly:
1. **Scanned PDFs**: Convert to text-based PDFs first
2. **Complex layouts**: Try exporting PDF to Word, then import .docx
3. **Encrypted PDFs**: Remove password protection first

### Q: Chat responses don't match my content
**A:** Potential causes:
1. **Limited memories**: Add more relevant content
2. **Poor connections**: Run `imos rebuild-links`
3. **Context**: Use more specific questions
4. **API issues**: Check your Groq API key is valid

---

## Advanced Usage

### Q: Can I automate IMOS with scripts?
**A:** Absolutely! IMOS is designed for automation:
```bash
# Batch import
find ~/NewContent -name "*.txt" -exec imos addfile {} \;

# Scheduled questions
imos ask "What tasks are due this week?" > weekly-tasks.txt

# Automated workflows
imos import-folder ~/Daily-Notes && imos rebuild-links
```

### Q: How do I integrate IMOS with other tools?
**A:** IMOS works well with:
- **Text editors**: Import your notes folders
- **Note apps**: Export to supported formats, then import
- **Productivity tools**: Use IMOS output in your workflows
- **Scripts**: Pipe IMOS commands into other tools

### Q: Can multiple people share an IMOS knowledge base?
**A:** Currently, IMOS is single-user. For team use:
1. **Shared folder**: Put `memory.db` in shared directory
2. **Git repository**: Version control your knowledge base
3. **Export/import**: Share specific insights rather than full database

Team features are planned for future releases.

### Q: How do I migrate from other note-taking tools?
**A:** Export strategies by tool:
- **Obsidian**: Export to Markdown, convert to .txt
- **Notion**: Export to Markdown/Word
- **Evernote**: Export to .html, convert to .txt
- **OneNote**: Export sections to .docx
- **Roam**: Export JSON, extract text

After export, use `imos import-folder` on the converted files.

---

## Getting Help

### Q: Where can I get support?
**A:** Multiple support channels:
1. **This FAQ**: Covers common issues
2. **[GitHub Issues](https://github.com/Sumitagarwal-i/IMOS_terminal/issues)**: Bug reports and feature requests
3. **[Community](community.md)**: Connect with other users
4. **Built-in help**: `imos command --help` for specific commands

### Q: How do I report a bug?
**A:** Please include:
1. **IMOS version**: `imos --version`
2. **Python version**: `python --version`
3. **Operating system**: Windows/macOS/Linux
4. **Error message**: Full text of any errors
5. **Steps to reproduce**: What you were trying to do

Post to [GitHub Issues](https://github.com/Sumitagarwal-i/IMOS_terminal/issues) with this information.

### Q: Can I request new features?
**A:** Yes! We welcome feature requests on [GitHub Issues](https://github.com/Sumitagarwal-i/IMOS_terminal/issues). Popular requests include:
- Memory editing and deletion
- More file format support
- Team collaboration features
- Mobile companion app
- Web interface option

---

## Future Development

### Q: What's on the roadmap?
**A:** See our [roadmap](roadmap.md) for detailed plans. Key upcoming features:
- Memory editing capabilities
- Additional file format support
- Team collaboration features
- Performance optimizations
- Mobile apps

### Q: How often is IMOS updated?
**A:** We aim for:
- **Bug fixes**: As needed (usually weekly)
- **Minor features**: Monthly releases
- **Major features**: Quarterly releases

Updates are automatic via `pip install --upgrade imos`.

### Q: Can I contribute to IMOS development?
**A:** Absolutely! Check our [contribution guidelines](https://github.com/Sumitagarwal-i/IMOS_terminal/blob/main/CONTRIBUTING.md) for:
- Code contributions
- Documentation improvements
- Bug reports and testing
- Feature suggestions

---

**Still have questions?** Join our [community](community.md) or open an issue on [GitHub](https://github.com/Sumitagarwal-i/IMOS_terminal/issues)!