---
title: Installation
---

# Installation Guide

This guide covers installation for different use cases: data consumption, API integration, and development.

## For Data Consumers

### Download Pre-Built Datasets

No installation required! Simply download the files:

1. Go to [Releases](https://github.com/open-ev-data/open-ev-data-dataset/releases/latest)
2. Download your preferred format:
   - `vehicles.json` (23 MB)
   - `vehicles.db` (18 MB)
   - `vehicles.sql` (25 MB)
   - `vehicles.csv` (15 MB)
   - `vehicles.xml` (28 MB)

### Verify Downloads

Check file integrity with SHA256 checksums:

```bash
sha256sum -c vehicles.json.sha256
```

## For API Consumers

### No Installation Needed

The API is hosted and ready to use:

**Base URL**: `https://api.open-ev-data.org/v1`

Test the connection:

```bash
curl https://api.open-ev-data.org/v1/health
```

### Optional: API Client Libraries

=== "Python"

    ```bash
    pip install requests
    ```

=== "JavaScript"

    Built-in `fetch` API (no installation needed)

=== "Rust"

    Add to `Cargo.toml`:
    ```toml
    [dependencies]
    reqwest = { version = "0.12", features = ["json"] }
    tokio = { version = "1", features = ["full"] }
    ```

## For Contributors

### Dataset Development

#### Prerequisites

- **Git**: [Download](https://git-scm.com/)
- **Node.js**: Version 18+ [Download](https://nodejs.org/)
- **Text Editor**: VS Code recommended [Download](https://code.visualstudio.com/)

#### Installation Steps

```bash
git clone https://github.com/open-ev-data/open-ev-data-dataset.git
cd open-ev-data-dataset
npm install
npm run validate
```

#### Verify Installation

```bash
npm run validate
```

Expected output:
```
✓ Schema validation passed
✓ All vehicles valid
✓ Sources verified
Total vehicles: 1234
```

### API Development

#### Prerequisites

- **Git**: [Download](https://git-scm.com/)
- **Rust**: Version 1.80+ [Install](https://rustup.rs/)
- **Cargo**: Included with Rust

#### Installation Steps

```bash
rustup install stable
rustup default stable
```

Clone and build:

```bash
git clone https://github.com/open-ev-data/open-ev-data-api.git
cd open-ev-data-api
cargo build --release
```

#### Verify Installation

```bash
cargo test --all
cargo clippy
```

Expected output:
```
running 45 tests
test result: ok. 45 passed; 0 failed; 0 ignored
```

### Documentation Development

#### Prerequisites

- **Git**: [Download](https://git-scm.com/)
- **Python**: Version 3.13+ [Download](https://www.python.org/)
- **Poetry**: [Install](https://python-poetry.org/docs/#installation)

#### Installation Steps

Install Poetry:

```bash
curl -sSL https://install.python-poetry.org | python3 -
```

Clone and install:

```bash
git clone https://github.com/open-ev-data/open-ev-data.github.io.git
cd open-ev-data.github.io
poetry install
```

#### Verify Installation

```bash
poetry run mkdocs serve
```

Visit `http://localhost:8000` to see the documentation.

## Multi-Repository Workspace Setup

For contributors working across multiple repositories.

### Step 1: Create Parent Directory

```bash
mkdir open-ev-data
cd open-ev-data
```

### Step 2: Clone All Repositories

```bash
git clone https://github.com/open-ev-data/open-ev-data-dataset.git
git clone https://github.com/open-ev-data/open-ev-data-api.git
git clone https://github.com/open-ev-data/open-ev-data.github.io.git
git clone https://github.com/open-ev-data/.github.git
```

### Step 3: Open Workspace

```bash
code .github/open-ev-data.code-workspace
```

Or in Cursor:

```bash
cursor .github/open-ev-data.code-workspace
```

### Step 4: Install All Dependencies

In separate terminals:

```bash
cd open-ev-data-dataset && npm install

cd ../open-ev-data-api && cargo build

cd ../open-ev-data.github.io && poetry install
```

## System Requirements

### Minimum Requirements

| Component | Requirement |
|-----------|-------------|
| **RAM** | 4 GB |
| **Disk Space** | 1 GB free |
| **OS** | Linux, macOS, Windows 10+ |
| **Internet** | Required for downloads |

### Recommended Requirements

| Component | Requirement |
|-----------|-------------|
| **RAM** | 8 GB+ |
| **Disk Space** | 5 GB+ free |
| **CPU** | 4 cores+ |
| **OS** | Linux, macOS, Windows 11 |

## Platform-Specific Notes

### Windows

Install Git Bash or WSL2 for better compatibility:

```powershell
wsl --install
```

Use PowerShell for native Windows commands.

### macOS

Install Xcode Command Line Tools:

```bash
xcode-select --install
```

Use Homebrew for package management:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### Linux

Install build essentials:

=== "Ubuntu/Debian"

    ```bash
    sudo apt update
    sudo apt install build-essential git curl
    ```

=== "Fedora/RHEL"

    ```bash
    sudo dnf groupinstall "Development Tools"
    sudo dnf install git curl
    ```

=== "Arch"

    ```bash
    sudo pacman -S base-devel git curl
    ```

## Docker Setup (Optional)

### API Server

Pull the Docker image:

```bash
docker pull ghcr.io/open-ev-data/ev-server:latest
```

Run the server:

```bash
docker run -p 3000:3000 \
  -v $(pwd)/vehicles.db:/app/vehicles.db:ro \
  ghcr.io/open-ev-data/ev-server:latest
```

### Documentation

Build and serve locally:

```bash
docker build -t openev-docs .
docker run -p 8000:8000 openev-docs
```

## Troubleshooting

### Node.js Installation Issues

Check version:

```bash
node --version
npm --version
```

If outdated, use nvm:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
nvm install 18
nvm use 18
```

### Rust Installation Issues

Update Rust:

```bash
rustup update
```

Check version:

```bash
rustc --version
cargo --version
```

### Poetry Installation Issues

Verify installation:

```bash
poetry --version
```

Update Poetry:

```bash
poetry self update
```

### Permission Errors

On Linux/macOS, avoid using `sudo` with npm:

```bash
npm config set prefix ~/.npm-global
export PATH=~/.npm-global/bin:$PATH
```

## Next Steps

<div class="grid cards" markdown>

-   [**Quick Start Guide**](quick-start.md)
    
    Start using the data

-   [**Contributing Guide**](../guides/contributing.md)
    
    Make your first contribution

-   [**Development Setup**](../guides/development-setup.md)
    
    Complete development environment

-   [**Architecture Overview**](../documentation/architecture.md)
    
    Understand the system

</div>

## Get Help

- [GitHub Issues](https://github.com/open-ev-data/.github/issues)
- [Discussions](https://github.com/orgs/open-ev-data/discussions)
- [Documentation Home](../index.md)

