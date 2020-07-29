# SOC2020 - Sofia Robb

Sequencing of new genomes has become commonplace. In this episode of SOC, Sofia Robb will discuss available open source methods for sharing genome-scale data if it is not feasible to share it through standard databases such as Ensembl. She will also demonstrate helpful ways to mine Ensembl data with Biomart and useful UNIX command line tricks for sorting, searching, and reformatting text data files.

[Link to talk]() 

## Hands on  Workshop: Let's LARP

Live Action Role Playing

You work with chickens and have completed an RNAseq experiment. You have two conditions, condition1 (g1 = 'h3.3a-/-, h3.3b-/-'), condition2 (g2 = 'wild type genotype'). You performed differential expression analysis, perhaps with cuffdiff. 

__Let's get the expression data__
[EBI Expression Atlas](https://www.ebi.ac.uk/gxa/home)

1. Select [chicken](https://www.ebi.ac.uk/gxa/experiments?experimentType=differential&species=gallus+gallus)
2. Check box to download the first experiment, ["RNA-seq of H3.3 knockout and wild type chicken DT40 cells"](https://www.ebi.ac.uk/gxa/experiments-content/E-MTAB-2754/resources/DifferentialSecondaryDataFiles.RnaSeq/analytics)
3. Click the download link at the top of the last column.
4. Navigate to E-MTAB-2754 directory
5. Checkout the contents of E-MTAB-2754-analytics.tsv 
```
$ head E-MTAB-2754-analytics.tsv
Gene ID	Gene Name	g1_g2.p-value	g1_g2.log2foldchange
ENSGALG00000000003	PANX2	0.100242375805959	-0.4
ENSGALG00000000011	C10orf88	0.0802046773105167	0.2
ENSGALG00000000038	CTRB2	NA	0.2
ENSGALG00000000044	WFIKKN1	NA	0
ENSGALG00000000048		0.288103121752422	0.4
ENSGALG00000000055	LAMTOR3	0.529728058895927	0.1
ENSGALG00000000059	TUBB3	0.228430079834946	-0.2
ENSGALG00000000067	SPR	0.0560358954256604	-0.4
ENSGALG00000000071		0.878861305389193	0
```

__What is it that people want to do usually with differential expression data?__  
They usually want to find the top up regulated genes and the top down regulated genes.

Let's do it!!

Where do we start?
1. We want to make sure we are only looking at data points that are statically signifant, p-value > 0.001.  
  a. [Sort file by p-value](sort_by_pvalue/README.md)  
  b. [Keep only the lines that have a p-value > 0.001](significant_only/README.md).  

2. Now let's find our most up- and down- regulated genes. Which means we need to sort the log2foldchage column (4th column)  
 a. [Sort file by log2foldchange](sort_log2fold/README.md)  
 b. [Get the top 100 up/down-regulated genes](sort_log2fold/README.md#get-the-extremes)   
 c. [Get a list of all the genes with the most signifant changes](sort_log2fold/README.md#most-signficant-changes)   
 d. [Do it a different way](sort_log2fold/README.md#other-way-to-do-the-same)   


__Now what are these genes?__  
Here is where we are going to mine data from Ensembl biomart. Biomart is a SUPER handy tool if your organims is in Ensembl. Ensembl has 5 different sites for different groups of organisms. 

Ensembl (veterbrates)
Ensembl Plant
Ensembl Fungi
Ensembl Bacteria
Ensembl Metazoa

Let's find out more about chicken genes using Ensembl's BioMart tool

1. Retieve the gene ID, gene name, gene description, and interporscan ID, short description, and description for every chicken gene. [Need Help?](biomart_get_gene_info/README.sh)
2. [Pull out gene information about out upregulated genes.](gene_info_upregulated/README.md)


__Are any involved in a process I am super interested in?__  
Of our most signficant up- and down-regualted genes, are any involved in stem cell proliferation (GO:0072089) or pigmenation (GO:0043473)?

1. Get a list of genes involved in stem cell proliferation (GO:0072089). [Need Help](biomart_get_gene_and_go_info/README.sh)
2. Are any of our up-regulated also in our list of genes involved in stem cell proliferation?  [Need Help](biomart_get_gene_and_go_info/README.sh#upregulated_and_stem_cell_proliferation)

