# Community-Based-Metagenome-Binning
Uses my Universal Reference Database and the ContigAnalysis.pl output to generate functionally complete strain-specific MAGs.

In a separate repository () I describe using a modified read quality control process, and using multiple assemblers with specific settings, followed by assembly merging using my merge-overlap.pl script. This is all in an attempt to get a high quality metagenome assembly with the longest possible contigs and most comprehensive collection of genes.

Then I described how to use Diamond to align the predicted contig genes to my Universal Reference Database genes (proteins in this case as Diamond does BlastX). The ContigAnalysis.pl script does a variety of things. 
1. First it screens the Diamond output - removing any URD hits with less than half the score of the top hit OR any hits with a score < 1000 AND an eval > 0.0000001.
2. Next it extracts all the organisms and functions for each hit from the URD.
3. Then it loops through all the organisms, removing those who do not have a least 1 unique gene (1 gene to 1 hit found in only 1 organism).
4. It also finds genes with only organisms having no unique genes, then setting aside the highest scoring organisms to explain those non-unique genes, removing the remaining organisms from all gene-hit-lineages.
5. Now with the reduced gene-lineages, loop through all contigs, constructing each gene's lowest common ancestor (LCA) and from these, the contig LCA. If it is a partial end gene, they tend to have many more URD hits/lower LCA - thus reduce the sensitivity of the contig LCA. 
