# Building the Customer Support AI Project — A Beginner's Story

> **What this guide is based on:** the lecture transcript. The transcript's automatic captions contain a few misspelled technical words, so obvious command names are written in their usual form (for e[...)

## The story: we're opening a workshop

Imagine we're opening a small software workshop. Our goal is to build an **autonomous customer-support resolution platform**: a support assistant that can understand a customer's issue, classify it, i[...)

Before building the assistant, we need to prepare our workshop:

1. Create a project folder.
2. Open it in a code editor.
3. create a GitHub repository so our work has a remote home.
4. Prepare Python and its project dependencies.
5. Track our work with Git.
6. Keep the project organized and document how to run it.
7. Use separate Git branches so unfinished work does not accidentally land in `main`.
8. Use project guidance files with an AI coding assistant to help plan and create the project structure.

---

## Chapter 1 — Create the workshop folder

### Step 1: Make a folder

Create a folder for the project. The lecturer used a name like `clouddesk`/`Cloudus`; use one name consistently on your own machine.

Example folder structure will grow over time:

```text
clouddesk/
```

### Step 2: Open the folder in your editor

The lecturer mentions Cursor, Visual Studio Code, and other coding environments. Use whichever one you have access to.

From a terminal opened **inside the project folder**, you may be able to open the editor with:

```bash
cursor .
```

For Visual Studio Code, the equivalent is:

```bash
code .
```

- `.` means “the current folder.”
- These commands work only if the editor's command-line launcher is installed and available on your PATH. If not, open the folder through the editor's File menu.

**Story version:** We have rented an empty workshop and opened its door. Now we need a notebook to record our work and tools to build the product.

---

## Chapter 2 — Give the project a home on GitHub

GitHub is the online home for a copy of our project. Git is the tool that records changes to files.

### Step 1: Create a repository on GitHub

1. Sign in to GitHub.
2. Click the **+** menu and choose **New repository**.
3. Give it a name, for example `clouddesk`.
4. Create the repository.

The lecture says that a description is optional for this initial setup.

### Step 2: Open a terminal

The lecturer recommends Git Bash for Git commands on Windows. macOS and Linux users can normally use their terminal. The integrated terminal in Cursor or VS Code is also fine, as long as Git is instal[...]

### A small vocabulary lesson

| Word | Simple meaning |
|---|---|
| **Working folder** | The files you're currently editing. |
| **Local repository** | The project and its Git history on your computer. |
| **Remote / `origin`** | The online repository, usually on GitHub. |
| **Commit** | A saved checkpoint in the project's history. |
| **Branch** | A separate line of work. |
| **Push** | Send local commits to the remote repository. |
| **Pull** | Bring remote changes into your local branch. |
| **Pull request (PR)** | A request to review and merge one branch into another. |

---

## Chapter 3 — Set up Python with `uv`

The lecture chooses **uv** as the Python project/package manager. It can create project files, manage dependencies, and create virtual environments. It also caches downloaded packages, so it can often[...]

Think of `uv` as the workshop's supply manager.

### Step 1: Install `uv` if you don't already have it

The transcript mentions installing it with pip:

```bash
python -m pip install uv
```

This is one option. Follow the current official uv installation instructions if you prefer its platform-specific installer. After installing, check that the command is available:

```bash
uv --version
```

If the terminal says `uv` is not recognized or not found, close and reopen the terminal and check the installation/PATH.

### Step 2: Initialize the project

From the project folder, run:

```bash
uv init
```

**What it does:** creates starter files for a Python project. Depending on the uv version and options, these may include `pyproject.toml`, a Python source file, and `.gitignore`.

**Story version:** We have the workshop, so `uv init` creates the project registration papers.

### Step 3: Understand the important files

| File/folder | What it is for |
|---|---|
| `pyproject.toml` | Project details and dependency declarations. |
| `.gitignore` | Tells Git which files/folders not to track. |
| `README.md` | Human-friendly explanation of the project and how to run it. |
| `.venv/` | The project's isolated Python environment, created in a later step. |
| `src/` or a starter `.py` file | Place for Python source code; the exact layout depends on how the project was initialized. |

The transcript sometimes captions `pyproject.toml` as “project dot qml.” The intended Python project file is **`pyproject.toml`**.

### Step 4: Create a virtual environment

Run:

```bash
uv venv
```

This normally creates a `.venv` folder.

**What is a virtual environment?** Imagine each project has its own toolbox. The customer-support project can use the versions of libraries it needs without mixing them with other projects on your com[...]

### Step 5: Activate the environment (optional when using uv commands)

On **Windows PowerShell**:

```powershell
.\.venv\Scripts\Activate.ps1
```

On **Windows Command Prompt**:

```bat
.venv\Scripts\activate.bat
```

On **macOS/Linux**:

```bash
source .venv/bin/activate
```

When you're finished working in the virtual environment, deactivate it with:

```bash
deactivate
```

The transcript's spoken activation command was not fully clear, so use the command for your actual terminal. You can also use `uv run ...` for many commands without manually activating the environment[...]

### Step 6: Add a library

The lecturer demonstrates adding LangChain. The caption spells the name incorrectly as “Langstain”; the likely intended package is `langchain`.

```bash
uv add langchain
```

**What it does:** installs the package for the project and records the dependency in `pyproject.toml` (and updates the lock file when applicable).

You should see the dependency listed in `pyproject.toml`. Later, other libraries can be added using the same pattern:

```bash
uv add package-name
```

Replace `package-name` with the real package you need. Don't install libraries just because they appear in an example; add only the ones your project uses.

### A note about `uv` and `pip`

The lecture explains that uv is fast partly because it uses a cache and efficient dependency management. A useful nuance: **pip also has a cache**, so it is not accurate to say pip downloads every pac[...]

---

## Chapter 4 — Write a README so another person can use the project

A project should not be a mysterious box that only its creator understands.

Create or edit `README.md`. The lecture says it should explain:

- The project name.
- What the project does.
- The major components or tools used.
- How to install/setup it.
- How to run it locally.
- Any important project notes.

Update it as the project grows. A recruiter or teammate should be able to open the repository and understand what it does without asking you to explain every detail.

---

## Chapter 5 — Teach Git to save checkpoints

Git lets us save meaningful checkpoints and share them with GitHub.

> **Important:** The transcript's early setup steps mix `uv init` with Git initialization. They are different tools: `uv init` initializes a Python project; `git init` initializes Git in a folder. If [...]

### Step 1: Initialize Git if needed

```bash
git init
```

### Step 2: Check what Git sees

```bash
git status
```

This lists changed, untracked, and staged files.

### Step 3: Stage files

To stage only the README:

```bash
git add README.md
```

To stage all changes in the current directory, except those ignored by `.gitignore`:

```bash
git add .
```

**Staging** is like putting the files you want into a box before sealing a checkpoint.

### Step 4: Commit the staged changes

```bash
git commit -m "Initial project setup"
```

- `commit` saves a checkpoint.
- `-m` supplies a short message describing it.

If Git asks you to configure your name/email, use your own Git identity. Do not copy someone else's identity.

### Step 5: Use `main` as the branch name (if needed)

```bash
git branch -M main
```

This renames the current branch to `main`. If your branch is already named `main`, there may be nothing to change.

### Step 6: Connect the local repository to GitHub

Copy the repository's URL from your own GitHub page, then run:

```bash
git remote add origin <YOUR_GITHUB_REPOSITORY_URL>
```

Replace `<YOUR_GITHUB_REPOSITORY_URL>` with your real repository URL. Do not type the angle-bracket placeholder literally.

If `origin` already exists, don't repeat this command blindly. Check it with:

```bash
git remote -v
```

### Step 7: Push the first commit

```bash
git push -u origin main
```

This sends the local `main` branch to GitHub and sets its upstream, so later pushes are easier.

**Story version:** `git add` packs the files, `git commit` seals a checkpoint, and `git push` sends that checkpoint to the online workshop.

---

## Chapter 6 — Keep `main` safe with branches

The lecture emphasizes that the team should not do day-to-day development directly on `main`. It introduces branches such as `development` and `testing`, with new feature branches created from `develo[...]

A simple way to picture it:

- `main` is the stable version.
- `development` is where work is brought together for the next version.
- `feature/...` branches are separate workbenches for individual tasks.
- A pull request asks the team to review work before merging it.

### Useful branch commands

See the branches:

```bash
git branch
```

Switch to an existing branch:

```bash
git switch development
```

Create a new branch and switch to it:

```bash
git switch -c feature/customer-intake
```

Push a new branch to GitHub and set its upstream:

```bash
git push -u origin feature/customer-intake
```

The transcript demonstrates creating a `testing` branch from `main`:

```bash
git switch main
git switch -c testing
git push -u origin testing
```

Use the branch names your team actually agreed on. A branch must exist locally before `git switch <branch>` can switch to it.

### Before starting work each day, pull the latest changes

The lecturer demonstrates pulling from `origin` while on the `development` branch:

```bash
git switch development
git pull origin development
```

**What it means:** “Bring the latest `development` branch from GitHub into my local `development` branch.”

Pulling is a good habit before starting work, but if you have local changes, check `git status` first and resolve any conflicts if Git reports them.

### Typical feature-branch workflow

```bash
# 1. Go to development and update it
git switch development
git pull origin development

# 2. Create a branch for your task
git switch -c feature/short-description

# 3. Edit files, then inspect your changes
git status
git diff

# 4. Stage and commit the changes
git add .
git commit -m "Describe the feature"

# 5. Push your feature branch
git push -u origin feature/short-description
```

Then open GitHub and create a pull request **from your feature branch into the team's agreed target branch** (the lecture describes feature work being reviewed into `development`). A push sends commit[...]

Do not merge into `main` just because GitHub displays a “Compare & pull request” button. Check the source and target branches first.

---

## Chapter 7 — Keep unnecessary and private files out of GitHub

The lecture highlights `.gitignore`. It keeps generated files and local-only files out of the repository.

Common examples include:

- `.venv/` — your local virtual environment.
- `.env` — often contains secrets or local configuration.
- `__pycache__/` and `*.pyc` — Python-generated cache files.
- Build artifacts and temporary files.

A simple `.gitignore` could look like this:

```gitignore
# Python virtual environment
.venv/

# Python cache
__pycache__/
*.py[cod]

# Local secrets/configuration
.env
.env.*

# Common local editor files
.vscode/
```

**Caution:** only add `.env.*` if you intend to ignore every file matching that pattern. If your project deliberately tracks a safe example file such as `.env.example`, add an exception:

```gitignore
!.env.example
```

Never commit API keys, passwords, access tokens, or other secrets. If a secret was already committed, adding it to `.gitignore` does not erase it from Git history; rotate the secret and follow your te[...]

The lecture's rule is: **check `.gitignore` before staging and pushing code.**

---

## Chapter 8 — Give the AI coding assistant project instructions

Later in the lecture, the instructor discusses using a project guide called `cloud.md` and asking an AI coding assistant to create supporting files and folders. The exact prompt and all generated cont[...]

The idea is to give the assistant one clear source of truth describing:

- What the application should do.
- Its architecture and request flow.
- The agents/services and their responsibilities.
- API endpoints and data expectations.
- Safety rules and boundaries.
- Repository/project organization.

The lecturer also mentions files such as:

| File | Intended role in the workflow |
|---|---|
| `cloud.md` | Main project brief or source of project requirements (as named in the transcript). |
| `memory.md` | Notes/context the AI workflow should preserve. |
| `task.md` | A task list or description of the work to do. |
| `plan.md` / phase-planning files | Break the work into steps or phases. |
| `docs/` | A place for supporting documentation, including a Git workflow guide. |
| `architecture.md` | A description or diagram of the system architecture. |

These are the names mentioned or suggested by the transcript; the transcript does not fully specify the contents of every file. Follow the actual files supplied by your instructor if their names or sp[...]

### Example of the kind of request being made

This is a **simplified example**, not a verbatim transcript prompt:

```text
Read the project's cloud.md requirements.
Summarize the application goals and architecture.
Create a clear project plan and supporting documentation files.
Do not invent requirements that are not in cloud.md.
List any missing information instead of guessing.
```

The lecturer demonstrates referencing a file directly in the coding assistant rather than copying the whole document into the chat. The exact syntax depends on the editor/assistant, so use its file-re[...]

### Using Claude Code in VS Code

If you want to use Claude Code from inside VS Code, follow these steps:

1. Open VS Code.
2. In the lower-left corner of the window, click the **Accounts** icon.
3. Select your GitHub account or sign in to GitHub if prompted.
4. Open the Command Palette with **Ctrl+Shift+P** on Windows/Linux or **Cmd+Shift+P** on macOS.
5. Type **Claude Code** in the Command Palette.
6. Choose the command to open the Claude Code panel or chat window, such as **Claude Code: Open Panel** or **Claude Code: Open Chat**. The exact option name can vary by extension version.
7. If you do not see the command, install the Claude Code extension from the VS Code Extensions view and sign in again.

**Story version:** `cloud.md` is the architect's blueprint. The AI assistant can help turn that blueprint into a plan and supporting documents, but the team still needs to review the generated work.

---

## Chapter 9 — What are we actually building?

The project goal from the lecture is an **autonomous customer-support resolution platform**.

The intended flow, as described in the transcript, is broadly:

1. Understand the user's requirement.
2. Classify the issue.
3. Investigate and retrieve relevant information.
4. Troubleshoot the problem.
5. Resolve it or take the appropriate action.
6. Escalate finance-related issues when needed.
7. Remember conversations associated with a particular user.

The lecture refers to a “CACD pipeline,” but the acronym is not clearly explained in the captured transcript. Do not assume what it stands for without checking the instructor's project documents.

At this point, the lecture mainly sets up the project, Python environment, GitHub workflow, and AI project guidance. The transcript does **not** provide enough clear, complete code to document the fin[...]

---

## Quick command cheat sheet

Run commands from the appropriate terminal and project directory.

| Goal | Command | Plain-English meaning |
|---|---|---|
| Open current folder in Cursor | `cursor .` | Open this folder in Cursor. |
| Open current folder in VS Code | `code .` | Open this folder in VS Code. |
| Check uv installation | `uv --version` | Show the installed uv version. |
| Start a Python project | `uv init` | Create starter project files. |
| Create a virtual environment | `uv venv` | Create the project's isolated Python environment. |
| Add a dependency | `uv add langchain` | Add LangChain to the project. |
| Initialize Git if needed | `git init` | Start Git tracking in this folder. |
| Check file/branch state | `git status` | Show current changes. |
| Stage one file | `git add README.md` | Prepare the README for a commit. |
| Stage all non-ignored changes | `git add .` | Prepare current-folder changes. |
| Save a checkpoint | `git commit -m "Initial setup"` | Record a commit. |
| Rename current branch | `git branch -M main` | Rename it to `main`. |
| Show remote URLs | `git remote -v` | See which remote repositories are configured. |
| Connect GitHub remote | `git remote add origin <URL>` | Set the online repository address. |
| Push main for the first time | `git push -u origin main` | Upload main and set its upstream. |
| List local branches | `git branch` | Show local branch names. |
| Switch branches | `git switch development` | Move to the development branch. |
| Create and switch to a branch | `git switch -c feature/my-task` | Start a new task branch. |
| Download branch updates | `git pull origin development` | Update local development from GitHub. |
| Push a feature branch | `git push -u origin feature/my-task` | Upload the feature branch. |

---

## The whole journey in one picture

```text
Create project folder
        |
        v
Open folder in Cursor / VS Code
        |
        v
Create GitHub repository
        |
        v
uv init  --->  pyproject.toml and starter files
        |
        v
uv venv  --->  isolated Python environment
        |
        v
uv add langchain  --->  add project dependency
        |
        v
Write README.md and check .gitignore
        |
        v
git add  --->  git commit  --->  git push
        |
        v
Use development / feature branches and pull requests
        |
        v
Use project guidance files to plan the customer-support AI
```

## Beginner checklist

- [ ] I created and opened the project folder.
- [ ] I created a GitHub repository.
- [ ] `uv --version` works.
- [ ] I ran `uv init`.
- [ ] I ran `uv venv`.
- [ ] I added the required dependency or dependencies.
- [ ] I understand what `pyproject.toml`, `.venv/`, `.gitignore`, and `README.md` are for.
- [ ] I staged and committed my changes.
- [ ] I connected the local repository to the correct GitHub URL.
- [ ] I pushed to the intended branch.
- [ ] I did not upload secrets or the `.venv/` folder.
- [ ] I understand that feature work should be reviewed before it is merged into a stable branch.

**Final lesson:** don't try to memorize every command at once. Remember the story: prepare the workshop, set up the Python tools, save checkpoints with Git, share them with GitHub, and keep experiment[...]
