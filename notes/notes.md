# Installation

Verified and recommended methods:

- Windows: `pipx`
- Ubuntu: `asdf`

# Configuration

    pdm config

## My configuration

- install cache:

        pdm config install.cache true

    > Notes:
    > 
    > Developer mode has to be activated on Windows to enable using of symlinks.

- venv in project:

        pdm config venv.in_project false
    
    > Notes:
    > 
    > I prefer centralized location of venvs. 

- python providers:

        pdm config python.providers rye

- added subdirectories to `%LOCALAPPDATA%\pdm\pdm`:

    - `templates`

        ```bash
        %LOCALAPPDATA%\pdm\pdm> git clone https://github.com/opalapj/pdm-templates.git templates 
        ```

- added files to `%LOCALAPPDATA%\pdm\pdm`:

    - `config.toml`

        https://github.com/opalapj/pdm/blob/main/config.toml

# Get info about project

    pdm info

# Project initialization

    pdm init

# Managing interpreters

    pdm python

# Managing venvs

    pdm venv

> Notes:
>
> For venv activation:
>
>       for /f %i in ('pdm venv activate <venv name>') do %i
>
> or
>
>       for /f "tokens=*" %i in ('pdm venv activate <venv name>') do %i
>
> or
>
>       pdm venv activate <venv name> | clip
>       ctrl + v

# Managing dependencies

## List

    pdm list
    pdm list --tree
    pdm list --sort
    pdm list --fields name,version,groups,licenses,location,homepage

## Add

    pdm add
    pdm add pandas requests
    pdm add --group test pytest coverage
    pdm add --dev --group lint flake8 black
    pdm add --frozen-lockfile --no-sync pandas requests

## Lock

    pdm lock

## Install

    pdm install

> Notes:
>
> All development dependencies are included as `--prod` is not passed and `-G`
> does not specify any `dev` groups.

## Export

    pdm export
    pdm export --no-hashes --pyproject --output requirements.txt
    pdm export --no-hashes --output requirements-lock.txt

# Plugins

Development workflow described in plugin template.

## Plugin naming convention

Each plugin name should contain `pdm-` prefix, e.g.:

    pdm-hello
    pdm-learn

# Useful `pdm` options

```toml
[tool.pdm.options]
info = ["--json"]
add = ["--frozen-lockfile", "--no-sync"]
list = ["--fields", "name,version,groups,licenses,location,homepage"]
export = ["--no-hashes"]
```

More:
- https://pdm-project.org/en/latest/usage/config/#passing-constant-arguments-to-every-pdm-invocation

# Useful `pdm` scripts

```toml
[tool.pdm.scripts]
gen-req = {cmd = "pdm export --prod --pyproject --output requirements.in"}
gen-req-lock = {cmd = "pdm export --prod --output requirements.txt"}
post_lock = {composite = ["gen-req", "gen-req-lock"]}
```

More:
- https://pdm-project.org/en/latest/usage/scripts/#user-scripts
