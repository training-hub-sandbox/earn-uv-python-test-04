## Step 3: Add and Manage Dependencies

Excellent! Now that you have a project, let's add some external packages.

### 📖 Theory: Dependency Management with UV

> [!IMPORTANT]
> UV automatically updates both `pyproject.toml` and `uv.lock` when you add dependencies. The lock file ensures everyone gets the exact same versions!

Key concepts:
- **`uv add`**: Installs and adds dependencies to your project
- **`--dev` flag**: Marks dependencies as development-only (not needed in production)
- **`uv.lock`**: Lock file that pins exact versions for reproducibility
- **Automatic dependency resolution**: UV figures out compatible versions for all packages

### ⌨️ Activity: Add dependencies to your calculator

1. Add the `requests` package (we'll use it to fetch data):
   ```bash
   uv add requests
   ```

2. Add `pytest` as a development dependency:
   ```bash
   uv add --dev pytest
   ```

3. Update `calculator.py` to add a new function that fetches a random number:
   ```python
   import requests

   def add(a: float, b: float) -> float:
       """Add two numbers and return the result."""
       return a + b

   def subtract(a: float, b: float) -> float:
       """Subtract b from a and return the result."""
       return a - b

   def get_random_number() -> int:
       """Fetch a random number from an API."""
       response = requests.get("https://www.randomnumberapi.com/api/v1.0/random?min=1&max=100")
       return response.json()[0]

   if __name__ == "__main__":
       print(f"5 + 3 = {add(5, 3)}")
       print(f"10 - 4 = {subtract(10, 4)}")
       print(f"Random number: {get_random_number()}")
   ```

4. Observe the changes:
   - Check `pyproject.toml` - notice `requests` in dependencies
   - Check `pyproject.toml` - notice `pytest` in `dependency-groups.dev`
   - A new `uv.lock` file was created

5. Commit your changes and push to the main branch:
   ```bash
   git add pyproject.toml uv.lock calculator.py
   git commit -m "Add requests and pytest dependencies"
   git push
   ```

<details>
<summary>Having trouble? 🤷</summary><br/>

- Make sure UV is in your PATH and working (`uv --version`)
- If `uv add` fails, ensure you're in the project root directory
- The lock file (`uv.lock`) might be large - that's normal!
- Both `requests` and `pytest` must appear in `pyproject.toml` for the checks to pass
- Don't forget to commit the `uv.lock` file - it's important for reproducibility!

</details>
