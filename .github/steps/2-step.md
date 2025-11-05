## Step 2: Create Your First UV Project

Great job installing UV! Now let's create a Python project with a specific Python version.

### 📖 Theory: UV Project Initialization

> [!TIP]
> UV automatically manages Python versions for you. When you specify a Python version, UV will download and use it if it's not already on your system!

Key concepts:
- **`uv init`**: Creates a new Python project with the recommended structure
- **`pyproject.toml`**: The modern Python project configuration file (PEP 621)
- **Python version management**: UV handles downloading and managing Python interpreters
- **Project structure**: UV creates a clean, standard project layout

### ⌨️ Activity: Initialize a calculator project

1. In the root of your repository, initialize a new UV project with Python 3.12:
   ```bash
   uv init --python 3.12
   ```

2. Examine the generated `pyproject.toml` file. Notice:
   - The `requires-python` field specifying Python 3.12
   - The project metadata section
   - The build system configuration

3. Create a file named `calculator.py` in the root with the following code:
   ```python
   def add(a: float, b: float) -> float:
       """Add two numbers and return the result."""
       return a + b

   def subtract(a: float, b: float) -> float:
       """Subtract b from a and return the result."""
       return a - b

   if __name__ == "__main__":
       print(f"5 + 3 = {add(5, 3)}")
       print(f"10 - 4 = {subtract(10, 4)}")
   ```

4. Commit your changes and push to the main branch:
   ```bash
   git add pyproject.toml calculator.py
   git commit -m "Initialize UV project with calculator"
   git push
   ```

<details>
<summary>Having trouble? 🤷</summary><br/>

- If UV says Python 3.12 isn't available, run `uv python install 3.12` first
- Make sure you're running `uv init` from the root directory of your repository
- If you accidentally ran `uv init` with a project name, you can delete the generated folder and run `uv init` without arguments
- The `pyproject.toml` must contain "3.12" for the automated check to pass

</details>
