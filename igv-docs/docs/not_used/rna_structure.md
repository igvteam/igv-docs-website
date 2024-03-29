
<!---
The page title should not go in the menu
-->
<p class="page-title"> RNA structure </p>

IGV can be used to visualize RNA secondary structures in arcs connecting base pairs (the linear format). Alternative
structures, where one nucleotide is involved in more than one base pair, and pseudo knots, where arcs cross, can be
accommodated.


To visualize the structures, the base pairing information should be stored in a bed format file, which is quite
    similar to the commonly used &#39;connect format&rsquo; described by the mfold program (Zuker 2003, PMID: 12824337).
    
<!---
THE FOLLOWING IS ALREADY IN THE DATAFORMATS PAGE:
-->
    
The file must include a track line which species graphType=arc, e.g. &quot;track graphType=arc&rdquo;. Each record
    line must contain the first three columns of a bed file: chrom, start and end, where the start and end represent the
    base pair. Note that the start position follows standard BED file convention and is zero-based (first base on a
    sequence is position 0). The following small example represent a hypothetical stem loop:</p>

```
    track graphType=arc
    chr1 10 25 stemloop1
    chr1 11 24 stemloop1
    chr1 12 23 stemloop1
    chr1 13 22 stemloop1
    chr1 14 21 stemloop1
    chr1 15 20 stemloop1
```

Additional examples can be found in the supplement of the following paper

[Lu Z, Zhang QC, Lee B, Flynn RA, Smith MA, Robinson JT, Davidovich C, Gooding AR, Goodrich KJ, Mattick JS, Mesirov JP, Cech TR, Chang HY. RNA Duplex Map in Living Cells Reveals Higher-Order Transcriptome Structure. Cell. 2016 May 12](https://www.cell.com/cell/abstract/S0092-8674(16)30422-6).
