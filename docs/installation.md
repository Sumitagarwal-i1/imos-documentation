# Installation Guide

Getting IMOS up and running is quick and easy. Follow these steps based on your operating system and preferences.

## Prerequisites

- **Python 3.8 or higher** (check with `python --version`)
- **pip** (Python package manager - usually comes with Python)
- **Internet connection** (for initial setup and AI features)

## Quick Install

### Option 1: Install from PyPI (Recommended)

```bash
pip install imos
```

That's it! IMOS is now installed and ready to use.

### Option 2: Install with User Flag (if permissions issues)

```bash
pip install --user imos
```

### Option 3: Install in Virtual Environment (Advanced)

```bash
# Create virtual environment
python -m venv imos-env

# Activate it
# Windows:
imos-env\Scripts\activate
# macOS/Linux:
source imos-env/bin/activate

# Install IMOS
pip install imos
```

## Verify Installation

Test that IMOS is properly installed:

```bash
imos --help
```

You should see the IMOS help menu with available commands.

## API Key Setup (Required for Chat Features)

IMOS uses Groq's fast AI models for intelligent conversations. Setting up your API key is free and takes 2 minutes:

### Step 1: Get Your Free API Key

1. Visit [Groq Console](https://console.groq.com/)
2. Sign up for a free account (no credit card required)
3. Navigate to "API Keys" in your dashboard
4. Click "Create API Key"
5. Copy your API key (starts with `gsk_...`)

### Step 2: Set Your API Key

Choose one of these methods:

#### Method 1: Environment Variable (Recommended)

**Windows (Command Prompt):**
```cmd
set GROQ_API_KEY=your_api_key_here
```

**Windows (PowerShell):**
```powershell
$env:GROQ_API_KEY="your_api_key_here"
```

**macOS/Linux:**
```bash
export GROQ_API_KEY="your_api_key_here"
```

#### Method 2: .env File (Persistent)

Create a `.env` file in your working directory:

```bash
echo "GROQ_API_KEY=your_api_key_here" > .env
```

Or create it manually with any text editor:
```
GROQ_API_KEY=your_api_key_here
```

## Test Complete Setup

Verify everything is working:

```bash
# Test basic functionality
imos add "This is my first memory"

# Test AI features (requires API key)
imos ask "What do I know?"
```

You should see IMOS respond with information about your first memory.

## Troubleshooting

### Python Not Found
**Error**: `'python' is not recognized as an internal or external command`

**Solution**: 
- Windows: Install Python from [python.org](https://python.org) and check "Add to PATH"
- macOS: Install Python via [python.org](https://python.org) or `brew install python`
- Linux: Use your package manager: `sudo apt install python3 python3-pip`

### Pip Not Found
**Error**: `'pip' is not recognized`

**Solution**:
```bash
python -m ensurepip --upgrade
```

### Permission Errors
**Error**: `Permission denied` when installing

**Solutions**:
1. Use `pip install --user imos`
2. On macOS/Linux: `sudo pip install imos`
3. Use a virtual environment (recommended)

### IMOS Command Not Found
**Error**: `'imos' is not recognized`

**Solutions**:
1. Restart your terminal
2. Check if pip's script directory is in your PATH
3. Try `python -m imos` instead
4. Reinstall with `pip install --user imos`

### API Key Issues
**Error**: `IMOS Setup Required!` or authentication errors

**Solutions**:
1. Verify your API key is correct (starts with `gsk_`)
2. Check your environment variable: `echo $GROQ_API_KEY`
3. Try using a `.env` file instead
4. Restart your terminal after setting environment variables

### Slow Performance
**Issue**: IMOS feels slow on first run

**Explanation**: This is normal! IMOS downloads the AI model on first use (~100MB). Subsequent runs are lightning fast.

## System Requirements

### Minimum Requirements
- **RAM**: 2GB available
- **Storage**: 1GB free space (for AI models and your memories)
- **CPU**: Any modern processor (2010+)

### Recommended Requirements
- **RAM**: 4GB or more
- **Storage**: 5GB free space
- **CPU**: Multi-core processor for best performance

## Next Steps

Now that IMOS is installed:

1. **[Quick Start Guide](getting-started.md)** - Learn the basics in 10 minutes
2. **[Command Reference](commands.md)** - Explore all available features
3. **[Use Cases](use-cases.md)** - See real-world examples

## Updates

To update IMOS to the latest version:

```bash
pip install --upgrade imos
```

Check your current version:
```bash
imos --version
```

---

**Need help?** Visit our [FAQ](faq.md) or join our [community](community.md) for support.