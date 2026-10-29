# AI CI_Agent: Autonomous CI Detection & Repair Demo

A standalone, guide-ready demonstration application for autonomous CI failure diagnosis and repair using local LLMs (Ollama `qwen2.5:3b`) and Docker container verification.

---

## 🎯 What This Demo Shows to Your Project Guide

1. **Target Repository Inspection:** Fetches repository `https://github.com/bhuvaneshwaran016/taskflow_ci_agent_test` and inspects the latest failed GitHub Actions CI run (`Workflow: TaskFlow CI - FAILED ❌`).
2. **Workspace Isolation:** Clones the target into an isolated `workspace/` folder, keeping the original repository completely untouched.
3. **Reproduces CI Failure Locally:** Executes `pytest -v`, capturing the real failure output (**51 passed, 58 failed, exit code 1**).
4. **LLM Chain-of-Thought Diagnosis & Repair:** Sends failure context to the local Ollama LLM (`qwen2.5:3b`), diagnoses all 7 defects in `taskflow/service.py`, and generates a minimal code patch.
5. **Local Full Suite Verification:** Reruns pytest across all tests, verifying **109 passed, 0 failed, 100% success (exit code 0)** with zero regressions.
6. **Docker Container Verification:** Mounts the repaired code into an ephemeral clean Linux Docker container and executes the full pytest suite inside Docker, proving environment-independent correctness (**109 passed in Docker, exit code 0**).
7. **Code Diff Review:** Displays the unified diff of the repaired code.
8. **Human Approval & Push to GitHub:** Prompts the user:
   - Entering **`YES`** stages, commits, and pushes the Docker-verified fix to GitHub.
   - Automatically monitors the newly triggered GitHub Actions CI workflow live on GitHub until it finishes with **PASSED ✅**.

---

## 🚀 How to Run the Demo

Open PowerShell in this folder (`D:\Ci_Agent_demo`):

```powershell
Set-Location D:\Ci_Agent_demo
uv run python main.py
```

Or run with the repository URL directly:

```powershell
uv run python main.py https://github.com/bhuvaneshwaran016/taskflow_ci_agent_test
```

When prompted:
- **Target Repository URL:** Press `Enter` (uses default `https://github.com/bhuvaneshwaran016/taskflow_ci_agent_test`).
- **Push Approval:** Type `YES` to push the Docker-verified fix to GitHub and watch GitHub Actions CI pass live!
