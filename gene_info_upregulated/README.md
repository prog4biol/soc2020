# Gene info for upregulated genes

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
