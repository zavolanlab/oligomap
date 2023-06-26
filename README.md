# Oligomap

1. **[Introduction](#introduction)**
2. **[Installation](#installation)**
3. **[Usage](#usage)**
4. **[Test data](#test-data)**
5. **[Citing Oligomap](#citing-oligomap)**
6. **[License](#license)**

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

```
conda install -c dblue oligomap
```

> NOTE: `Oligomap` will be soon moved to the [Bioconda](bioconda) channel.


### Building from source

To install `oligomap`, you must ensure you have installed in your system
`autoconf`, `automake`, `cmake` and `libtool`. If you don't, you can install
them with the command:

```
sudo apt-get install libtool cmake automake autoconf
```

In addition, you need to ensure that the `g++` compiler has the minimum version
`11.3.0`.
Once these dependencies are available, traverse to the desired path on your
file system, then clone the repository and change into it with:

```
git clone https://github.com/zavolanlab/oligomap.git
cd oligomap
```

In order to build the program, traverse to the `installation` directory and
use the commands:

```
./configure
make
```

If you have root permissions you can install `oligomap` with the command:

```
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

```
./oligomap target.fa query.fa
```

If you installed `oligomap` using [Conda](conda) or with `make install`, you can
run it from any directory with the command:

```
oligomap target.fa query.fa
```

## Test data

Under the [test](test) directory you can find test data. Consult the
[README](test/README.md) located there for usage examples.

## Citing Oligomap

If you use oligomap in your research, please cite:

	Berninger P, Gaidatzis D, van Nimwegen E, Zavolan M. 
	"Computational analysis of small RNA cloning data", Methods, 44(13-21), 2008

## License

This project is covered by the [GPL-3.0](LICENSE) License.

[bioconda]: <https://bioconda.github.io/>
[conda]: <https://docs.conda.io/projects/conda/en/latest/index.html>