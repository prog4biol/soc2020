https://www.ebi.ac.uk/gxa/home
# pick chicken
https://www.ebi.ac.uk/gxa/experiments?experimentType=differential&species=gallus+gallus
# pick E-MTAB-2754-analytics.tsv
# https://www.ebi.ac.uk/gxa/experiments-content/E-MTAB-2754/resources/DifferentialSecondaryDataFiles.RnaSeq/analytics

(base) mp181vbhv2j:E-MTAB-2754 smr$ head E-MTAB-2754-analytics.tsv
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

cat E-MTAB-2754-analytics.tsv | grep -v -e "\tNA\t" | sort -t$'\t' -k3 -g > sorted_by_p.tsv
# open file remove any lines that are larger that 0.001

(base) mp181vbhv2j:E-MTAB-2754 smr$  sort -t$'\t' -k4 sorted_by_p.tsv | head
ENSGALG00000004956	GPI	0.000716071813497406	-0.2
ENSGALG00000013726	PAICS	0.000641946257320909	-0.2
ENSGALG00000028851	RAB8A	0.000906523776344118	-0.2
ENSGALG00000000573	PER3	3.83839038727545e-06	-0.3
ENSGALG00000000777	EYA3	2.07370849415051e-05	-0.3
ENSGALG00000001024	TPRG1L	0.000101701679175278	-0.3
ENSGALG00000001231	SAMHD1	8.36393218354028e-05	-0.3
ENSGALG00000001253	RC3H2	2.11973648517545e-05	-0.3
ENSGALG00000001428	EFHD1	0.00080177461598348	-0.3
ENSGALG00000001501	MAPK3	1.88860781387958e-05	-0.3
(base) mp181vbhv2j:E-MTAB-2754 smr$  sort -t$'\t' -k4 -r sorted_by_p.tsv | head
Gene ID	Gene Name	g1_g2.p-value	g1_g2.log2foldchange
ENSGALG00000026591	GNG12	2.48713188587058e-106	5.1
ENSGALG00000006456	C14H16orf45	4.83210331845551e-134	4.3
ENSGALG00000053328		6.06296117790466e-59	4.2
ENSGALG00000016602	ARHGAP6	3.50644039913878e-72	4.2
ENSGALG00000002118	KCNMB1	4.08819738778984e-92	4
ENSGALG00000033941	RORC	4.14460236124194e-76	3.8
ENSGALG00000048302		9.7889149897967e-41	3.7
ENSGALG00000030602	ADAM33	8.84702727723148e-114	3.7
ENSGALG00000007416	CD3E	2.42674555681373e-48	3.6


cat E-MTAB-2754-analytics.tsv | grep -v -e "\tNA\t" | sort -t$'\t' -k3 -g | cat -n  |  more
## find your cutoff line ===> 2206

cat E-MTAB-2754-analytics.tsv | grep -v -e "\tNA\t" | sort -t$'\t' -k3 -g | head -n 2206

(base) mp181vbhv2j:E-MTAB-2754 smr$ cat E-MTAB-2754-analytics.tsv | grep -v -e "\tNA\t" | sort -t$'\t' -k3 -g | head -n 2206 | sort -t$'\t' -k4 -n -r sorted_by_p.tsv | head
ENSGALG00000026591	GNG12	2.48713188587058e-106	5.1
ENSGALG00000006456	C14H16orf45	4.83210331845551e-134	4.3
ENSGALG00000053328		6.06296117790466e-59	4.2
ENSGALG00000016602	ARHGAP6	3.50644039913878e-72	4.2
ENSGALG00000002118	KCNMB1	4.08819738778984e-92	4
ENSGALG00000033941	RORC	4.14460236124194e-76	3.8
ENSGALG00000048302		9.7889149897967e-41	3.7
ENSGALG00000030602	ADAM33	8.84702727723148e-114	3.7
ENSGALG00000007416	CD3E	2.42674555681373e-48	3.6
ENSGALG00000047182		8.49031135004632e-58	3.5
(base) mp181vbhv2j:E-MTAB-2754 smr$ cat E-MTAB-2754-analytics.tsv | grep -v -e "\tNA\t" | sort -t$'\t' -k3 -g | head -n 2206 | sort -t$'\t' -k4 -n  | head
ENSGALG00000020078	H3F3C	0	-8
ENSGALG00000002286	H3F3B	0	-7
ENSGALG00000039102	TOX	3.14377780904377e-137	-5.3
ENSGALG00000005610	SLC44A3	2.67237306894498e-109	-4.8
ENSGALG00000048035	GCNT2	4.81421762236255e-69	-4.5
ENSGALG00000027365	HIVEP3	1.55554665427949e-117	-4.1
ENSGALG00000031768	SPO11	3.97130937569517e-59	-3.9
ENSGALG00000039264	SLA	3.3960317531256e-97	-3.9
ENSGALG00000016906	SPRY2	7.1093323557451e-55	-3.8
ENSGALG00000027353	C10orf71	1.29880461971355e-212	-3.7



cat E-MTAB-2754-analytics.tsv | grep -v -e "\tNA\t" | sort -t$'\t' -k3 -g | head -n 2206 | sort -t$'\t' -k4 -n | head -100  | cut -f 1 > dn_reg.txt
cat E-MTAB-2754-analytics.tsv | grep -v -e "\tNA\t" | sort -t$'\t' -k3 -g | head -n 2206 | sort -t$'\t' -k4 -n -r  | head -100  | cut -f 1 > up_reg.txt
grep -f up_reg.txt mart_export.txt
grep -f dn_reg.txt mart_export.txt


## just top 10
head -10 up_reg.txt > top10_up_reg.txt
head -10 dn_reg.txt > top10_dn_reg.txt


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

