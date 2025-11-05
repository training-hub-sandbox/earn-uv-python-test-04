## Step 1: Install UV and Verify Setup

Welcome to your UV learning journey! In this first step, you'll install UV and get familiar with this modern Python package manager.

### 📖 Theory: What is UV?

> [!NOTE]
> UV is a fast Python package installer and resolver written in Rust. It's designed to be a drop-in replacement for pip, pip-tools, virtualenv, and more - all in one tool!

Key benefits of UV:
- **Fast**: 10-100x faster than pip
- **All-in-one**: Replaces multiple tools (pip, virtualenv, pip-tools)
- **Reliable**: Deterministic dependency resolution
- **Modern**: Built with the latest Python packaging standards

### ⌨️ Activity: Install UV and document your setup

1. Install UV using the official installer:
   - **macOS/Linux**: Run `curl -LsSf https://astral.sh/uv/install.sh | sh`
   - **Windows**: Run `powershell -c "irm https://astral.sh/uv/install.ps1 | iex"`

2. Close and reopen your terminal to ensure UV is in your PATH

3. Verify the installation by running:
   ```bash
   uv --version
   ```

4. Create a new file named `INSTALLATION.md` in the root of this repository

5. In `INSTALLATION.md`, document:
   - The UV version you installed (include the text "uv version" followed by the version number)
   - Your operating system
   - The installation method you used

6. Commit your changes and push to the main branch:
   ```bash
   git add INSTALLATION.md
   git commit -m "Add UV installation documentation"
   git push
   ```

<details>
<summary>Having trouble? 🤷</summary><br/>

- If the installation command fails, ensure you have `curl` (macOS/Linux) or PowerShell (Windows) available
- If `uv --version` doesn't work after installation, try restarting your terminal completely
- On macOS, you might need to add `~/.cargo/bin` to your PATH manually
- Make sure to include the exact text "uv version" in your INSTALLATION.md file for the automated check to pass

</details>
