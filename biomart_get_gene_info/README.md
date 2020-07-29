# Use BioMart to get gene info 

Retieve the gene ID, gene name, gene description, and interporscan ID, short description, and description for every chicken gene.


1. Go to [Ensembl](http://www.ensembl.org)  
2. Click link to [BioMart](http://www.ensembl.org/biomart/martview)  
3. Choose Database --> Ensembl Genes 100 (this is the current version)  
4. Choose Dataset --> Chicken genes (GRCg6a)  
5. Change Attributes:  
   a. Click "Attibutes" 
   b. Expand "GENE:"  
   c. Deselect 
      *  "Gene stable ID"  
      * "Transcript stable ID"  
      * "Transcript stable ID verion" 
   d. Should only have "Gene Stable ID version" selected
6. Add Attributes:  
   a. Select "Gene description"  
   b. Select "Gene name"
7. Add Additonal Attributes:  
   a. Scroll Down. 
   b. Expand "PROTEIN DOMAINS AND FAMILIES:"  
   c. Select "Interpro ID"  
   d. Select "Interpro Short Description"  
   e. Select "Interpro Decription" 
8. Retrieve results  
   a. Click the "Results" button near the top left.
   b. Check Unique results only once results appear.  
   c. We want to download TSV to a file, which is default, so Click the "GO" button.  
   d. Wait, Download called "mart_export.txt" will be in your downloads location.  
   e. Copy mart_export.txt to the location with your expression data.   
      * for me, will likely be different for you: `mv ~/Downloads/mart_export.txt ~/Desktop/soc2020/.` 

