# Tools/Tooling 

## Install Mistral Vibe locally from `git` repo using `uv`

```
uv tool install --from git+https://github.com/ph4ge/mistral-vibe mistral-vibe
```

## Install Mistral Vibe locally from `git` repo

After cloning the `mistral-vibe` repository, you can run the tests using the following steps:

1) **Navigate to the repository directory**:

   ```bash
   cd mistral-vibe
   ```

2) **Install the package in development mode** (this will install all dependencies):

   ```bash
   uv pip install -e .
   ```

3) **Run the tests**:

   ```bash
   uv run pytest
   ```

4) **For more detailed output**, you can add the `-v` flag:

   ```bash
   uv run pytest -v
   ```

5) **To run specific tests**, you can specify the test file or directory:

   ```bash
   uv run pytest tests/test_core.py
   ```

6) **To run tests with coverage**, you can use the following command:

   ```bash
   uv run pytest --cov=vibe
   ```

These commands will run the test suite for `mistral-vibe` using `pytest`. The `-e` flag in the installation command installs the package in development mode, which is necessary for running the tests.

## Quickly running pytest

After cloning the `mistral-vibe` repo (this assumes that [uv](https://docs.astral.sh/uv/) is installed)


1) **Navigate to the repository directory**:

   ```bash
   cd mistral-vibe
   ```

2) **Trigger tests**: 
   ```bash
   uv run pytest -v
   ``` 

This will automatically create a virtual environment and run the tests.
