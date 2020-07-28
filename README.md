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
  a. [Sort file by p-value](1_sort_by_pvalue/README.md)  
  b. [Keep only the lines that have a p-value > 0.001](2_significant_only/README.md).  

2. Now let's find our most up- and down- regulated genes. Which means we need to sort the log2foldchage column (4th column)  
 a. [Sort file by log2foldchange](3_sort_log2fold/README.md)  
 b. [Get the top 100 up/down-regulated genes](3_sort_log2fold/README.md#get-the-extremes)   
 c. [Get a list of all the genes with the most signifant changes](#most-signficant-changes)   
 d. [Do it a different way](3_sort_log2fold/README.md#other-way-to-do-the-same)   


__Now what are these genes?__  
Here is where we are going to mine data from Ensembl biomart. Biomart is a SUPER handy tool if your organims is in Ensembl. Ensembl has 5 different sites for different groups of organisms. 

Ensembl (veterbrates)
Ensembl Plant
Ensembl Fungi
Ensembl Bacteria
Ensembl Metazoa

Let's find out more about chicken genes using Ensembl's BioMart tool

PUT STEP BY STEP IN NEW README

Let's get gene info.
I want to get the gene ID, name, description, and IPRSCAN domain info for every chicken gene. Here is how you do this with BioMart.


1. Go to [Ensembl](http://www.ensembl.org)  
2. Click link to [BioMart](http://www.ensembl.org/biomart/martview)  
3. Choose Database --> Ensembl Genes 100 (this is the current version)  
4. Choose Dataset --> Chicken genes (GRCg6a)  
5. Change Attributes:  
  a. Click "Attibutes" 
  b. Expand "GENE:"  
  c. Deselect 
  	i. "Gene stable ID"  
	ii. "Transcript stable ID"  
  	iii. "Transcript stable ID verion" 
  d. Should only have "Gene Stable ID version" selected
6. Add Attributes:  
	i. Select "Gene description"
	ii. Select "Gene name"
7. Add Additonal Attributes:  
  a. Scroll Down. 
  b. Expand "PROTEIN DOMAINS AND FAMILIES:"  
  c. Select "Interpro ID"  
  d. Select "Interpro Short Description"  
  e. Select "Interpro Decription" 
8. Retrieve results  
  a. Click the "Results" button near the top left.
  b. Check Unique results only once results appear
  c. We want to download TSV to a file, which is default, so Click the "GO" button.  
  d. Wait, Download called "mart_export.txt" will be in your downloads location.
  e. Copy mart_export.txt to the location with your expression data. 
	i. for me, will likely be different for you: `mv ~/Downloads/mart_export.txt ~/Desktop/soc2020/.` 

Review information about my upregulated genes.

PUT STEP BY STEP IN NEW README

Get just the IDs to use with `grep`
```
$ cut -f 1 up2.tsv > up2ids.txt
```

Use grep to pull out the genes that >= 2 log2foldchage from the the complete gene info file.
```
$ grep -f up2ids.txt mart_export.txt | head
ENSGALG00000006388.7	interleukin 16 [Source:NCBI gene;Acc:374270]	IL16	IPR001478	PDZ	PDZ domain
ENSGALG00000006388.7	interleukin 16 [Source:NCBI gene;Acc:374270]	IL16	IPR020450	IL-16	Interleukin-16
ENSGALG00000006388.7	interleukin 16 [Source:NCBI gene;Acc:374270]	IL16	IPR036034	PDZ_sf	PDZ superfamily
ENSGALG00000010770.7	scinderin [Source:NCBI gene;Acc:420588]	SCIN	IPR007122	Villin/Gelsolin	Villin/Gelsolin
ENSGALG00000010770.7	scinderin [Source:NCBI gene;Acc:420588]	SCIN	IPR007123	Gelsolin-like_dom	Gelsolin-like domain
ENSGALG00000010770.7	scinderin [Source:NCBI gene;Acc:420588]	SCIN	IPR029006	ADF-H/Gelsolin-like_dom_sf	ADF-H/Gelsolin-like domain superfamily
ENSGALG00000010770.7	scinderin [Source:NCBI gene;Acc:420588]	SCIN	IPR030012	Adseverin	Adseverin
ENSGALG00000010770.7	scinderin [Source:NCBI gene;Acc:420588]	SCIN	IPR036180	Gelsolin-like_dom_sf	Gelsolin-like domain superfamily
ENSGALG00000014730.7	ELOVL fatty acid elongase 7 [Source:NCBI gene;Acc:431579]	ELOVL7	IPR002076	ELO_fam	ELO family
ENSGALG00000014730.7	ELOVL fatty acid elongase 7 [Source:NCBI gene;Acc:431579]	ELOVL7	IPR030457	ELO_CS	ELO family, conserved site
```

You can do the same with the down-regulated genes.
```
$ cut -f 1 dn-2.tsv > dn-2ids.txt
$ grep -f dn-2ids.txt mart_export.txt | head
ENSGALG00000016736.6	cytoplasmic FMR1 interacting protein 1 [Source:NCBI gene;Acc:418677]	CYFIP1	IPR008081	Cytoplasmic_FMR1-int	Cytoplasmic FMR1-interacting
ENSGALG00000016736.6	cytoplasmic FMR1 interacting protein 1 [Source:NCBI gene;Acc:418677]	CYFIP1	IPR009828	DUF1394	Protein of unknown function DUF1394
ENSGALG00000030229.2	CUB and Sushi multiple domains 2 [Source:NCBI gene;Acc:419640]	CSMD2	IPR000436	Sushi_SCR_CCP_dom	Sushi/SCR/CCP domain
ENSGALG00000030229.2	CUB and Sushi multiple domains 2 [Source:NCBI gene;Acc:419640]	CSMD2	IPR000859	CUB_dom	CUB domain
ENSGALG00000030229.2	CUB and Sushi multiple domains 2 [Source:NCBI gene;Acc:419640]	CSMD2	IPR035914	Sperma_CUB_dom_sf	Spermadhesin, CUB domain superfamily
ENSGALG00000030229.2	CUB and Sushi multiple domains 2 [Source:NCBI gene;Acc:419640]	CSMD2	IPR035976	Sushi/SCR/CCP_sf	Sushi/SCR/CCP superfamily
ENSGALG00000039826.2	cyclic nucleotide gated channel alpha 3 [Source:NCBI gene;Acc:396144]	CNGA3	IPR000595	cNMP-bd_dom	Cyclic nucleotide-binding domain
ENSGALG00000039826.2	cyclic nucleotide gated channel alpha 3 [Source:NCBI gene;Acc:396144]	CNGA3	IPR005821	Ion_trans_dom	Ion transport domain
ENSGALG00000039826.2	cyclic nucleotide gated channel alpha 3 [Source:NCBI gene;Acc:396144]	CNGA3	IPR014710	RmlC-like_jellyroll	RmlC-like jelly roll fold
ENSGALG00000039826.2	cyclic nucleotide gated channel alpha 3 [Source:NCBI gene;Acc:396144]	CNGA3	IPR018488	cNMP-bd_CS	Cyclic nucleotide-binding, conserved site
```

__Are any involved in a process I am super interested in?__  
Of our most signficant up- and down-regualted genes, are any involved in stem cell proliferation (GO:0072089) or pigmenation (GO:0043473)?

```
$ grep -f up2ids.txt  proliferation_mart_export.txt
ENSGALG00000040493	ENSGALG00000040493.2	pleiotrophin [Source:NCBI gene;Acc:418125]	GO:0007406	negative regulation of neuroblast proliferation

$ grep -f dn-2ids.txt  proliferation_mart_export.txt
ENSGALG00000039861	ENSGALG00000039861.2	plexin B2 [Source:NCBI gene;Acc:425938]	GO:0007405	neuroblast proliferation

$ grep -f up2ids.txt  pigmentation_mart_export.txt

$ grep -f dn-2ids.txt  pigmentation_mart_export.txt
ENSGALG00000040465	ENSGALG00000040465.2	zinc finger E-box binding homeobox 2 [Source:NCBI gene;Acc:424306]	GO:0045636	positive regulation of melanocyte differentiation
ENSGALG00000040465	ENSGALG00000040465.2	zinc finger E-box binding homeobox 2 [Source:NCBI gene;Acc:424306]	GO:0048066	developmental pigmentation
ENSGALG00000040465	ENSGALG00000040465.2	zinc finger E-box binding homeobox 2 [Source:NCBI gene;Acc:424306]	GO:1903056	regulation of melanosome organization
```

