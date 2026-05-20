# Tools/Tooling 

## Install Mistral Vibe locally from `git` repo using `uv`

```
uv tool install --from git+https://github.com/ph4ge/mistral-vibe mistral-vibe
```

## Install Mistral Vibe locally from `git` repo

After cloning the [`mistral-vibe`](https://github.com/mistralai/mistral-vibe/) repository, you can run the tests using the following steps:

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


## Installing Mistral Vibe locally (multiple instances/versions of it)

Sometimes, it's interesting to have multiple instances of Mistral Vibe installed. This is easily achieved using Python virtualenv e.g. through `uv`.

The following is especially useful when one wants to use a fresh `config.toml` file. More specifically, an already installed instance of `vibe` could be located at:

```bash
~/.local/bin/vibe
```

but actually pointing to:

```bash
~/.local/share/uv/tools/mistral-vibe/bin/vibe
```

Now, installing another instance of `vibe` in another virtualenv would still pick up the `config.toml` file which is by default located:

```bash
~/.vibe/config.toml   
```

Depending on the use case, this can be useful and especially for re-using the locally stored API keys.

However, if one wants to have a fresh `config.toml` file, we need an additional step. For demonstration purposes, we use the `/tmp/` directory:

1) **Create a directory:**

```bash
mkdir /tmp/vibe-test
```

2) **Set and expose the `VIBE_HOME` variable to this directory**:

```bash
export VIBE_HOME=/tmp/vibe-test
```

3) **Create and activate your virtualenv** and install Mistral Vibe:

```bash
uv venv 
Using CPython 3.14.2
Creating virtual environment at: .venv
```
```bash
source .venv/bin/activate
uv pip install git+https://github.com/ph4ge/mistral-vibe mistral-vibe # using my fork
```
`vibe` will be installed:
```bash
(.venv)/tmp/vibe-test$ which vibe
/tmp/vibe-test/.venv/bin/vibe
```

4) **Run Mistral Vibe:**

```bash
vibe
```
This will create a fresh `config.toml` file in `/tmp/vibe-test`
