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
