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

__Where do we start?__
1. We want to make sure we are only looking at data points that are statically signifant, p-value > 0.001.  
  a. [Sort file by p-value](1_sort_by_pvalue/README.md)  
  b. [Keep only the lines that have a p-value > 0.001](2_significant_only/README.md).  

2. Now let's find our most up- and down- regulated genes. Which means we need to sort the log2fold column (4th column)  
 a. [Sort file by log2foldchange](3_sort_log2fold/README.md)  
 b.  [Get the top 100 up/down-regulated genes](3_sort_log2fold/README.md#get-the-extremes)   
 c.  [Do it a different way](3_sort_log2fold/README.md#other-way-to-do-the-same)   






## of the top 100 up and down, are any involved in stem cell proliferation (http://purl.obolibrary.org/obo/GO_0072089), pigmenation (http://purl.obolibrary.org/obo/GO_0043473)?

(base) mp181vbhv2j:E-MTAB-2754 smr$ grep -f up_reg.txt  proliferation_mart_export.txt
ENSGALG00000040493	ENSGALG00000040493.2	pleiotrophin [Source:NCBI gene;Acc:418125]	GO:0007406	negative regulation of neuroblast proliferation
(base) mp181vbhv2j:E-MTAB-2754 smr$ grep -f dn_reg.txt  proliferation_mart_export.txt
ENSGALG00000039861	ENSGALG00000039861.2	plexin B2 [Source:NCBI gene;Acc:425938]	GO:0007405	neuroblast proliferation
(base) mp181vbhv2j:E-MTAB-2754 smr$ grep -f dn_reg.txt  pigmentation_mart_export.txt
ENSGALG00000040465	ENSGALG00000040465.2	zinc finger E-box binding homeobox 2 [Source:NCBI gene;Acc:424306]	GO:0045636	positive regulation of melanocyte differentiation
ENSGALG00000040465	ENSGALG00000040465.2	zinc finger E-box binding homeobox 2 [Source:NCBI gene;Acc:424306]	GO:0048066	developmental pigmentation
ENSGALG00000040465	ENSGALG00000040465.2	zinc finger E-box binding homeobox 2 [Source:NCBI gene;Acc:424306]	GO:1903056	regulation of melanosome organization


awk -F "\t" '{if ($3 <= 1e-5 && $4 > 2) {print $1}}' E-MTAB-2754-analytics.tsv
awk -F "\t" '{if ($3 <= 1e-5 && $4 > 2) {print $1}}' E-MTAB-2754-analytics.tsv  | wc -l
      59

## BIOMART


Dataset
Chicken genes (GRCg6a)
Filters
[None selected]
Attributes
Gene stable ID version
Gene description
Gene name
Interpro ID
Interpro Short Description
Interpro Description
Dataset
[None Selected]

