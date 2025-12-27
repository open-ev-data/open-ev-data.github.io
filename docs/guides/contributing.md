---
title: Contributing to OpenEV Data
---

# Contributing Guide

Thank you for your interest in contributing to OpenEV Data! This project aims to be the single source of truth for electric vehicle specifications, and we welcome contributions from EV enthusiasts, engineers, researchers, and manufacturers worldwide.

!!! info "Community Project"
    OpenEV Data is a community-driven project. Every contribution, no matter how small, helps make the database more accurate and comprehensive.

## Quick Links

- [Code of Conduct](../governance/CODE_OF_CONDUCT.md)
- [Project Setup](../governance/GET_STARTED.md)
- [API Documentation](../api/index.md)
- [Dataset Documentation](../dataset/index.md)

## Ways to Contribute

=== "Add Vehicle Data"

    **Best for**: EV owners, enthusiasts, researchers
    
    Help expand the database by adding specifications for new EVs:
    
    1. Read the [Dataset Documentation](../dataset/index.md)
    2. Gather reliable sources
    3. Follow the schema structure
    4. Submit a pull request
    
    **Requirements**:
    - Minimum 2 reliable sources per specification
    - International coverage (USA, EU, China, Japan, Brazil)
    - Complete specifications (battery, range, charging)

=== "Correct Data"

    **Best for**: Detail-oriented contributors
    
    Help maintain accuracy by correcting errors:
    
    1. Open an issue with the data correction template
    2. Provide reliable sources for corrections
    3. Specify which fields are incorrect
    4. Submit a pull request with fixes
    
    **Requirements**:
    - Official sources preferred
    - Clear documentation of changes
    - Multiple sources for verification

=== "Improve Code"

    **Best for**: Developers
    
    Enhance the API, ETL pipeline, or tooling:
    
    1. Check [open issues](https://github.com/open-ev-data/open-ev-data-api/issues)
    2. Read the [API Architecture](../api/ARCHITECTURE.md)
    3. Follow [Rust Guidelines](../api/RUST_GUIDELINES.md)
    4. Submit a pull request
    
    **Requirements**:
    - Rust 1.80+
    - Tests for new features
    - Documentation for public APIs

=== "Write Documentation"

    **Best for**: Technical writers
    
    Improve guides, tutorials, and documentation:
    
    1. Check for gaps or unclear sections
    2. Fork the documentation repository
    3. Make improvements
    4. Submit a pull request
    
    **Requirements**:
    - Clear, concise writing
    - Follow DRY principles
    - Test all code examples

## Getting Started

### 1. Read the Documentation

Before contributing, familiarize yourself with:

- [Project Setup](../governance/GET_STARTED.md)
- [API Architecture](../api/ARCHITECTURE.md)
- [Dataset Schema](../dataset/SCHEMA.md)
- [Contributing Guidelines](../governance/CONTRIBUTING.md)

### 2. Set Up Your Environment

Follow the [Project Setup Guide](../governance/GET_STARTED.md), [API Getting Started](../api/GET_STARTED.md) or [Dataset Documentation](../dataset/index.md) guide to configure your local environment.

### 3. Find Something to Work On

**Good first issues**:

- Adding missing vehicle data
- Correcting inaccurate specifications
- Improving documentation
- Writing tests

Browse issues with the `good-first-issue` label:

- [Dataset Issues](https://github.com/open-ev-data/open-ev-data-dataset/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22)
- [API Issues](https://github.com/open-ev-data/open-ev-data-api/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22)

### 4. Make Your Changes

Follow the specific guides:

- [Dataset Documentation](../dataset/index.md)
- [API Documentation](../api/index.md)
- [Rust Guidelines](../api/RUST_GUIDELINES.md)

### 5. Submit a Pull Request

See [Pull Request Process](#pull-request-process) below.

## Pull Request Process

### Before Submitting

- [ ] Fork the repository
- [ ] Create a feature branch: `git checkout -b feature/your-feature`
- [ ] Make your changes
- [ ] Test thoroughly
- [ ] Commit with clear messages
- [ ] Push to your fork

### Commit Message Format

Follow conventional commit format:

```
<type>: <description>

[optional body]

[optional footer]
```

**Types**:

- `Add`: New feature or data
- `Fix`: Bug fix or data correction
- `Update`: Modification to existing feature/data
- `Remove`: Deletion of feature or data
- `Docs`: Documentation changes
- `Refactor`: Code refactoring
- `Test`: Test additions or modifications
- `Chore`: Maintenance tasks

**Examples**:

```
Add: Tesla Model 3 2024 specifications

Added complete specifications for Tesla Model 3 2024 including:
- Battery specifications
- Charging capabilities
- Range data (WLTP and EPA)
- Performance metrics

Sources: Tesla.com, EPA certification
```

```
Fix: Correct BYD Seal DC charging power

Changed max DC power from 120kW to 150kW based on official
specifications from BYD.

Fixes #123
```

### Submitting the PR

1. Go to the original repository
2. Click "New Pull Request"
3. Select your branch
4. Fill out the pull request template
5. Link related issues
6. Wait for review

### Review Process

- Maintainers review within 7 days
- Address feedback promptly
- Keep discussions focused and professional
- Be open to suggestions

### After Approval

- Squash commits if requested
- Maintainers will merge
- Your contribution is included in the next release

## Style Guidelines

### General

- Use English for all content
- Follow SOLID principles
- Apply DRY principles
- Avoid unnecessary comments
- No emojis in code or data

### JSON Formatting

```json
{
  "schema_version": "1.0.0",
  "make": {
    "slug": "tesla",
    "name": "Tesla"
  },
  "model": {
    "slug": "model_3",
    "name": "Model 3"
  }
}
```

**Rules**:

- 2-space indentation
- Double quotes for strings
- Trailing commas in arrays/objects
- Sort keys alphabetically where logical

### Rust Code

```rust
pub struct Vehicle {
    pub make: String,
    pub model: String,
    pub year: u16,
}

impl Vehicle {
    pub fn new(make: String, model: String, year: u16) -> Self {
        Self { make, model, year }
    }
}
```

**Rules**:

- Follow Rust naming conventions
- Use `cargo fmt` default configuration
- Maximum line length: 100 characters
- Use Result types for error handling
- Document public APIs with rustdoc

### Documentation

```markdown
# Title

Brief introduction paragraph.

## Section

Content with examples:

    ```python
    import openev
    
    vehicle = openev.get_vehicle("tesla", "model_3", 2024)
    ```

See [Related Guide](./related.md) for details.
```

**Rules**:

- Use clear, concise language
- Include code examples
- Test all commands
- Link to related documentation
- Use frontmatter for metadata

## Data Quality Standards

### Source Requirements

**Required**:

- Minimum 2 reliable sources per specification
- Official manufacturer specifications preferred
- Regulatory certifications (EPA, WLTP) when available

**Source Hierarchy**:

1. Official manufacturer specifications
2. Regulatory certifications
3. Professional automotive publications
4. Verified user testing data

**Avoid**:

- Unverified forums or social media
- Estimations without methodology
- Outdated sources

### Completeness

Each vehicle entry should include:

- Battery specifications
- Range data (multiple test cycles)
- Charging specifications (AC and DC)
- Performance metrics
- Physical dimensions
- Market availability

### International Coverage

Include sources from:

- USA
- Brazil
- EU (Portugal, Germany, France, Italy, UK)
- China
- Japan

### Accuracy

- Verify all specifications
- Document assumptions clearly
- Update when new information available
- Note regional variations

Read the complete [Data Quality Standards](../governance/CONTRIBUTING.md) guide.

## Community Guidelines

### Code of Conduct

We are committed to providing a welcoming and inclusive environment. Read our [Code of Conduct](../governance/CODE_OF_CONDUCT.md).

### Communication

- Be respectful and professional
- Provide constructive feedback
- Ask questions when unclear
- Share knowledge generously

### Best Practices

- Search existing issues before creating new ones
- Use appropriate issue templates
- Provide detailed reproduction steps for bugs
- Include relevant context in discussions

## Recognition

Contributors are recognized:

- In the contributors list
- In release notes
- In the dataset metadata

## License

By contributing, you agree that your contributions will be licensed under:

- **Dataset**: CDLA-Permissive-2.0
- **API/Code**: Apache License 2.0
- **Documentation**: CC-BY 4.0

See [License Information](../governance/index.md) for details.

## Get Help

Need assistance?

- [GitHub Issues](https://github.com/open-ev-data/.github/issues)
- [GitHub Discussions](https://github.com/orgs/open-ev-data/discussions)
- [Documentation](../index.md)

## Next Steps

<div class="grid cards" markdown>

-   [**Project Setup**](../governance/GET_STARTED.md)
    
    Complete development environment setup

-   [**API Documentation**](../api/index.md)
    
    Learn about the API

-   [**Dataset Documentation**](../dataset/index.md)
    
    Understand the dataset structure

-   [**Code of Conduct**](../governance/CODE_OF_CONDUCT.md)
    
    Community standards

</div>

---

Thank you for helping make OpenEV Data the most accurate and comprehensive EV specification database!

