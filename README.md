# Dataproc Agent Skills

> [!NOTE]
> Currently in beta (pre-v1.0), and may see breaking changes until the first stable release (v1.0).

This repository provides a set of agent skills to interact with [Dataproc](https://cloud.google.com/dataproc) clusters and jobs. These skills can be used with various AI agents, including [Gemini CLI](https://google-gemini.github.io/gemini-cli/), Claude Code, and Codex, to manage your clusters, monitor jobs, and troubleshoot issues using natural language prompts.

> [!IMPORTANT]
> **We Want Your Feedback!**
> Please share your thoughts with us by filling out our feedback [form][form].
> Your input is invaluable and helps us improve the project for everyone.

[form]: https://docs.google.com/forms/d/e/1FAIpQLSfEGmLR46iipyNTgwTmIDJqzkAwDPXxbocpXpUbHXydiN1RTw/viewform?usp=pp_url&entry.157487=dataproc

## Table of Contents

- [Why Use Dataproc Agent Skills?](#why-use-dataproc-agent-skills)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
  - [Configuration](#configuration)
  - [Installation & Usage](#installation--usage)
    - [Gemini CLI](#gemini-cli)
    - [Claude Code](#claude-code)
    - [Codex](#codex)
    - [Antigravity](#antigravity)
- [Usage Examples](#usage-examples)
- [Supported Skills](#supported-skills)
- [Troubleshooting](#troubleshooting)

## Why Use Dataproc Agent Skills?

- **Seamless Workflow:** Integrates seamlessly into your AI agent's environment. No need to constantly switch contexts for common Dataproc tasks.
- **Natural Language Queries:** Stop wrestling with complex gcloud commands. Manage your clusters and jobs by describing what you want in plain English.
- **Full Lifecycle Control:** Manage the entire lifecycle of your Dataproc resources, from listing clusters to checking job statuses.

## Prerequisites

Before you begin, ensure you have the following:

- One of these AI agents installed
  - [Gemini CLI](https://github.com/google-gemini/gemini-cli) version **v0.6.0** or higher
  - [Claude Code](https://claude.com/product/claude-code) version **v2.1.94** or higher
  - [Codex](https://developers.openai.com/codex) **v0.117.0** or higher
  - [Antigravity](https://antigravity.google) **v1.14.2** or higher
- A Google Cloud project with the **Dataproc API** enabled.
- Ensure [Application Default Credentials](https://cloud.google.com/docs/authentication/gcloud) are available in your environment.
- IAM Permissions:
  - Dataproc Viewer (`roles/dataproc.viewer`) or Dataproc Editor (`roles/dataproc.editor`)

## Getting Started

### Configuration

Please keep these env vars handy during the installation process:

- `DATAPROC_PROJECT`: The GCP project ID.
- `DATAPROC_REGION`: The region of your Dataproc resources.

> [!NOTE]
>
> - Ensure [Application Default Credentials](https://cloud.google.com/docs/authentication/gcloud) are available in your environment.
> - If your Cloud SQL for PostgreSQL instance uses private IPs, you must run your agent in the same Virtual Private Cloud (VPC) network.


### Installation & Usage

To start interacting with Dataproc, install the skills for your preferred AI agent, then launch the agent and use natural language to ask questions or perform tasks.

For the latest version, check the [releases page][releases].

[releases]: https://github.com/gemini-cli-extensions/dataproc/releases

<!-- {x-release-please-start-version} -->

<details open>
<summary id="gemini-cli">Gemini CLI</summary>

**1. Install the extension:**

```bash
gemini extensions install https://github.com/gemini-cli-extensions/dataproc
```

During the installation, enter your environment vars as described in the [configuration section](#configuration).

**2. (Optional) Manage Configuration:**
To view or update your configuration in Gemini CLI:

- Terminal: `gemini extensions config dataproc [setting name] [--scope <scope>]`
- Gemini CLI: `/extensions list`

**3. Start the agent:**

```bash
gemini
```

_(Tip: Run `/extensions list` to verify your configuration and active extensions.)_

> [!WARNING]
> **Changing Instance & Database Connections**
> Currently, the database connection must be configured before starting the agent and can not be changed during a session.
> To save and resume conversation history in Gemini CLI use command: `/chat save <tag>` and `/chat resume <tag>`.

</details>

<details>
<summary id="claude-code">Claude Code</summary>

**1. Set env vars:**
In your terminal, set your environment vars as described in the [configuration section](#configuration).

**2. Start the agent:**

```bash
claude
```

**3. Add the marketplace:**

```bash
/plugin marketplace add https://github.com/gemini-cli-extensions/dataproc.git#0.0.0
```

**4. Install the plugin:**

```bash
/plugin install dataproc@dataproc-marketplace
```

</details>

<details>
<summary id="codex">Codex</summary>

**1. Clone the Repo:**

```bash
git clone --branch 0.0.0 git@github.com:gemini-cli-extensions/dataproc.git
```

**2. Install the plugin:**

```bash
mkdir -p ~/.codex/plugins
cp -R /absolute/path/to/dataproc ~/.codex/plugins/dataproc
```

**3. Set env vars:**
Enter your environment vars as described in the [configuration section](#configuration).

**4. Create or update marketplace.json:**
`~/.agents/plugins/marketplace.json`

```json
{
  "name": "my-data-cloud-google-marketplace",
  "interface": {
    "displayName": "Google Data Cloud Skills"
  },
  "plugins": [
    {
      "name": "dataproc",
      "source": {
        "source": "local",
        "path": "./plugins/dataproc"
      },
      "policy": {
        "installation": "AVAILABLE",
        "authentication": "ON_INSTALL"
      },
      "category": "Data & Analytics"
    }
  ]
}
```

</details>

<details>
<summary id="antigravity">Antigravity</summary>

**1. Clone the Repo:**

```bash
git clone --branch 0.0.0 https://github.com/gemini-cli-extensions/dataproc.git
```

**2. Install the skills:**

Choose a location for the skills:
- **Global (all workspaces):** `~/.gemini/antigravity/skills/`
- **Workspace-specific:** `<workspace-root>/.agents/skills/`

Copy the skill folders from the cloned repository's `skills/` directory to your chosen location:

```bash
cp -R dataproc/skills/* ~/.gemini/antigravity/skills/
```

**3. Set env vars:**
Set your environment vars as described in the [configuration section](#configuration).

</details>

<!-- {x-release-please-end} -->

## Usage Examples

Interact with Dataproc using natural language:

- **List Clusters:**
  - "List all my Dataproc clusters in us-central1."
- **Check Jobs:**
  - "Show me the status of the job with ID 'my-spark-job-123'."
  - "List all failed jobs in my project."
- **Get Details:**
  - "Get details for the cluster named 'my-cluster'."

## Supported Skills

The following skills are available in this repository:

- [Dataproc Skills](./skills/dataproc-skills/SKILL.md) - Skills to interact with your Dataproc clusters and jobs.

## Troubleshooting

Use the debug mode of your agent (e.g., `gemini --debug`) to enable debugging.

Common issues:

- "failed to find default credentials": Ensure [Application Default Credentials](https://cloud.google.com/docs/authentication/gcloud) are available in your environment.
- "cannot execute binary file": The Toolbox binary did not download correctly.
