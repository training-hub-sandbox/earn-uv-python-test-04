## Step 5: Working with Multiple Python Versions

You're almost done! In this final step, let's explore UV's Python version management capabilities.

### 📖 Theory: Python Version Management

> [!NOTE]
> UV can install and manage multiple Python versions on your system. This is perfect for testing compatibility or working with different project requirements!

Key concepts:
- **`uv python list`**: Shows all available Python versions
- **`uv python install`**: Installs a specific Python version
- **Version switching**: Change your project's Python version by updating `pyproject.toml`
- **`uv export`**: Generate a requirements.txt file for deployment

### ⌨️ Activity: Switch Python versions and export dependencies

1. Check what Python versions are available:
   ```bash
   uv python list
   ```

2. Install Python 3.11 (if not already installed):
   ```bash
   uv python install 3.11
   ```

3. Create a new branch for testing Python 3.11:
   ```bash
   git checkout -b python-3.11-test
   ```

4. Update your `pyproject.toml` to use Python 3.11. Change the `requires-python` line to:
   ```toml
   requires-python = ">=3.11"
   ```

5. Test that your code still works with Python 3.11:
   ```bash
   uv run calculator.py
   uv run pytest
   ```

6. Export your production dependencies to `requirements.txt`:
   ```bash
   uv export --no-dev > requirements.txt
   ```
   This creates a requirements.txt with only production dependencies (excludes pytest).

7. Review the `requirements.txt` file - notice it has all the pinned versions!

8. Commit your changes:
   ```bash
   git add pyproject.toml requirements.txt
   git commit -m "Update to Python 3.11 and add requirements.txt"
   git push origin python-3.11-test
   ```

9. Create a Pull Request:
   - Go to your repository on GitHub
   - Click "Compare & pull request"
   - Title: "Test Python 3.11 compatibility"
   - Create the PR

<details>
<summary>Having trouble? 🤷</summary><br/>

- If `uv python install` is slow, it's downloading and building Python - be patient!
- Make sure you're on the new branch before making changes (`git branch` to check)
- The `requirements.txt` should contain pinned versions with `==`
- If tests fail on Python 3.11, check that all dependencies are compatible
- Don't forget to push to the new branch name: `origin python-3.11-test`
- The automated check looks for "3.11" in pyproject.toml and an open pull request

</details>
