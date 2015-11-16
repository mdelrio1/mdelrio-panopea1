# *Panopea* analysis of GOSlim without bacteria using Excel

From fileGeoduck-transcriptome-v3.faextract sequence names using Jupyter, follow notebook`fasta-to-tab-panopea.ipynb`
to obtain the sequences names in the file`Geoduck-transcriptome-v3-names.out`
In excel we need to create the file 
`Geoduck-transcriptome-v2-GO-SlimAnalisis.xlsx`
import file`Geoduck-transcriptome-v2-GO-Slim.csv`I changed the column headers using ncbi information on the format 6 and this pagehttp://www.metagenomics.wiki/tools/blast/blastn-output-format-6The original blast file output has 12 columns, but column2 (sseqid) has three values  separated by `|` so it was separated into three columns
`sseqid-1``sseqid-2``sseqid-3`the file should look like this
<center><img src="../img/Screen Shot PanopeaGO.png"/ width = 110%></center>
add the names in cells and formulas
|cell|content|
|----|-------||U1|contig||U2|=VALUE(MID(A2,5,FIND("_",A2)-5))|Copy formula down (double click in the righthandside of the cell)Transform formulas to values

## It is very important to save file every time you copy formulas and transform them into values. You are using a lot of RAM.	|cell|content|
|----|-------||V1|contigs||V2|=IF(U2=U1,V1+1,1)|Copy formula down (double click in the righthandside of the cell)	Transform formulas to values|cell|content|
|----|-------||W1|GOSlim_bin_rep||W2|=IF(R2="reproduction","reproduction",S2)|Copy formula down (double click in the righthandside of the cell)	Transform formulas to values	This formula considers the "term" from the GO, if it is "reproduction" then writes it in the cell. This formula can be change in order to have other terms (i. e. "death")|cell|content|
|----|-------||X1|seq||X2|=IF(A2=A1,"",1)|
Copy formula down (double click in the righthandside of the cell)	Transform formulas to values	This formula gives 1 only there is a change in the squence contig name. Data should be sorted.	name the sheet `Geoduck-transcriptome-v2-GOSlim`in a new sheet import the results from Jupyter, 	`Geoduck-transcriptome-v3-names.out`
select all contigs (remember the first row is "contigs", do not select it)	define a name range (insert, name, define) the name "datos" for the database (or other name)
name the sheet database	in Geoduck-transcriptome-v2-GOSlim sheet add column and formula as follows:
|cell|content|
|----|-------||Y1|nobacteria||Y2|=IF(VLOOKUP(A2,datos,1)=A2,W2,"")|
this formula looks for the presence of the GO slim data and if found writes the GOSlim term, if not, places a "blank"	
Formulas and data should look like this:<center><img src="../img/Screen Shot PanopeaGO4.png"/ width = 75%></center>
Build the pivot table using the columns	asdatabase	`Geoduck-transcriptome-v2-GOSlim'!$A$1:$Y$102359`you can place the pivot table in the same sheet or in a new one
Use	as follows in the pivot table:
`GOSlim_bin`		`rows`
`qseqid`		`values (count)`
this will give the following results
<center><img src="../img/Screen Shot PanopeaGO2.png"/ width = 75%></center>A second pivot table for reproduction	Build the pivot table using the columns	asdatabase	`Geoduck-transcriptome-v2-GOSlim'!$A$1:$Y$102359`you can place the pivot table in the same sheet or in a new one	Use	as follows in the pivot table:
`nobacteria`	`rows`
`qseqid`	`values (count)``seq`	`filter`		`change filter to 1`this will give the following results	<center><img src="../img/Screen Shot PanopeaGO3.png"/ width = 75%></center>
