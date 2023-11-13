## Description

This directory contains data for each of the following examples.
The `genomic_ref.fa` file contains a sequence of 10000 nucleotides
from the _Homo sapiens_ chromosome 19 reference sequence. The `test_library.fa`
file contains a set of 250 small RNA sequences build with a custom script.

## Examples

In this section, one example per CLI option will be seen. Each of which, will
use the same set of small RNA sequences and the same set of genomic references.
Note that the directory used in the third example contains exactly the same
reference sequence, but split across different files.

### Example 1 | Basic usage

```bash
oligomap genomic_ref.fa test_library.fa > results.oligomap
```

### Example 2 | Generate a match report

```bash
oligomap genomic_ref.fa test_library.fa -r report.txt > results.oligomap
```

### Example 3 | Use directory as a target

```bash
oligomap genome_seqs/ test_library.fa -d > dir_results.oligomap
```

### Example 4 | Scan only target plus strand

```bash
oligomap genomic_refs.fa test_library.fa -s > plus_strand_results.oligomap
```

### Example 5 | Set maximum number of hits

```bash
oligomap genomic_refs.fa test_library.fa -m 2 > m_2_results.oligomap
```
