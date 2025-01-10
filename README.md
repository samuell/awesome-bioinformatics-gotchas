# (Not so) Awesome Bioinformatics Gotchas

### Confusing meaning of M operation in CIGAR strings

Wikipedia [writes this](https://en.wikipedia.org/w/index.php?title=Sequence_alignment&oldid=1260199287#CIGAR_Format) about the CIGAR string:

> The original CIGAR format from the [exonerate alignment
> program](https://www.ebi.ac.uk/about/vertebrate-genomics/software/exonerate)
> did not distinguish between mismatches or matches with the M character.
> 
> The [SAMv1 spec document](https://github.com/samtools/hts-specs/blob/master/SAMv1.pdf) defines newer CIGAR codes. In most cases it is
> preferred to use the `=` and `X` characters to denote matches or mismatches
> rather than the older `M` character, which is ambiguous.

### Count reads is a FASTQ using lines that start with `@`

FASTQ files use `@` to denote the start of a new read, but `@` is also a valid quality score! 

Let's pretend this is your FASTQ:

```
@read_1
ANCACCAGCACGCCGCTGGCCTCCAGCACCAGCTCGCTGGTCAGGCGCAGGCCCGCCTGTTTATCCTCCGCCGTTACCGTCAGGGTGTGTCCCTGCTGCTGCACGTCTGTAGTGGTAAAGACGGGGGAACCGTCCAGCCCCTGGCGATGT
+
@#IIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIIII
@read_2
GCCCGAATCGCAGCAGCAACGCTGCAACCGGTAGCACGGCGATAGGGAGCTGCAAAGCCCTACCGAGGCGCTGGAAAAAACCTAAAATATTCATCCTATTCCCCCTACGAGAACCATTGTTAAGACTCGCGCATAAACTATGTTTTTATC
+
9III999II9I99II9IIII9I99--III-9I-9II-II9I-I-I---IIIIII9999I-II-I-9II9-I--9I9-I---9--9999-9-9999-9I-II9III99999II--I-II-9I-I--IIII999-9-III-9I9-III999-
```

So, you can't simply use something like the following:

```
grep -c "^@" test.fastq
```

Because in `read_1` the quality line begins with `@`, so you will incorrectly get 3 reads, instead of 2.

### BCFTools actually has a lot of plug-ins

If you have ever used BCFTools and found yourself requiring additional data to be added to your VCF file, you are not alone. Fortunately BCFTools offers a rich set of [plugins](https://samtools.github.io/bcftools/howtos/plugins.html) that can be used to fill in missing VCF information or to perform complex operations.

For example, if you need to filter VCF entries based on the alternate allele frequency (AF), you may find that BCFTools does not provide this information by default. However the [fill-tags](https://samtools.github.io/bcftools/howtos/plugin.fill-tags.html) plugin can compute and populate the AF values while adding additional information to the `INFO` and `FORMAT` tags that can be used for subsequent operations.

## Other Resources:

- [Blasted Bioinformatics](https://blastedbio.blogspot.com/) A blog of common bioinformatics gotchas written by [Peter Cock]([https://github.com/peterjc/blast_max_target_seqs](https://github.com/peterjc)) containing a list of bioinformatic lessons learned the hard way including a set of posts related to Blast+ parameter issues.




