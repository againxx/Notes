# GitHub Actions
A platform to **automate developer workflows**
    - When something happens in/to your repository (GitHub events), automatic actions are executed in response

## Syntax
* `name` [optional], is displayed on your repos action page
* `on` [required], name of GitHub event that triggers the workflow
* `jobs` [required], one or more jobs, is composed of sequence of tasks (steps)
    - `steps` can run commands, setup tasks or run an action
        - `uses` selects an **action** (under path `action/` of a reusable repo)
        - `run` runs a command-line command (use `|` to run multiple commands)
    - `runs-on`, can runs on Ubuntu, Windows, or macOS

## Where does this code run?
* managed by GitHub (but can also host you own)
* **each job** in a workflow **runs in a fresh** virtual environment (runs in parallel by default)
