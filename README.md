# gologic-workflows
A bunch of reusable github workflows

## Available Workflows

This repository contains reusable GitHub Actions workflows for common build systems:

### Maven Build

**File:** `.github/workflows/maven-build.yml`

Builds a Maven project without running tests.

**Usage:**
```yaml
jobs:
  build:
    uses: gologic-ca/gologic-workflows/.github/workflows/maven-build.yml@main
    with:
      java-version: '17'           # Optional, default: '17'
      java-distribution: 'temurin' # Optional, default: 'temurin'
      maven-version: '3.9.6'       # Optional, default: '3.9.6'
      working-directory: '.'       # Optional, default: '.'
      maven-args: ''               # Optional, additional Maven arguments
```

### Maven Unit Tests

**File:** `.github/workflows/maven-test.yml`

Runs unit tests for a Maven project.

**Usage:**
```yaml
jobs:
  test:
    uses: gologic-ca/gologic-workflows/.github/workflows/maven-test.yml@main
    with:
      java-version: '17'           # Optional, default: '17'
      java-distribution: 'temurin' # Optional, default: 'temurin'
      maven-version: '3.9.6'       # Optional, default: '3.9.6'
      working-directory: '.'       # Optional, default: '.'
      maven-args: ''               # Optional, additional Maven arguments
```

### Gradle Build

**File:** `.github/workflows/gradle-build.yml`

Builds a Gradle project without running tests.

**Usage:**
```yaml
jobs:
  build:
    uses: gologic-ca/gologic-workflows/.github/workflows/gradle-build.yml@main
    with:
      java-version: '17'           # Optional, default: '17'
      java-distribution: 'temurin' # Optional, default: 'temurin'
      gradle-version: ''           # Optional, leave empty to use wrapper
      working-directory: '.'       # Optional, default: '.'
      gradle-args: ''              # Optional, additional Gradle arguments
```

### Poetry Build

**File:** `.github/workflows/poetry-build.yml`

Builds a Python project using Poetry.

**Usage:**
```yaml
jobs:
  build:
    uses: gologic-ca/gologic-workflows/.github/workflows/poetry-build.yml@main
    with:
      python-version: '3.11'       # Optional, default: '3.11'
      poetry-version: '1.7.1'      # Optional, default: '1.7.1'
      working-directory: '.'       # Optional, default: '.'
      poetry-install-args: ''      # Optional, additional install arguments
      poetry-build-args: ''        # Optional, additional build arguments
```

## Features

- **Flexible Configuration:** All workflows support customizable versions and additional arguments
- **Caching:** Intelligent caching for dependencies to speed up builds
- **Artifact Upload:** Build artifacts are automatically uploaded for later use
- **Working Directory Support:** Run builds from any subdirectory in your repository
