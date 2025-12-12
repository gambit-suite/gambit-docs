# Using GAMBIT on your local machine

This guide assumes you have prior knowledge of how to install software locally in a Unix command-line environment. The necessary databases will have to be downloaded independently to be used with GAMBIT. They are available in the [GAMBIT Databases](../databases/overview.md) section of this document and should be placed in a directory of your choice. The directory should not contain any other files with the same extensions.

## Installation

### Installation from Bioconda

The recommended way to install the tool is through the [Conda](https://www.anaconda.com/products/distribution) package manager from the [Bioconda](https://bioconda.github.io/) channel. You can simply run the following command to download GAMBIT’s latest version:

```bash
conda install -c bioconda gambit
```

### Installation with Docker

The latest version of GAMBIT software is available as a Docker container in Theiagen’s [Google Artifact Registry (GAR)](https://cloud.google.com/artifact-registry). If [Docker is installed in your system](https://docs.docker.com/engine/install/), you can simply run the following command to download the container:

```bash
docker pull us-docker.pkg.dev/general-theiagen/staphb/gambit:1.0.0
```

You can access the container with the following command (note: with the `-v $PWD:/data`, your current directory is being mounted to the `data/` folder inside the container):

```bash
docker run -v $PWD:/data -it us-docker.pkg.dev/general-theiagen/staphb/gambit:1.0.0 bash
```

### Installation from source

These instructions assume that you have [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git), [Python](https://www.python.org/downloads/) and [Pip](https://pip.pypa.io/en/stable/installation/) installed in your system. Navigate to <https://github.com/jlumpe/gambit> and clone the repository, or use the following command:

```bash
git clone https://github.com/jlumpe/gambit.git
```

Installing from source requires the Cython package as well as a C compiler to be installed on your system.  Navigate to the repository and install the package:

```bash
pip install .
```

## Usage

Positional arguments are one or more FASTA files containing query genome assemblies. You must provide the path to the directory containing the database files using either the `-d` option (*before* the `query` subcommand) or by setting the `GAMBIT_DB_PATH` environment variable. The results can be optionally outputted to a file, but by default, they are written to the terminal.

```bash
# optional
GAMBIT_DB_PATH=/path/to/database/
```

```bash
gambit [-d </path/to/database/>] query [-o results.csv] genome1.fasta genome2.fasta ...
```

### Advanced Usage

There are many available commands in GAMBIT:

```text
Usage: gambit [OPTIONS] COMMAND [ARGS]...

  Tool for rapid taxonomic identification of microbial pathogens from genomic data.

Options:
  -d, --db DIRECTORY  Directory containing GAMBIT database files.
  --version           Show the version and exit.
  --help              Show this message and exit.

Commands:
  dist        Calculate the GAMBIT distances between a set of query...
  query       Predict taxonomy of microbial samples from genome sequences.
  signatures  Create and inspect GAMBIT signature files.
  tree        Estimate a relatedness tree for a set of genomes and output...
```

GAMBIT’s `query` is the most used as it computes the distance of a query genome to the genomes provided in the database.

```text
Usage: gambit query [OPTIONS] GENOMES...

  Predict taxonomy of microbial samples from genome sequences.

Options:
  -l LISTFILE                     File containing paths to query genomes, one
                                  per line.
  --ldir DIRECTORY                Parent directory of paths in LISTFILE.
  -o, --output FILENAME           File path to write to. If omitted will write
                                  to stdout.
  -f, --outfmt [csv|json|archive]
                                  Format to output results in.
  -s, --sigfile FILE              File containing query signatures, to use in
                                  place of GENOMES.
  --progress / --no-progress      Show/don't show progress meter.
  -c, --cores INTEGER RANGE       Number of CPU cores to use.  [x>=1]
  --help                          Show this message and exit.
```

---