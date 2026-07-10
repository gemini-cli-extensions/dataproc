# Dataproc Agent Skills

> [!NOTE]
> Currently in beta (pre-v1.0), and may see breaking changes until the first stable release (v1.0).

This repository provides a set of agent skills to interact with [Dataproc](https://cloud.google.com/dataproc) clusters and jobs. These skills can be used with various AI agents, including [Antigravity](https://antigravity.google/), [Claude Code](https://claude.com/product/claude-code) and [Codex](https://developers.openai.com/codex), to manage your clusters, monitor jobs, and troubleshoot issues using natural language prompts.

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
    - [Antigravity](#antigravity)
    - [Claude Code](#claude-code)
    - [Codex](#codex)
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
  - Antigravity
     - [Antigravity CLI](https://github.com/google-gemini/gemini-cli) version **v1.6.0** or higher
     - [Antigravity 2.0](https://antigravity.google/product/antigravity-2) version **v2.0.0** or higher.
  - [Claude Code](https://claude.com/product/claude-code) version **v2.1.94** or higher.
  - [Codex](https://developers.openai.com/codex) **v0.117.0** or higher.
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
<summary id="antigravity">Antigravity</summary>

You can use either of these two agents for Antigravity:
- [Antigravity CLI](https://github.com/google-gemini/gemini-cli) version **v1.6.0** or higher
- [Antigravity 2.0](https://antigravity.google/product/antigravity-2) version **v2.0.0** or higher.

<blockquote>
💡 <strong>Tip — Migrating from Gemini CLI?</strong><br>
If you previously installed this extension with <code>gemini extensions install</code>, you can convert it to an Antigravity plugin instead of reinstalling from scratch:
<ul>
  <li><strong>On first launch of Antigravity CLI</strong>, accept the Migration Options prompt to automatically convert your installed Gemini CLI extensions to Antigravity plugins.</li>
  <li><strong>Or, from your terminal</strong>, run:
    <pre><code class="language-bash">agy plugin import gemini</code></pre>
  </li>
</ul>
See <a href="https://antigravity.google/docs/gcli-migration">Migrating from Gemini CLI</a> for details on plugins, context files (<code>GEMINI.md</code> / <code>AGENTS.md</code>), and MCP server config differences.
</blockquote>

#### Antigravity 2.0 (IDE)

**1. Clone the Repo:**

```bash
git clone --branch 0.1.0 https://github.com/gemini-cli-extensions/dataproc.git
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

_(Tip: Antigravity 2.0 automatically discovers skills in these directories at the start of a session. You can verify they are active by running the `/skills` command in your active session.)_

#### Antigravity CLI

You can install plugins directly from a remote GitHub repository.

**1. Install the plugin:**

```bash
agy plugin install https://github.com/gemini-cli-extensions/dataproc
```

**2. Set env vars:**
Set your environment vars as described in the [configuration section](#configuration).

</details>

<details>
<summary id="claude-code">Claude Code</summary>

**1. Set env vars:**
In your terminal, set your environment vars as described in the [configuration section](#configuration).

**2. Start the agent:**

```bash
claude
```

**3. Install the plugin:**

```bash
/plugin install dataproc@claude-plugins-official
```

</details>

<details>
<summary id="codex">Codex</summary>

**1. Install marketplace:**

```bash
codex plugin marketplace add GoogleCloudPlatform/data-agent-kit
```

**2. Install the plugin:**

```bash
codex plugin add dataproc@data-agent-kit
```

**3. Set env vars:**
Enter your environment vars as described in the [configuration section](#configuration).

**4. (Optional) Update the marketplace:**
```sh
codex plugin marketplace upgrade data-agent-kit
```

</details>

## Installing using [open agent skills tool](https://github.com/vercel-labs/skills)

You can install skills using the `npx skills` command.

**1. Install the skills:**

Run the following command in your terminal to automatically download and register the skills:

```bash
npx skills add https://github.com/gemini-cli-extensions/dataproc/tree/0.1.0
```

For detailed info check out the [Skills npm package](https://www.npmjs.com/package/skills).

**2. Set env vars:**
Set your environment vars as described in the [configuration section](#configuration).

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
