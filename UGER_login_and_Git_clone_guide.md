# UGER login and Git clone guide

## Login to UGER

Requires connection to the Broad Institute network (via VPN).

It's recommended to connect to a specific login node (login01 to login04) to resume sessions.

**Mac:**

1.  Open Terminal.
2.  Enter: `ssh <username>@login02`
3.  Enter your password.

**Windows:**

* Follow the instructions here: https://intranet.broadinstitute.org/bits/service-catalog/scientific-computing/login-servers

A successful login will display a terminal prompt.

## Optional: Using TMUX for Resumable Sessions

* Check for existing sessions: `tmux attach`
* Resume a disconnected session: `tmux attach`
* Start a new session: `tmux`

## Changing and Listing Directories

* Change directory: `cd <directory_path>`
    * Example: `cd /broad/grekalab`
* List files and folders: `ls`
* Navigate to your folder: `cd <your folder>`

## Cloning the TMED Recognition Repository

**One-time setup (for private repositories):**

* Set up SSH authentication with GitHub: https://phoenixnap.com/kb/git-clone-ssh

**Cloning the repository:**

1.  Navigate to the desired directory (e.g., `/broad/grekalab/jignacio/projects`).
2.  Clone the repository:
    ```bash
    git clone git@github.com:broadinstitute/tmed-recognition.git
    ```
3.  Change to the repository's working directory: `cd tmed-recognition`

**Pro-tip:** Use the TAB key for auto-completion of file/folder paths.

## Start an Interactive Session with a Compute Node

For computationally intensive tasks, use a compute node instead of a login node.

* Activate UGER (do this once per session): `use UGER`
* Start an interactive session with 4GB of memory: `ish -l h_vmem=4g`
    * The default `ish` command allocates 1 core and 1GB of memory and has a 3-day limit.  The `-l h_vmem=4g` overrides the memory allocation.
* Terminate an interactive session: `exit` or `CTRL+d`
* Detach from a TMUX session: `CTRL+d`
