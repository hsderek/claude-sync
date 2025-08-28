# LogReducer Development Guide

## Project Overview

LogReducer is a high-performance log processing system designed for reducing large log files while maintaining operational visibility. The system implements advanced pattern extraction, anomaly detection, and temporal analysis algorithms.

## Current Project Status (August 26, 2025)

### Completed Implementation ✓
- **Core LogReducer functionality**: Pattern extraction, anomaly detection, temporal analysis working
- **Enterprise Configuration**: HyperSec EULA licensing, professional branding throughout
- **CLI Interface**: Complete command-line interface with processing estimation
- **Output Formats**: LINE (default), JSON, JSONL with metadata support
- **Professional API Design**: Silent by default, proper logging, no print statements
- **Memory Management**: Configurable limits with enforcement testing
- **CPU Auto-detection**: Container-aware CPU core detection for threading
- **Security Scanning**: Comprehensive vulnerability detection pipeline
- **CI/CD Pipeline**: GitHub Actions with semantic-release automation
- **Documentation**: Sphinx docs, VS Code workspace, comprehensive README
- **Directory Structure**: Moved to `/data/output` structure, samples organized
- **Changelog**: Fixed dates working back from August 26, 2025 - LOCKED for semantic-release only
- **Git Repository**: Initialized with semantic versioning and automated releases
- **Dependencies**: Core deps updated (numpy, scikit-learn moved to core from optional)
- **Production Ready**: Full API testing passed, ready for PyPI deployment
- **Version 3.2.0**: Manually bumped version due to CI issues, semantic-release temporarily disabled
- **Generic Python Template**: Script structure designed for reuse as Python project template

### Verified Working ✓  
- **API Import**: `import logreducer` successful, LogReducer instances create without errors
- **Silent Operation**: API completely silent by default, perfect for production integration
- **Processing Modes**: Pattern, anomaly, temporal, and hybrid modes all functional
- **Configuration System**: Level/mode settings, memory limits, CPU auto-detection working
- **Output Formats**: LINE, JSON, JSONL formats with metadata support
- **Statistics Collection**: Processing metrics, reduction rates, performance data available
- **Professional Logging**: No print statements, proper logging with console/file options
- **Virtual Environment**: uv-managed .venv with all dependencies resolved
- **Git Automation**: Pushes trigger semantic-release, version bumps automated
- **Text Cleanup**: All unprofessional emojis removed, professional presentation maintained

## Architecture Principles

### Core Design
- Memory-safe streaming for unbounded file sizes
- Adaptive processing based on file characteristics  
- Configurable quality levels (Standard, Enhanced, Maximum)
- Multiple processing modes (Pattern, Anomaly, Temporal, Hybrid)

### Performance Targets
- Process 1GB logs in <30 seconds
- Achieve 90%+ reduction while preserving critical events
- Support concurrent processing of multiple files
- Memory usage capped at 500MB for streaming mode

## Development Guidelines

### Script Architecture
- **ALWAYS check `pdev` or `ci-helper` before creating new scripts**
- Developer commands belong in `scripts/pdev`
- CI/CD utilities belong in `scripts/ci-helper`
- Common functions go in `scripts/common.py`
- Only create standalone scripts for bootstrap operations (like setup)
- Consolidation prevents duplication and maintains consistency

### File System Usage
- **ALWAYS use `./.tmp` directory for temporary files and automation work**
- Never use `/tmp`, `~/tmp`, or system temporary directories for project automation
- All temporary processing, test outputs, development artifacts, and script work goes in `./.tmp`
- The `./.tmp` directory is git-ignored and project-local
- **Important:** This is for automation tooling only - the actual LogReducer application uses its own configured temp paths

### Code Style
- Follow PEP 8 with 88-character line length (Black formatter)
- Type hints for all public functions
- Comprehensive docstrings for modules and classes
- Unit tests for all new functionality

### Testing Strategy
- Unit tests: Individual component validation
- Integration tests: End-to-end workflows with real data
- Performance tests: Benchmark against sample datasets
- Coverage target: Maintain >90% test coverage

### Key Algorithms

#### Pattern Extraction (Drain3)
- Similarity threshold: 0.4-0.9 (configurable)
- Depth: 4 levels for parse tree
- Min occurrences: 2+ for pattern recognition
- Priority scoring based on error keywords and complexity

#### Anomaly Detection
- Isolation Forest with contamination rate 0.1
- TF-IDF vectorization for feature extraction
- Fallback to statistical methods when ML unavailable
- Adaptive thresholds based on data distribution

#### Temporal Analysis
- Time window: 60 minutes default (configurable)
- Pattern clustering by time buckets
- Hour-of-day and day-of-week analysis
- Event burst detection

## Configuration

### BigDial Framework
The configuration system uses a centralized BigDialConfig class:
- Environment variable overrides
- YAML configuration support
- Runtime parameter adjustment
- Validation and bounds checking

### Processing Levels
1. **Standard**: Basic pattern extraction, 70%+ reduction
2. **Enhanced**: Add anomaly detection, 80%+ reduction  
3. **Maximum**: Full analysis suite, 90%+ reduction

## Deployment

### Package Structure
```
src/logreducer/       # Source code
data/samples/         # Test datasets
tests/               # Test suite
scripts/             # Utility scripts
```

### Release Process
1. Semantic versioning (MAJOR.MINOR.PATCH)
2. Conventional commits for automated versioning
3. GitHub Actions CI/CD pipeline
4. JFrog Artifactory for private PyPI

### Dependencies
Core:
- drain3: Pattern extraction engine
- loguru: Structured logging
- tqdm: Progress visualization
- psutil: Memory monitoring
- numpy: Numerical operations (moved from optional)
- scikit-learn: Machine learning (moved from optional)

Optional (Enhanced):
- scipy: Advanced numerical operations
- polars: High-performance DataFrames
- datasketch: MinHash deduplication
- xxhash: Fast hashing algorithms

## Performance Optimization

### Memory Management
- Streaming processing for large files
- Batch sizes: 1000-10000 lines (adaptive)
- Memory monitoring with automatic throttling
- Efficient hash algorithms (xxhash when available)

### Caching Strategy
- LRU cache for pattern matching
- Memoization of expensive computations
- Persistent cache between runs (optional)

### Parallelization
- Multiprocessing for independent files
- Async I/O for cloud storage
- Thread pools for pattern matching

## Sample Datasets

The project includes 10 real-world log formats from LogHub:
- Apache, HDFS, Linux system logs
- OpenStack, Spark, Zookeeper logs
- HPC clusters (Thunderbird, BGL)
- Android, network proxy logs

## Troubleshooting

### Common Issues
1. **OOM on large files**: Reduce batch_size in config
2. **Slow processing**: Check if enhanced features disabled
3. **Low reduction**: Adjust min_pattern_occurrences
4. **Missing patterns**: Lower drain_similarity threshold

### Debug Mode
Set environment: `LOGREDUCER_DEBUG=1`
Enables verbose logging and performance profiling.

## Changelog Management

**IMPORTANT**: The changelog is now locked and should NOT be manually edited by anyone, including Claude.

- The current CHANGELOG.md reflects the complete development history up to August 25, 2025
- All future changelog updates must be handled exclusively by semantic-release automation
- This includes version bumps, release notes, and changelog entries
- Manual changelog edits are prohibited to maintain consistency with semantic versioning
- Use conventional commit messages for semantic-release to work properly

## Python Project Template Components

This project structure is designed to be reusable as a **generic Python project template**. The following components can be extracted and reused:

### ✅ **Generic Template Structure**
- **`Makefile`** - Industry standard interface calling Python scripts
- **`scripts/pdev`** - Generic Python development commands (replaces project-specific names)
- **`scripts/setup`** - Environment setup with tool requirements checking
- **`scripts/common.py`** - Centralized logging & configuration utilities
- **`scripts/security_scan.py`** - Comprehensive security scanning
- **`scripts/test_editable_install.py`** - PEP 660 editable install testing

### ✅ **Professional Logging System**
- **Tee Approach**: Scripts log to both console AND file by default  
- **Module Approach**: Only logs to file if path provided, console if specified
- **RFC 3339 Timestamps**: `2025-08-27T15:55:44.389+10:00` format
- **Enterprise Configuration**: ConfigMap → ENV vars → CLI args precedence
- **Dynaconf Integration**: YAML + environment variable + CLI argument precedence

### ✅ **CI/CD Pipeline Template**
- **Multi-stage workflow**: test → security → build → release → deploy
- **Python version detection**: Dynamic from `.python-version-config.yaml`
- **Security integration**: Uses unified security scan script
- **Semantic release**: Automated versioning and changelog
- **Professional output**: No emojis, clear status indicators

### ✅ **Hybrid Development Workflow**
**Industry Standard Make + Professional Python Scripts:**
```bash
# One-time setup
make setup

# Daily development (Make - Industry Standard)
make test               # Run all tests
make format             # Format code
make lint              # Run linting
make security          # Security scan
make all               # Run everything

# Alternative: Direct script usage
scripts/setup           # Environment setup
scripts/pdev test       # Python script with professional logging
```

**Best of Both Worlds:**
- **Make**: Industry standard, simple commands, parallel execution
- **Python Scripts**: Professional logging, configuration management, cross-platform
- **Template Ready**: Both Makefile and scripts/ can be reused across projects

### ✅ **Configuration Management**
- **`common.py`**: Centralized config utilities with enterprise patterns
- **`config.yaml`**: Auto-generated default configuration  
- **Environment Variables**: `APP_` prefix with override precedence
- **CLI Arguments**: Final override precedence
- **Kubernetes Ready**: ConfigMap/Secret mounting patterns

### ✅ **Template Extraction Guidelines**
When creating the generic template:
1. **Replace project-specific references** in help text and comments
2. **Keep `scripts/pdev`** name for consistency across all Python projects  
3. **Update `pyproject.toml`** with template project structure
4. **Preserve logging/config patterns** - they work for any Python project
5. **Keep professional emoji-free output** - suitable for enterprise use
6. **Maintain tool requirement checking** - ensures consistent dev environments

### ✅ **Template Benefits**
- **Consistent Development**: Same commands across all Python projects
- **Enterprise Ready**: Professional logging, configuration, CI/CD  
- **Security Built-in**: Comprehensive scanning from day one
- **Auto-Environment**: No manual venv activation needed
- **Scale Ready**: Supports development to production deployment

## Future Enhancements

### High Priority
- **Fix Semantic-Release CI**: Troubleshoot and fix GitHub Actions semantic-release automation
  - Currently disabled due to failing builds causing CI spam
  - Workflow has permissions and environment loading issues
  - Debug output added but automation still not triggering version bumps
  - Need to investigate GitHub token permissions and semantic-release configuration
  - Version manually updated to 3.2.0 until automation is fixed
- **Metrics Integration**: Metrics functionality has been moved to a separate module for better separation of concerns

### Medium Priority
- Real-time streaming mode
- Distributed processing support
- Custom pattern libraries
- Web-based visualization dashboard
- Integration with log management systems

## Testing Commands

```bash
# Run all tests
pytest tests/

# Run with coverage
pytest --cov=logreducer --cov-report=html

# Run specific test suite
pytest tests/unit/
pytest tests/integration/

# Performance benchmarks
python scripts/benchmark.py
```

## Development Setup

### Quick Environment Check
```bash
# Check if all required development tools are installed
python scripts/check_dev_tools.py

# Show installation guide for missing tools
python scripts/check_dev_tools.py --install

# Show dfe-fedora-desktop VM setup information
python scripts/check_dev_tools.py --vm-info
```

### Manual Setup
```bash
# Create virtual environment with uv (REQUIRED)
uv venv .venv
source .venv/bin/activate  # Linux/Mac
.venv\Scripts\activate     # Windows

# Install development dependencies
uv pip install -e ".[dev,enhanced]"

# Initialize Git LFS and commit hooks
git lfs install
npm install && npx husky install

# Run code formatters
black src/ tests/
isort src/ tests/

# Type checking
mypy src/logreducer/

# Security scanning (automated in CI)
python scripts/security_scan.py

# Test API functionality
python -c "import logreducer; print('Version:', logreducer.__version__)"
```

### Required Development Tools
The development environment requires:
- **Python 3.12+**: Core language and interpreter
- **uv**: Fast Python package installer and resolver
- **Git 2.34+**: Version control with Git LFS support
- **Node.js 18+**: For Husky commit hooks
- **GitHub CLI**: Repository management and automation

Run `python scripts/check_dev_tools.py` to verify all tools are installed and properly configured.

## Claude Code VS Code Integration Fixes (August 28, 2025)

### Fixed Startup Issues
1. **Path Error Resolution**: Removed incorrect `/projects/infra-jira-github` reference from `.claude/settings.local.json`
   - The path didn't exist (actual path is `/projects/cicd-jira-github`)
   - Cleaned up all absolute path permissions that were pointing to other projects
   - Permissions should be relative to project root, not OS root

2. **Double venv Activation Fix**: Disabled VS Code Python extension's auto-activation
   - Set `"python.terminal.activateEnvironment": false` in `.vscode/settings.json`
   - Claude Code handles venv activation automatically
   - Prevents duplicate activation commands in terminal

3. **Claude VS Code Settings Added**: Enhanced integration settings in `.vscode/settings.json`
   ```json
   "claude.alwaysAllowReadOnly": true,
   "claude.alwaysAllowEdits": true,
   "claude.confirmBeforeEdit": false,
   "claude.confirmBeforeRead": false
   ```

### Current Configuration Status
- `.claude/settings.local.json`: Contains clean project-specific permissions without cross-project references
- `.vscode/settings.json`: Includes Claude integration settings and disabled Python auto-activation
- Virtual environment: Located at `.venv/` and properly detected by Claude Code
- No more startup errors about missing paths or duplicate venv activation

## Important Notes for Future Sessions

### Virtual Environment Management
- **ALWAYS use uv**: `uv venv .venv` and `uv pip install` for dependency management
- The project requires numpy and scikit-learn as core dependencies (not optional)
- If .venv is corrupted, remove it completely and recreate with uv

### Git Workflow
- Repository is at: https://github.com/hypersec-io/logreducer
- Uses semantic-release for automated versioning and changelog updates  
- All commits should use conventional commit format for proper automation
- Push changes to trigger CI/CD pipeline and version bumps

### Key Configuration
- Logging is OFF by default (`enable_logging: bool = False`)
- Output directory is `/data/output` (moved from `/output`)
- CPU detection is container-aware for proper threading
- Memory limits are enforced and tested
- All text has been cleaned of unprofessional emojis
- Current version: 3.2.1
- Scripts consolidated: `pdev` for dev, `ci-helper` for CI/CD, `setup` for bootstrap
- Common functions in `scripts/common.py`
- Python floor version: 3.11 (this project uses 3.12 via .python-version)

### Known Issues
- **Semantic-release CI**: GitHub Actions automation failing, currently disabled to prevent spam
- Need to debug semantic-release configuration and GitHub token permissions
- Manual version management in use until CI is fixed

## Corporate Python Project Template Recommendations (August 28, 2025)

### CI/CD Architecture Analysis

Based on comprehensive analysis of the LogReducer CI/CD pipeline, here are the key recommendations for using this as a corporate-wide Python project template:

#### ✅ Strengths (Keep As-Is)

1. **Multi-Stage CI Pipeline**
   - Clear separation: test → security → build → deploy
   - Parallel job execution where possible
   - Smart caching strategies for dependencies
   - Comprehensive test coverage reporting

2. **Semantic Release Integration**
   - Automated versioning based on conventional commits
   - Changelog generation from commit history
   - Multiple version file synchronization (pyproject.toml, __init__.py, VERSION)
   - GitHub release creation with artifacts

3. **Security-First Approach**
   - Security scanning integrated but non-blocking (allows deployment while alerting)
   - Multiple security tools: pip-audit, bandit, optional semgrep
   - Dedicated security workflow for scheduled scans
   - Security reports stored in `.tmp/security-reports/`

4. **Script Consolidation**
   - Clean separation: `pdev` (dev), `ci-helper` (CI/CD), `setup` (bootstrap)
   - Configuration-driven via YAML files
   - Common utilities in `scripts/common.py`
   - Professional logging with RFC 3339 timestamps

5. **Environment Management**
   - Python version detection from `.python-version-config.yaml`
   - Virtual environment auto-detection and creation
   - Container-aware CPU detection for proper threading
   - Memory management with configurable limits

#### ⚠️ Areas Needing Attention

1. **Semantic Release Configuration**
   - Currently requires manual `semantic-release` installation
   - GitHub token permissions need proper setup
   - Consider using `python-semantic-release` v8+ for better Python integration
   - Add `.releaserc.json` for cleaner configuration

2. **Local CI Testing**
   - `act` requires GitHub authentication for action downloads
   - Consider creating offline-capable CI tests
   - Add Docker-based local CI option without GitHub dependencies

3. **Documentation Generation**
   - Sphinx configuration present but not integrated into CI
   - Add automated documentation deployment to GitHub Pages
   - Consider adding API documentation generation

#### 🎯 Template Extraction Checklist

When creating the corporate template from this project:

1. **Replace Project-Specific References**
   ```yaml
   # In CI workflows, replace:
   - "logreducer" → "{{ project_name }}"
   - "hypersec.jfrog.io" → "{{ artifactory_url }}"
   - HyperSec references → "{{ company_name }}"
   ```

2. **Create Template Structure**
   ```
   corporate-python-template/
   ├── .github/
   │   ├── workflows/
   │   │   ├── ci.yml.template
   │   │   ├── release-python.yml.template
   │   │   └── security.yml.template
   │   └── runner-env.sh
   ├── scripts/
   │   ├── setup           # Keep as-is
   │   ├── pdev           # Keep as-is
   │   ├── ci-helper     # Keep as-is
   │   ├── common.py     # Keep as-is
   │   ├── pdev.yaml.template
   │   └── ci-helper.yaml.template
   ├── src/
   │   └── {{ project_name }}/
   │       ├── __init__.py.template
   │       └── py.typed
   ├── tests/
   │   ├── conftest.py
   │   └── test_sample.py.template
   ├── .python-version-config.yaml
   ├── pyproject.toml.template
   ├── Makefile
   ├── README.md.template
   └── cookiecutter.json   # For template variables
   ```

3. **Add Cookiecutter Configuration**
   ```json
   {
     "project_name": "my_project",
     "project_slug": "{{ cookiecutter.project_name.lower().replace(' ', '_').replace('-', '_') }}",
     "company_name": "CompanyName",
     "artifactory_url": "https://company.jfrog.io",
     "python_version": "3.12",
     "author_name": "Development Team",
     "author_email": "dev@company.com",
     "enable_semantic_release": true,
     "enable_security_scanning": true,
     "enable_docs": false
   }
   ```

4. **CI/CD Configuration Variables**
   - Store sensitive data in GitHub Secrets
   - Use GitHub Variables for non-sensitive configuration
   - Document required secrets in template README

5. **Recommended GitHub Secrets Setup**
   ```
   Required Secrets:
   - ARTIFACTORY_USERNAME     # For package deployment
   - ARTIFACTORY_PASSWORD     # For package deployment
   - PYPI_API_TOKEN          # Optional: For public PyPI
   
   Required Variables:
   - ENABLE_ARTIFACTORY_DEPLOYMENT  # true/false
   - ENABLE_PYPI_DEPLOYMENT         # true/false
   - PYTHON_VERSION                 # Default Python version
   ```

#### 🚀 Deployment Strategy Recommendations

1. **Branch Strategy**
   - `main` → Production deployments
   - `develop` → Staging deployments
   - `feature/*` → Development builds only
   - Use branch protection rules

2. **Release Process**
   - Enforce conventional commits via commitlint
   - Use semantic-release for automated versioning
   - Create GitHub releases with changelog
   - Deploy to appropriate PyPI repository based on branch

3. **Testing Strategy**
   - Unit tests: Always run, fast feedback
   - Integration tests: Run on PR and main
   - Security scans: Non-blocking but visible
   - Performance tests: Optional, scheduled

#### 📋 Implementation Priority

1. **Phase 1: Core Template** (Week 1)
   - Extract scripts/ directory as-is
   - Create cookiecutter template structure
   - Document setup process

2. **Phase 2: CI/CD Templates** (Week 2)
   - Parameterize GitHub workflows
   - Add local CI testing options
   - Create deployment documentation

3. **Phase 3: Security & Compliance** (Week 3)
   - Integrate corporate security policies
   - Add compliance checking workflows
   - Create security documentation

4. **Phase 4: Documentation & Training** (Week 4)
   - Create template usage guide
   - Add example projects
   - Conduct team training sessions

#### 🔧 Maintenance Considerations

1. **Version Management**
   - Use semantic-release for all projects
   - Maintain VERSION file for non-Python consumers
   - Synchronize all version references automatically

2. **Dependency Updates**
   - Use Dependabot for automated updates
   - Pin major versions, allow minor/patch updates
   - Regular security vulnerability scanning

3. **Template Updates**
   - Maintain template in separate repository
   - Version the template itself
   - Provide migration guides for template updates

#### 💡 Best Practices for Template Users

1. **Initial Setup**
   ```bash
   cookiecutter gh:company/python-template
   cd my_project
   scripts/setup
   ```

2. **Development Workflow**
   ```bash
   scripts/pdev test     # Run tests
   scripts/pdev format   # Format code
   scripts/pdev all      # Run all checks
   ```

3. **CI/CD Integration**
   - Configure GitHub Secrets before first push
   - Use conventional commits from the start
   - Review security scan results regularly

4. **Documentation**
   - Keep README.md updated
   - Document API changes
   - Maintain CHANGELOG via semantic-release

This template provides a production-ready foundation for Python projects with enterprise-grade CI/CD, security scanning, and automated release management

## Claude State Sync Script (STANDALONE - DO NOT INTEGRATE)

### Important: `scripts/claude-sync` is STANDALONE

The `scripts/claude-sync` script is a **COMPLETELY STANDALONE UTILITY** that must remain independent of any project. 

**CRITICAL RULES FOR CLAUDE SESSIONS:**
1. **DO NOT integrate claude-sync into pdev** - It's standalone by design
2. **DO NOT add claude-sync to any project scripts** - It operates independently  
3. **DO NOT make the project aware of claude-sync** - The project should have zero knowledge of it
4. **DO NOT commit claude-sync to the main repo** - It's in .gitignore for a reason
5. **DO NOT create dependencies on claude-sync** - It must work across any project
6. **DO NOT use project venv** - It uses system Python with no pip dependencies
7. **DO NOT assume any project setup** - It works with zero configuration

### How Claude Sync Works

The script syncs Claude-specific files to a central repository (`https://github.com/hsderek/claude-sync`) with subdirectories for each project:

```
claude-sync/
├── scripts/             # Standalone scripts
│   ├── claude-sync      # The sync script
│   └── README.md        # Script documentation
├── logreducer/          # This project
│   ├── CLAUDE.md
│   ├── .claude/
│   └── docs/
├── another-project/     # Another project
│   ├── CLAUDE.md
│   └── .claude/
└── yet-another/         # Yet another project
    ├── CLAUDE.md
    └── .claude/
```

### Usage (Standalone)

```bash
# Run with system Python (NOT project venv!)
/usr/bin/python3 scripts/claude-sync

# Or make it executable and run directly
chmod +x scripts/claude-sync
./scripts/claude-sync

# With custom message
./scripts/claude-sync --message "feat: Add new template recommendations"

# Dry run to see what would be synced
./scripts/claude-sync --dry-run
```

### Configuration

The script reads from `.env` (but doesn't require it):
```bash
CLAUDE_STATE_REPO=https://github.com/hsderek/claude-sync
CLAUDE_STATE_SUBDIR=logreducer  # Auto-detected from directory name
```

### Files Synced

- `CLAUDE.md` - This file with all development context
- `.claude/` - Claude Code settings
- `scripts/claude-sync` - The sync script itself
- `scripts/README.md` - Scripts documentation
- `.vscode/settings.json` - VS Code Claude integration
- Various `docs/*.md` files about development

### Why Completely Standalone?

1. **No Git Interference**: Uses temporary clones, never touches local git
2. **No Python Dependencies**: Uses only Python stdlib, no pip packages
3. **No Virtual Environment**: Uses system Python directly
4. **Concurrent Safe**: Multiple projects can sync simultaneously  
5. **No CI/CD Triggers**: Excluded from all automation
6. **Cross-Project**: Works identically across any project
7. **Zero Configuration**: Works even without .env file

### For New Claude Sessions

If you're a new Claude session working on this project:
- **NEVER** integrate claude-sync into the project workflow
- **NEVER** add it to pdev or other scripts
- **ALWAYS** keep it as a standalone utility
- The project itself should remain unaware of claude-sync's existence

## End-of-Day Sequence for Claude Sessions

### Standard End-of-Day Request (Copy & Paste)

```
Please perform the end-of-day sequence:

1. Summarize today's work
2. Update CLAUDE.md if needed
3. Check git status  
4. Run claude-sync to backup state
5. Create handover notes for next session
6. Verify CI/CD still works

Project: logreducer
Claude sync repo: https://github.com/hsderek/claude-sync
```

### What Claude Should Do

1. **Summary**: List accomplishments and pending tasks
2. **Git Check**: Show modified files and what shouldn't be committed
3. **Sync State**: Run `/usr/bin/python3 scripts/claude-sync`
4. **Handover**: Create notes for session continuity
5. **Validation**: Ensure project still builds and tests pass

### Quick Commands

```bash
# Check status
git status --short

# Sync Claude state
/usr/bin/python3 scripts/claude-sync --message "eod: [summary]"

# Verify tests
scripts/pdev test-unit

# Check versions
scripts/pdev version-check
```

See `CLAUDE_END_OF_DAY.md` for the full template and customization options.