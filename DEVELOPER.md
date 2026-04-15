# DEVELOPER.md

This document provides instructions for setting up your development environment
and contributing to the Dataproc Agent skills project.

## Prerequisites

Before you begin, ensure you have the following:

1.  **Gemini CLI:** Install the Gemini CLI version v0.6.0 or above.
2.  **Dataproc Resources:** Access to active Dataproc clusters and jobs for testing.

## Developing the Extension

### Running from Local Source

1.  **Clone the Repository:**

    ```bash
    git clone https://github.com/gemini-cli-extensions/dataproc.git
    cd dataproc
    ```

2.  **Install the Extension Locally:**

    ```bash
    gemini extensions install .
    ```

3.  **Testing Changes:** After installation, start the Gemini CLI (`gemini`).
    You can now interact with the `dataproc` skills to manually test your changes.

## Testing

### Automated Presubmit Checks

A GitHub Actions workflow (`.github/workflows/presubmit-tests.yml`) is triggered
for every pull request. This workflow primarily verifies that the extension can
be successfully installed by the Gemini CLI.

The skills themselves are validated using the `skills-validate.yml` workflow.

### Other GitHub Checks

*   **License Header Check:** A workflow ensures all necessary files contain the
    proper license header.
*   **Conventional Commits:** This repository uses
    [Release Please](https://github.com/googleapis/release-please) to manage
    releases. Your commit messages must adhere to the
    [Conventional Commits](https://www.conventionalcommits.org/) specification.

## Maintainer Information

### Releasing

The release process is automated using `release-please`. Merging a Release PR
will create a new GitHub tag and release.
