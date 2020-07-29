# Find up- and down- regulated genes

To find the most up/down-regulated genes we will have to sort by the 4th column, the log2foldchange column

Make sure to start with the data sorted and filted by pvalue significance (pvalue_sorted_significant_only.tsv). 

## Review 4th column (log2foldchange)
Check the 4th column to make sure there are no unexpected values:
```
$ cut -f 4 pvalue_sorted_significant_only.tsv | sort | uniq
-0.2
-0.3
-0.4
-0.5
-0.6
-0.7
-0.8
-0.9
-1
-1.1
-1.2
-1.3
-1.4
-1.5
-1.6
-1.7
-1.8
-1.9
-2
-2.1
-2.2
-2.3
-2.4
-2.5
-2.6
-2.7
-2.9
-3
-3.1
-3.3
-3.4
-3.5
-3.6
-3.7
-3.8
-3.9
-4.1
-4.5
-4.8
-5.3
-7
-8
0.2
0.3
0.4
0.5
0.6
0.7
0.8
0.9
1
1.1
1.2
1.3
1.4
1.5
1.6
1.7
1.8
1.9
2
2.1
2.2
2.3
2.4
2.5
2.6
2.7
2.8
2.9
3
3.1
3.2
3.3
3.4
3.5
3.6
3.7
3.8
4
4.2
4.3
5.1
g1_g2.log2foldchange
``` 
  - After a quick reveiw of the 4th column, there are no scientific notations we can sort with a simple numeric sort.

## Sort by log fold change
Let's sort and check the top and bottom of our file to make sure we are getting what we expect:
```
$  sort -t$'\t' -k4 -n pvalue_sorted_significant_only.tsv |  head
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
```
 - Looks good. Values looks like they are correctly sorted from smallest to largest at the top of the file

Check the bottom or tail of the file to be sure it is sorted properly:
```
$  sort -t$'\t' -k4 -n pvalue_sorted_significant_only.tsv |  tail
ENSGALG00000047182		8.49031135004632e-58	3.5
ENSGALG00000007416	CD3E	2.42674555681373e-48	3.6
ENSGALG00000030602	ADAM33	8.84702727723148e-114	3.7
ENSGALG00000048302		9.7889149897967e-41	3.7
ENSGALG00000033941	RORC	4.14460236124194e-76	3.8
ENSGALG00000002118	KCNMB1	4.08819738778984e-92	4
ENSGALG00000016602	ARHGAP6	3.50644039913878e-72	4.2
ENSGALG00000053328		6.06296117790466e-59	4.2
ENSGALG00000006456	C14H16orf45	4.83210331845551e-134	4.3
ENSGALG00000026591	GNG12	2.48713188587058e-106	5.1
```
  - The file is sorted from smalled to largest values, just as we wanted.

Let's create a new file with our data sorted by log fold change:
```
$  sort -t$'\t' -k4 -n pvalue_sorted_significant_only.tsv > logfold_sorted.tsv
```

## Get the extremes

Now we need to decide if we want the top 100 down-regulated and the top 100 up-regulated or if we want to keep everything below and above a specific cut off. Let's do both. We will start with the simplest.

What are the top 100 down-regulated genes?

Use the file sorted by log2foldchange column (logfold_sorted.tsv) and save the top 100 lines:
```
$ head -n100 logfold_sorted.tsv > top_100_dn_regulated.tsv 
```

Check it! Use head to make sure the top of your new files looks like you expect:
```
$ head top_100_dn_regulated.tsv
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
```
  - Look's like we expect! Log fold change values are decreasing.

Make sure there are the correct number of lines: 
```
$ wc -l top_100_dn_regulated.tsv
     100 top_100_dn_regulated.tsv
```
  - And we have 100 lines!


What are the top 100 up-regulated genes?

Use the file sorted by log2foldchange column (logfold_sorted.tsv) and save the last 100 lines:
```
$ tail -n100 logfold_sorted.tsv | head
ENSGALG00000027961	PCASP2	1.69866188570141e-31	1.7
ENSGALG00000031812	TDRKH	4.17455719510327e-08	1.7
ENSGALG00000041611		6.67942448720794e-08	1.7
ENSGALG00000045199		1.15620475223544e-20	1.7
ENSGALG00000047074		1.35431345591457e-08	1.7
ENSGALG00000002132	KCNIP1	2.54918606842974e-10	1.8
ENSGALG00000005930	PLS3	6.03343167838705e-33	1.8
ENSGALG00000006242	PABPN1L	5.07074337575948e-09	1.8
ENSGALG00000006507	CLMP	1.36964186239542e-24	1.8
ENSGALG00000009606		9.40765240007633e-09	1.8
$ tail -n100 logfold_sorted.tsv | tail
ENSGALG00000047182		8.49031135004632e-58	3.5
ENSGALG00000007416	CD3E	2.42674555681373e-48	3.6
ENSGALG00000030602	ADAM33	8.84702727723148e-114	3.7
ENSGALG00000048302		9.7889149897967e-41	3.7
ENSGALG00000033941	RORC	4.14460236124194e-76	3.8
ENSGALG00000002118	KCNMB1	4.08819738778984e-92	4
ENSGALG00000016602	ARHGAP6	3.50644039913878e-72	4.2
ENSGALG00000053328		6.06296117790466e-59	4.2
ENSGALG00000006456	C14H16orf45	4.83210331845551e-134	4.3
ENSGALG00000026591	GNG12	2.48713188587058e-106	5.1
```
 - Hmm. That isn't quite the order we want, right.   
 - The top or head of our list is not in the order we want.  
 -  We want the most up-regulated at the top.

Let's get the top 100 up-regulated genes sorted with the most up-regulated on top.

Get the bottom 100 lines, then reverse the order:
```
$ tail -r -n100 logfold_sorted.tsv | head
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
$ tail -r -n100 logfold_sorted.tsv | tail
ENSGALG00000009606		9.40765240007633e-09	1.8
ENSGALG00000006507	CLMP	1.36964186239542e-24	1.8
ENSGALG00000006242	PABPN1L	5.07074337575948e-09	1.8
ENSGALG00000005930	PLS3	6.03343167838705e-33	1.8
ENSGALG00000002132	KCNIP1	2.54918606842974e-10	1.8
ENSGALG00000047074		1.35431345591457e-08	1.7
ENSGALG00000045199		1.15620475223544e-20	1.7
ENSGALG00000041611		6.67942448720794e-08	1.7
ENSGALG00000031812	TDRKH	4.17455719510327e-08	1.7
ENSGALG00000027961	PCASP2	1.69866188570141e-31	1.7
```
 - That is what we want!!  

Let's save the top 100 up-regulated genes: 
```
$ tail -r -n100 logfold_sorted.tsv > top_100_up_regulated.tsv
```


## Most signficant changes
Now let's get only that genes that have a large difference between the two conditons, based on the value of the log fold change.


Let's find and keep the genes that are significantly down-regulated, log2foldchange <= -2. Filter, or remove all lines that are > -2. 

Find the line number of the last line we want to keep:
```
cat -n top_100_dn_regulated.tsv | more
...
...
    49  ENSGALG00000035317      ID3     6.84555438556063e-30    -2
    50  ENSGALG00000039659              2.30629226416736e-11    -2
    51  ENSGALG00000040709              1.46034631555571e-23    -2
    52  ENSGALG00000002832      IFI35   1.71911726670551e-13    -1.9
    53  ENSGALG00000008850      TTLL7   9.76473174841786e-25    -1.9
    54  ENSGALG00000009172      OSBPL6  6.1254332770914e-82     -1.9
    55  ENSGALG00000010820      CHGA    1.00820079319201e-12    -1.9
```
 - Line 51 is the last line we want to keep.

Save the first 51 lines in a new file: 
```
$ head -n51 top_100_dn_regulated.tsv > dn-2.tsv
```

Check the file:
```
$ tail dn-2.tsv
ENSGALG00000008970	NRK	7.15258964094999e-58	-2
ENSGALG00000011024	CACHD1	4.31012629122905e-11	-2
ENSGALG00000011566	GYPC	1.43308550743335e-10	-2
ENSGALG00000016486	HS1BP3	8.43645568986891e-17	-2
ENSGALG00000017196	ARHGAP42	1.07083394031599e-15	-2
ENSGALG00000029834	AIF1L	7.76152676954634e-36	-2
ENSGALG00000030011	ZNF704	3.02544663072825e-127	-2
ENSGALG00000035317	ID3	6.84555438556063e-30	-2
ENSGALG00000039659		2.30629226416736e-11	-2
ENSGALG00000040709		1.46034631555571e-23	-2

$ wc -l dn-2.tsv
      51 dn-2.tsv
```


Now let's get the up-regulated genes, genes that have a log 2 fold change >= 2. Filter all the lines that are < 2.

Find the line number of the last line we want to keep:
```
$ cat -n top_100_up_regulated.tsv | more
...
...
    64  ENSGALG00000007596              2.95507709620223e-24    2
    65  ENSGALG00000006388      IL16    3.39670658139579e-77    2
    66  ENSGALG00000006318      IL21R   5.03533323722168e-16    2
    67  ENSGALG00000005402      DYNLRB2 7.15311215516991e-13    2
    68  ENSGALG00000046032      CD83    2.57171759140107e-12    1.9
    69  ENSGALG00000045581              3.12593472351979e-29    1.9
    70  ENSGALG00000045021              3.73801211076943e-10    1.9
    71  ENSGALG00000043728              8.30858747493683e-16    1.9
``` 
 - Line 67 is the last data point we want to keep

Save the first 67 lines in a new file: 
```
$ head -n67 top_100_up_regulated.tsv > up2.tsv
$ head up2.tsv
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
```

Check the file:  
```
$ tail up2.tsv
ENSGALG00000021271	MPZL3	9.81852164392542e-12	2.1
ENSGALG00000006112	SCN5A	1.44173131129112e-12	2.1
ENSGALG00000037611		1.81097665316164e-60	2
ENSGALG00000017644	COTL1	1.53876630297694e-120	2
ENSGALG00000017362	HAVCR1	4.31293464069193e-38	2
ENSGALG00000007868	BCO2	6.8435018149788e-11	2
ENSGALG00000007596		2.95507709620223e-24	2
ENSGALG00000006388	IL16	3.39670658139579e-77	2
ENSGALG00000006318	IL21R	5.03533323722168e-16	2
ENSGALG00000005402	DYNLRB2	7.15311215516991e-13	2

```
 - Just want we wanted!!


## Other way to do the same

Want to see one line to get all this from the first unmanipulated file?

Use `awk` to keep only the lines in the 3rd column (pvalue) that have values that are < 0.001 AND have values in the 4th column (log2foldchange) that are >= 2 THEN print the 1st column (gene ID) and the 4th column (log2foldchange), THEN sort by the new 2nd column (log2foldchage): 
```
$ awk -F "\t" '{if ($3 < 0.001 && $4 >= 2) {print $1 "\t" $4}}' E-MTAB-2754-analytics.tsv | sort -k2 -n -r  | head
ENSGALG00000026591	5.1
ENSGALG00000006456	4.3
ENSGALG00000053328	4.2
ENSGALG00000016602	4.2
ENSGALG00000002118	4
ENSGALG00000033941	3.8
ENSGALG00000048302	3.7
ENSGALG00000030602	3.7
ENSGALG00000007416	3.6
ENSGALG00000047182	3.5
```
Let's compare:
```
$ head up2.tsv | cut -f 1,4
ENSGALG00000026591	5.1
ENSGALG00000006456	4.3
ENSGALG00000053328	4.2
ENSGALG00000016602	4.2
ENSGALG00000002118	4
ENSGALG00000033941	3.8
ENSGALG00000048302	3.7
ENSGALG00000030602	3.7
ENSGALG00000007416	3.6
ENSGALG00000047182	3.5

```

!!!!!!! Yikes!! The same results, one line instead of many. The commmand line is awesome!!!
