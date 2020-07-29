# Are any of my most up or down regulated genes involved in stem cell proliferation or pigmentation?

Of our most signficant up- and down-regualted genes, are any involved in stem cell proliferation (GO:0072089) or pigmenation (GO:0043473)?

Get a list of genes involved in stem cell proliferation (GO:0072089)

Let's go back to ensembl. Hopefully you have your gene info download still open.

1. Click 'Attibutes' 
2. Make sure only these are selected:  
  a. "gene stable ID version"  
  b. "Gene description"  
  c. "Gene Name"  
  d. "External" --> GO --> "GO term accession"  
  e. "External" --> GO --> "GO term name"
3. Click 'Filters'  
4. Expand "GENE ONTOLOGY"
5. Type or Copy GO:0072089 into the text box.
6. Click "Results" in the top left.  
7. Notice that not all the GO term IDs are 'GO:0072089'. Children terms, terms that are 'stem cell proliferation' are also appearing
7. Export all results to "File" TSV format   
8. Check "Unique results only"  
9. Select "Go"
10. move downloaded file to your working directory.  
  a. for me, probably different for you: `mv ~/Downloads/mart_export.txt ~/Desktop/soc2020/proliferation_mart_export.txt`

Do the same for pigmentation --> GO:0043473 


## upregulated and stem cell proliferation

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

