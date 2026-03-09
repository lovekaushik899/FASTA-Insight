# FASTA-Insight

A comprehensive toolkit for FASTA sequence analysis with support for both nucleotide and protein sequences. FASTA-Insight provides statistical analysis, sequence composition metrics, and advanced sequence pattern detection.

## Overview

FASTA-Insight is a dual-tool suite designed for bioinformatics workflows. It offers two implementations:
- **Python version** (`fasta_analysis.py`): Full-featured with visualization capabilities
- **Bash version** (`fasta_analysis.sh`): Lightweight alternative for shell-based pipelines

Both tools perform core sequence analysis tasks including length statistics, composition analysis, k-mer counting, palindrome detection, and ORF (Open Reading Frame) identification.

## Features

### Core Analysis
- **Sequence Statistics**: Count, length distribution (min, max, mean, median, std)
- **Sequence Composition**: Nucleotide or amino acid frequency analysis
- **GC Content**: GC percentage calculation per sequence
- **GC Skew**: (G-C)/(G+C) ratio computation (Python)
- **K-mer Analysis**: Frequency distribution of k-length subsequences

### Advanced Features
- **Palindrome Detection**: Identification of palindromic motifs (4-12 bp)
- **ORF Finding**: Open Reading Frame detection in all 6 reading frames
- **Molecular Weight**: Protein molecular weight calculation (Python)
- **Visualization**: Length and GC content distribution plots (Python)

## Installation

### Prerequisites

**Python version:**
```bash
python3 >= 3.6
pip install numpy matplotlib
```

**Bash version:**
- Standard Unix utilities (awk, sort, sed)
- No external dependencies

### Setup

```bash
# Clone the repository
git clone https://github.com/lovekaushik899/FASTA-Insight.git
cd FASTA-Insight

# Make scripts executable
chmod +x fasta_analysis.py fasta_analysis.sh
```

## Usage

### Python Implementation

#### Basic nucleotide analysis:
```bash
python3 fasta_analysis.py --input sequences.fasta --nt
```

#### Protein sequence analysis:
```bash
python3 fasta_analysis.py --input proteins.fasta --pep
```

#### Parallel processing (specify cores):
```bash
python3 fasta_analysis.py --input sequences.fasta --nt --cores 4
```

### Bash Implementation

#### Basic nucleotide analysis:
```bash
./fasta_analysis.sh --input sequences.fasta --nt
```

#### Protein sequence analysis:
```bash
./fasta_analysis.sh --input proteins.fasta --pep
```

#### Multi-core processing:
```bash
./fasta_analysis.sh --input sequences.fasta --nt --cores 8
```

## Output

### Console Output

**Sequence Summary:**
```
==============================
FASTA SUMMARY
==============================
count      : 100
min        : 245
max        : 5420
mean       : 1523.45
median     : 1201.50
std        : 892.34
```

**Nucleotide Composition:**
```
NUCLEOTIDE COMPOSITION
A: 0.3145
T: 0.2891
G: 0.1945
C: 0.2019
```

**K-mer Analysis (Top 20):**
```
TOP 20 KMER (k=3)
125 ATG
89  GCG
76  TAA
...
```

### Generated Files

- `sequence_length_distribution.png` - Histogram of sequence lengths
- `gc_distribution.png` - GC content frequency distribution
- `predicted_orfs.fasta` - Detected ORFs in FASTA format

## Command-Line Options

| Option | Description | Required |
|--------|-------------|----------|
| `--input FILE` | Path to input FASTA file | Yes |
| `--nt` | Analyze nucleotide sequences | No* |
| `--pep` | Analyze protein sequences | No* |
| `--cores N` | Number of processing cores | No (default: 1) |

*Specify either `--nt` or `--pep`

## Input Format

Input files must be in standard FASTA format:

```
>sequence_header_1
ATGCGATGCGATGC
>sequence_header_2
GCTAGCTAGCTAGC
```

- Headers start with `>`
- Sequences can span multiple lines
- Supports mixed case (converted to uppercase)
- Handles standard IUPAC codes (N for nucleotides)

## Algorithm Details

### ORF Detection
- Searches all 6 reading frames (forward and reverse complement)
- Identifies start codon (ATG) and stop codons (TAA, TAG, TGA)
- Outputs complete ORF sequences from ATG to first in-frame stop

### Palindrome Detection
- Searches for sequences identical to reverse complement
- Range: 4-12 bp length
- Reports top 20 by frequency

### K-mer Analysis
- Extracts all k-length subsequences
- Counts frequency across all sequences
- Useful for sequence fingerprinting and composition profiling

## Performance Considerations

**Python Version:**
- Faster processing for large datasets
- Supports multi-core execution
- Memory-efficient streaming of results

**Bash Version:**
- Lower memory overhead
- Suitable for resource-constrained environments
- Single-threaded processing

## Examples

### Example 1: Analyze nucleotide sequences
```bash
python3 fasta_analysis.py --input genomes.fasta --nt --cores 4
```
This will:
- Load sequences from `genomes.fasta`
- Calculate length statistics
- Analyze nucleotide composition
- Generate GC content plots
- Detect ORFs and palindromes
- Output `predicted_orfs.fasta`

### Example 2: Protein analysis
```bash
./fasta_analysis.sh --input proteins.fasta --pep
```
This will:
- Load protein sequences
- Calculate length statistics
- Analyze amino acid composition

## Output Interpretation

- **GC Content**: Higher values indicate more stable DNA (3 H-bonds per GC vs 2 for AT)
- **K-mer Distribution**: Identifies compositional biases in sequences
- **Palindromic Motifs**: Often represent restriction enzyme recognition sites
- **ORF Length**: Longer ORFs more likely to represent functional genes

## Troubleshooting

**Issue**: `The requested resource was not found`
- Verify input file path is correct and accessible
- Check file permissions

**Issue**: `Unknown parameter` (Bash)
- Review command syntax: `--input`, `--nt`/`--pep`, `--cores`

**Issue**: Memory errors with large files (Python)
- Reduce `--cores` parameter
- Process files in segments

## Limitations

- Does not perform alignment or homology searches
- ORF detection is basic (no codon usage optimization)
- Assumes standard genetic code
- Palindrome detection limited to specified length range

## Contributing

For bug reports and feature requests, please open an issue on the repository.

## License

This project is provided as-is for research and educational purposes.

## References

- FASTA Format: https://en.wikipedia.org/wiki/FASTA_format
- IUPAC Codes: https://en.wikipedia.org/wiki/Nucleic_acid_notation
- ORF Detection: https://en.wikipedia.org/wiki/Open_reading_frame

## Authors

- **lovekaushik899** - Initial development

---

**Version**: 1.0.0  
**Last Updated**: 2026-03-09
