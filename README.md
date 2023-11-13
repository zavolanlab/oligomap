# Oligomap

1. **[Introduction](#introduction)**
2. **[Installation](#installation)**
3. **[Usage](#usage)**
4. **[Output Format](#output-format)**
5. **[Test data](#test-data)**
6. **[Citing Oligomap](#citing-oligomap)**
7. **[License](#license)**

## Introduction

`Oligomap` is a program for fast identification of nearly-perfect matches of
small RNAs in sequence databases. It allows to exhaustively identify
all the perfect and 1-error (where an error is defined to be a mismatch,
insertion or deletion) matches of large sets of small RNAs to target
sequences. 

> NOTE: Optimal performance is achieved at about 500000 query sequences. This
will require ~2GB of memory.

## Installation

### With Conda

`Oligomap` can be installed using package manager [Conda](conda), which needs
to be installed on your system before proceeding.

```bash
conda install -c bioconda oligomap
```

### With Docker

You can create a new container using the [docker](docker) platfrom, which needs
to be installed on your system, from the `oligomap` image with the command:

```bash
docker pull quay.io/biocontainers/oligomap:1.0.1--hdcf5f25_0
```

### Building from source

To install `oligomap`, you must ensure you have installed in your system
`autoconf`, `automake`, `cmake` and `libtool`. If you don't, you can install
them with the command:

```bash
sudo apt-get install libtool cmake automake autoconf
```

In addition, you need to ensure that the `g++` compiler has the minimum version
`11.3.0`.
Once these dependencies are available, traverse to the desired path on your
file system, then clone the repository and change into it with:

```bash
git clone https://github.com/zavolanlab/oligomap.git
cd oligomap
```

In order to build the program, traverse to the [install](install) directory and
use the commands:

```bash
./configure
make
```

If you have root permissions you can install `oligomap` with the command:

```bash
sudo make install
```

## Usage

`Oligomap` is a command line program that requires at least two arguments:

- `target.fa`. Target sequences we want to map the library against.
- `query.fa`. Small RNA sequence library to be mapped.

In addition, the available arguments are:

| Flag | Meaning |
| - | - |
| -s | scan only plus strand of the target |
| -d | scan all `.fa` target files in a directory (`target.fa` must be a directory) |
| -r PATH | create a match report at the end |
| -m INT | maximum hits for one query to print |

> NOTE: By default, the output is printed to the `STDOUT`. To keep the results
the output must be redirected. 

If you just built the program, you can run it from the directory where the
executable is with the command:

```bash
./oligomap target.fa query.fa
```

If you installed `oligomap` using [Conda](conda) or with `make install`, you can
run it from any directory with the command:

```bash
oligomap target.fa query.fa
```

If you had pulled the [docker](docker) image, you can run `oligomap` using the
command:

```bash
docker run oligomap target.fa query.fa
```

## Output format

`Oligomap` returns the alignment's data in 6 lines:

- The first line contains the read's name, its length, the start and end
mapped positions in the read's sequence, the reference sequence name and, the
start and end mapped positions in the reference sequence in this order.
- The second line, contains the reference sequence name.
- The third line, contains the fields "errors:" and "orientation:" with the
alignment's number of errors and reference sequence strand.
- The fourth and sixth lines are the read and reference sequences
respectively.
- The fifth line contains a vertical bar for each match between the sequences
base pairs or a space otherwise.

Alignments are separated with a blank line.

Below is an example consisting of two output records:

```console
    read_1 (23 nc) 1..23	ref_chr_19	44377..44398
    ref_chr_19
    errors: 1 orientation: +
    CTACAAAGGGAAGCACTTGTCTC
    |||||||||||||||||| ||||
    CTACAAAGGGAAGCACTT-TCTC


    read_2 (22 nc) 1..22	ref_chr_19	5338..5359
    ref_chr_19
    errors: 0 orientation: -
    TCAAAACTGAGGGGCATTTTCT
    ||||||||||||||||||||||
    TCAAAACTGAGGGGCATTTTCT
```

The report created when setting the flag `-r PATH` consists of a three-field
table with the following content:

- The read's name
- The number of alignments found for that read with no errors
- The number of alignments found for that read with a single error

```console
    read_1   0   2
    read_2   3   1
    read_3   0   0
```

## Test data

Under the [test](test) directory you can find test data. Consult the
[README](test/README.md) file located there for usage examples.

## Citing Oligomap

If you use oligomap in your research, please cite:

	Berninger P, Gaidatzis D, van Nimwegen E, Zavolan M. 
	"Computational analysis of small RNA cloning data", Methods, 44(13-21), 2008

## License

This project is covered by the [GPL-3.0](LICENSE) License.

[biocontainer]: <https://biocontainers-edu.readthedocs.io/en/latest/what_is_biocontainers.html>
[conda]: <https://docs.conda.io/projects/conda/en/latest/index.html>
[docker]: <https://docs.docker.com/>
