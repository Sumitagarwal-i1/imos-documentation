# Contributing to IMOS

Thank you for your interest in contributing to IMOS! This guide will help you get started with contributing code, documentation, or community support.

## 🌟 Ways to Contribute

### 🐛 Report Bugs
Found a bug? Help us fix it:
- Search existing [GitHub Issues](https://github.com/Sumitagarwal-i/IMOS_terminal/issues) first
- Create a detailed bug report with steps to reproduce
- Include your environment details (OS, Python version, IMOS version)

### 💡 Suggest Features
Have ideas for new features?
- Check our [roadmap](roadmap.md) to see what's planned
- Create a feature request issue with detailed use cases
- Join our [discussions](https://github.com/Sumitagarwal-i/IMOS_terminal/discussions) for community feedback

### 📝 Improve Documentation
Help make IMOS more accessible:
- Fix typos or clarify existing documentation
- Create tutorials or guides for specific use cases
- Translate documentation to other languages
- Add code examples and snippets

### 💻 Contribute Code
Ready to code? We welcome:
- Bug fixes for reported issues
- New features from our roadmap
- Performance improvements
- Test coverage improvements

---

## 🚀 Getting Started

### Prerequisites
- **Python 3.8+**: Required for development
- **Git**: For version control
- **Text Editor**: VS Code, PyCharm, or your preferred editor

### Development Setup

1. **Fork and Clone**
   ```bash
   # Fork the repository on GitHub first
   git clone https://github.com/YOUR_USERNAME/IMOS_terminal.git
   cd IMOS_terminal
   ```

2. **Create Virtual Environment**
   ```bash
   # Create virtual environment
   python -m venv imos_dev
   
   # Activate (Windows)
   imos_dev\Scripts\activate
   
   # Activate (macOS/Linux)  
   source imos_dev/bin/activate
   ```

3. **Install Dependencies**
   ```bash
   # Install IMOS in development mode
   pip install -e .
   
   # Install development dependencies
   pip install pytest black flake8 mypy
   ```

4. **Verify Setup**
   ```bash
   # Test that IMOS works
   imos --help
   
   # Run tests
   python -m pytest
   ```

### Project Structure

```
IMOS_terminal/
├── imos/                  # Main package
│   ├── __init__.py       # Package initialization
│   ├── main.py           # CLI entry point
│   ├── memory_db.py      # Database operations
│   ├── embedding.py      # AI model handling
│   └── utils.py          # Utility functions
├── tests/                # Test suite
│   ├── test_main.py      # CLI tests
│   ├── test_memory.py    # Database tests
│   └── test_utils.py     # Utility tests
├── docs/                 # Documentation
├── setup.py              # Package configuration
├── requirements.txt      # Dependencies
└── README.md            # Project overview
```

---

## 🛠️ Development Workflow

### Creating a Feature Branch

1. **Sync with main branch**
   ```bash
   git checkout main
   git pull upstream main
   ```

2. **Create feature branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Make your changes**
   ```bash
   # Edit code
   # Add tests
   # Update documentation
   ```

### Code Standards

#### Python Style Guide
We follow [PEP 8](https://pep8.org/) with these specifics:

```python
# Good: Clear function names and docstrings
def search_memories(query: str, limit: int = 10) -> List[Memory]:
    """Search for memories using semantic similarity.
    
    Args:
        query: The search query string
        limit: Maximum number of results to return
        
    Returns:
        List of Memory objects sorted by relevance
    """
    pass

# Good: Type hints for better code clarity
from typing import List, Optional, Dict, Any

def add_memory(content: str, source: Optional[str] = None) -> int:
    """Add a new memory to the database."""
    pass

# Good: Clear variable names
memory_embeddings = generate_embeddings(content)
similarity_scores = calculate_similarity(query_embedding, memory_embeddings)
```

#### Code Quality Tools

**Black (Code Formatting)**
```bash
# Format all Python files
black imos/ tests/

# Check formatting without changes
black --check imos/ tests/
```

**Flake8 (Linting)**
```bash
# Check code style and quality
flake8 imos/ tests/

# Configuration in setup.cfg
[flake8]
max-line-length = 88
ignore = E203, W503
```

**MyPy (Type Checking)**
```bash
# Check type annotations
mypy imos/

# Configuration in setup.cfg
[mypy]
python_version = 3.8
warn_return_any = True
warn_unused_configs = True
```

### Testing Guidelines

#### Writing Tests
```python
# tests/test_memory.py
import pytest
from imos.memory_db import MemoryDB

def test_add_memory():
    """Test adding a memory to the database."""
    db = MemoryDB(":memory:")  # Use in-memory database for testing
    
    memory_id = db.add_memory("Test content", "test_source.txt")
    
    assert memory_id > 0
    memories = db.search_memories("Test")
    assert len(memories) == 1
    assert memories[0]['content'] == "Test content"

def test_search_empty_database():
    """Test searching in empty database."""
    db = MemoryDB(":memory:")
    
    results = db.search_memories("anything")
    
    assert results == []

# Use fixtures for common setup
@pytest.fixture
def sample_db():
    """Create a database with sample data for testing."""
    db = MemoryDB(":memory:")
    db.add_memory("Python is great", "python_notes.txt")
    db.add_memory("JavaScript is fun", "js_notes.txt")
    return db

def test_search_with_data(sample_db):
    """Test search functionality with sample data."""
    results = sample_db.search_memories("Python")
    
    assert len(results) >= 1
    assert any("Python" in r['content'] for r in results)
```

#### Running Tests
```bash
# Run all tests
python -m pytest

# Run with coverage
python -m pytest --cov=imos

# Run specific test file
python -m pytest tests/test_memory.py

# Run tests with verbose output
python -m pytest -v
```

### Documentation Standards

#### Code Documentation
```python
def import_file(file_path: str, chunk_size: int = 1000) -> List[int]:
    """Import content from a file into memory.
    
    Processes the file content by extracting text, splitting into chunks,
    and adding each chunk as a separate memory with embeddings.
    
    Args:
        file_path: Path to the file to import
        chunk_size: Maximum characters per memory chunk
        
    Returns:
        List of memory IDs that were created
        
    Raises:
        FileNotFoundError: If the specified file doesn't exist
        UnsupportedFileType: If the file type isn't supported
        
    Example:
        >>> memory_ids = import_file("notes.txt", chunk_size=500)
        >>> print(f"Imported {len(memory_ids)} memories")
    """
    pass
```

#### User Documentation
- Use clear, beginner-friendly language
- Include working code examples
- Provide context for when to use features
- Add screenshots for UI elements

---

## 🎯 Contribution Types

### 🐛 Bug Fixes

**Priority Areas:**
- Memory corruption during imports
- Search result accuracy issues
- CLI command parsing errors
- Database connection problems

**Bug Fix Process:**
1. Create issue describing the bug
2. Write a test that reproduces the bug
3. Fix the bug
4. Verify the test passes
5. Submit pull request

### ✨ New Features

**Current Priorities** (see [roadmap](roadmap.md)):
- Memory editing capabilities
- Additional file format support
- Enhanced search filters
- Team collaboration features

**Feature Development Process:**
1. Discuss feature in GitHub Discussions
2. Create detailed design document
3. Break down into smaller tasks
4. Implement with tests
5. Update documentation
6. Submit pull request

### 🔧 Performance Improvements

**Focus Areas:**
- Embedding generation speed
- Search response time
- Memory usage optimization
- Database query performance

**Performance Guidelines:**
- Profile before optimizing
- Include benchmarks in pull requests
- Maintain backward compatibility
- Document performance impacts

### 📚 Documentation

**Documentation Types:**
- **API Documentation**: Code docstrings and type hints
- **User Guides**: How-to tutorials and examples
- **Developer Docs**: Architecture and contribution guides
- **FAQ**: Common questions and troubleshooting

---

## 🚦 Pull Request Process

### Before Submitting

**Checklist:**
- [ ] Code follows style guidelines (black, flake8, mypy)
- [ ] Tests pass locally (`pytest`)
- [ ] New features have tests
- [ ] Documentation updated if needed
- [ ] Commit messages are clear
- [ ] Branch is up-to-date with main

### Pull Request Template

```markdown
## Description
Brief description of changes and motivation.

## Type of Change
- [ ] Bug fix (non-breaking change fixing an issue)
- [ ] New feature (non-breaking change adding functionality)
- [ ] Breaking change (fix or feature causing existing functionality to not work)
- [ ] Documentation update

## Testing
- [ ] Tests pass locally
- [ ] Added tests for new functionality
- [ ] Manual testing performed

## Checklist
- [ ] Code follows style guidelines
- [ ] Self-review completed
- [ ] Documentation updated
- [ ] No breaking changes (or clearly documented)
```

### Review Process

1. **Automated Checks**: CI runs tests and quality checks
2. **Code Review**: Maintainers review for quality and design
3. **Testing**: Manual testing for complex features
4. **Approval**: At least one maintainer approves
5. **Merge**: Squash and merge to main branch

---

## 🏷️ Good First Issues

Perfect for new contributors:

### Beginner-Friendly Tasks

**Documentation Improvements**
- Fix typos in user guides
- Add more code examples
- Improve error message clarity
- Create video tutorials

**Small Code Improvements**
- Add input validation
- Improve error handling
- Add configuration options
- Enhance CLI help text

**Testing**
- Add test cases for edge cases
- Improve test coverage
- Add integration tests
- Performance benchmarking

### Finding Issues

**GitHub Labels:**
- `good first issue` - Perfect for newcomers
- `help wanted` - Community assistance needed
- `documentation` - Documentation improvements
- `bug` - Bug fixes needed
- `enhancement` - New features

**Issue Template:**
```markdown
**Good First Issue: Add file extension validation**

**Description:**
Currently, IMOS doesn't validate file extensions before import, leading to confusing errors.

**Acceptance Criteria:**
- [ ] Validate file extensions in import_file()
- [ ] Show clear error for unsupported formats
- [ ] Add test cases for validation
- [ ] Update documentation

**Estimated Effort:** 2-4 hours
**Skills:** Python, basic file handling
**Files to modify:** imos/utils.py, tests/test_utils.py
```

---

## 🤝 Community Guidelines

### Code of Conduct

**Our Pledge:**
We're committed to making IMOS an welcoming project for everyone, regardless of experience level, background, or identity.

**Expected Behavior:**
- Be respectful and inclusive in all interactions
- Provide constructive feedback and criticism
- Focus on what's best for the community
- Show empathy toward other community members

**Unacceptable Behavior:**
- Harassment or discriminatory language
- Personal attacks or trolling
- Publishing private information without permission
- Other conduct inappropriate in a professional setting

**Enforcement:**
Report unacceptable behavior to [maintainers@imos.dev] *(Coming Soon)*. All complaints will be reviewed and investigated promptly and fairly.

### Communication Channels

**GitHub Discussions**
- Feature requests and ideas
- General questions and help
- Architecture discussions
- Community announcements

**GitHub Issues**  
- Bug reports with detailed reproduction steps
- Specific feature requests with acceptance criteria
- Documentation improvements

**Discord** *(Coming Soon)*
- Real-time community chat
- Development discussions
- Getting started help
- Community events

### Getting Help

**For Contributors:**
- Read this contributing guide thoroughly
- Check existing issues and discussions
- Ask questions in GitHub Discussions
- Join our Discord community *(Coming Soon)*

**For Users:**
- Check the [FAQ](faq.md) first
- Search existing issues
- Create a new issue with details
- Join community discussions

---

## 🏆 Recognition

### Contributor Recognition

**Types of Recognition:**
- **Contributors file**: All contributors listed in CONTRIBUTORS.md
- **Release notes**: Significant contributions highlighted in changelogs
- **Community showcase**: Featured on project website *(Coming Soon)*
- **Swag**: IMOS stickers and merchandise for regular contributors *(Coming Soon)*

### Maintainer Path

**Becoming a Maintainer:**
1. **Consistent contributions** over 3+ months
2. **Community involvement** in discussions and reviews
3. **Quality work** meeting our standards consistently
4. **Demonstrated expertise** in specific areas
5. **Nomination and approval** by existing maintainers

**Maintainer Responsibilities:**
- Review pull requests promptly
- Help guide project direction
- Mentor new contributors
- Maintain code quality standards
- Participate in release planning

---

## 📊 Development Metrics

### Contribution Statistics

**Monthly Goals:**
- 10+ bug fixes
- 5+ feature contributions  
- 20+ documentation improvements
- 50+ community interactions

**Quality Metrics:**
- 95%+ test coverage
- <2 day average review time
- 90%+ user satisfaction
- Zero critical security issues

### Performance Standards

**Code Quality:**
- All code passes automated quality checks
- Comprehensive test coverage for new features
- Clear documentation and examples
- Performance impact considered

**Community Impact:**
- Helpful and respectful interactions
- Constructive feedback and reviews
- Active participation in discussions
- Support for other contributors

---

## 🎉 Getting Started Today

### Your First Contribution

1. **🍴 Fork the repository** on GitHub
2. **📥 Clone your fork** locally
3. **🔧 Set up development environment**
4. **👀 Browse good first issues**
5. **💬 Comment on an issue** you'd like to work on
6. **🏗️ Create a branch** and start coding
7. **✅ Submit a pull request**

### Quick Wins

**15-minute contributions:**
- Fix typos in documentation
- Add code examples to docstrings
- Improve error messages
- Add configuration options

**1-hour contributions:**
- Write test cases for existing features
- Implement small utility functions
- Create tutorial content
- Review and test pull requests

**Weekend project contributions:**
- Implement new file format support
- Add search filter options
- Create comprehensive tutorials
- Build performance benchmarks

---

**Ready to contribute? We're excited to work with you!**

*Check out our [good first issues](https://github.com/Sumitagarwal-i/IMOS_terminal/labels/good%20first%20issue) and join the conversation in [GitHub Discussions](https://github.com/Sumitagarwal-i/IMOS_terminal/discussions).*