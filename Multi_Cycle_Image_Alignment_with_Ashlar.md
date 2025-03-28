# Multi-cycle Image Alignment with Ashlar

## One-Time Setup: Anaconda Environment Configuration

These steps are required only once to set up your Anaconda environment on the system.

```bash
# Load the Anaconda3 module
use Anaconda3

# Initialize conda
conda init

# Configure conda to recognize the specified environment directory
conda config --append envs_dirs /broad/grekalab/jignacio/projects/align-img/lib/conda-envs

# Set the environment prompt to display the active environment name
conda config --set env_prompt '({name}) '

# Optional: Verify the environment configuration
# conda info --envs
````

## Login and Environment Loading

These commands are used to log in to the system and load the necessary environment for running the alignment code.

```bash
# Log in to UGER
use UGER

# Start an interactive session with 4GB of memory and 1 core.  The default values were found to be sufficient for Ashlar.
ish -l h_vmem=4g -pe smp 1

# Load the Anaconda3 module
use Anaconda3

# Change the current directory to the alignment project directory
cd /broad/grekalab/jignacio/projects/align-img

# Activate the 'ashlar-fmt' conda environment, which contains the Ashlar installation
conda activate ashlar-fmt
```

## Code Format: Ashlar Command

The following shows the general format for running the `ashlar` command.

```bash
ashlar "<path/to/cycle1/Images/Index.xml>" \
       "<path/to/cycle2/Images/Index.xml>" \
       "..." \
       "<path/to/cycleN/Images/Index.xml>" \
       --output "<path/to/output/dir>" \
       --output-channels 0 --plates
```

**Explanation of arguments:**

-   `"<path/to/cycle1/Images/Index.xml>"`: Paths to the `Index.xml` files for each imaging cycle (cycle1, cycle2, ..., cycleN).
    
-   `--output <path/to/output/dir>`: Path to the output directory. If argument the is dropped, a directory will be created in the current directory based on the path of the first cycle.
    
-   `--output-channels 0`: This flag specifies that only the first channel should be included in the output, usally used for a test run. In this case, it is assumed that the first channel is HOECHST/DAPI. Drop this argument to output all channels.
    
-   `--plates`: This flag enables plate mode analysis. When specified, Ashlar processes each well independently. If this flag is omitted, Ashlar treats all images as part of a single tissue.
    
Further arguments and explanations may be found on the [Ashlar GitHub page](https://labsyspharm.github.io/ashlar/instructions/running.html).

## Test Alignment of 3 Cycles

This is an example command to test the alignment of three imaging cycles using Ashlar.

```bash
ashlar "/broad/grekalab/Giulia/Export files cohort 2/Cycle 11/Second measurement 2b/2024120241204_cycle11__2024-12-05T14_59_26-Measurement 2b/Images/Index.xml" \
       "/broad/grekalab/Giulia/Export files cohort 2/Cycle 2/20241121_cycle2__2024-11-21T12_19_16-Measurement 1b/Images/Index.xml" \
       "/broad/grekalab/Giulia/Export files cohort 2/Cycle 3/20241122_cycle 3__2024-11-22T12_18_44-Measurement 1b/Images/Index.xml" \
       --output "/broad/grekalab/Giulia/Export files cohort 2/ashlar output" \
       --output-channels 0 --plates
```
**Additional Notes:**
-  It takes about 5-10 minutes to stich and align two cycles of one well.
-  The ouput is a row letter-column number format (A01) instead of r01c01 that Harmony uses.
