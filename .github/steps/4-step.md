## Step 4: Run Code with UV

Perfect! You've added dependencies. Now let's learn how UV makes running code seamless.

### 📖 Theory: Running Code with UV

> [!TIP]
> `uv run` automatically manages your virtual environment and executes Python in the project context. No need to activate/deactivate environments manually!

Key concepts:
- **`uv run`**: Executes Python scripts or commands in the project environment
- **Automatic environment management**: UV creates and manages virtual environments behind the scenes
- **No activation needed**: Unlike traditional virtualenvs, you never need to run "activate"
- **Consistent execution**: Everyone on your team runs code the same way

### ⌨️ Activity: Create tests and run your code

1. Create a new file named `test_calculator.py` with these tests:
   ```python
   from calculator import add, subtract

   def test_add():
       assert add(2, 3) == 5
       assert add(-1, 1) == 0
       assert add(0, 0) == 0

   def test_subtract():
       assert subtract(5, 3) == 2
       assert subtract(10, 10) == 0
       assert subtract(0, 5) == -5
   ```

2. Run your calculator script using UV:
   ```bash
   uv run calculator.py
   ```
   You should see the addition, subtraction, and random number output.

3. Run your tests using UV:
   ```bash
   uv run pytest
   ```
   All tests should pass!

4. Create a `README.md` file documenting how to use the project:
   ```markdown
   # Calculator Project

   A simple calculator built with UV for Python dependency management.

   ## Running the Calculator

   Run the calculator using uv run:
   ```bash
   uv run calculator.py
   ```

   ## Running Tests

   Run tests using pytest:
   ```bash
   uv run pytest
   ```

   ## Requirements

   - UV installed
   - Python 3.12+
   ```

5. Commit your changes and push to the main branch:
   ```bash
   git add test_calculator.py README.md
   git commit -m "Add tests and documentation"
   git push
   ```

<details>
<summary>Having trouble? 🤷</summary><br/>

- If `uv run` fails, ensure you're in the project root directory
- Make sure you ran `uv add --dev pytest` in the previous step
- If tests fail, check that your calculator functions match the test expectations
- The README.md must contain "uv run" for the automated check to pass
- Remember: no need to activate any virtual environment, UV handles it!

</details>
