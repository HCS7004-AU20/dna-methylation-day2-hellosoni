## Differential Methylation Analysis

The next step in the analysis pipeline following alignment and methylation calling using Bismark is to perform differential methylation analysis.
There are several pieces of software available to do this analysis, each with their own limitations and assumptions.
We will utilize the R package DSS to perform our analysis.

```cd /fs/scratch/PAS1752/osu9453/EpigeneticsLab/ExtractedMethylationFiles_BedReport```
```mkdir DSS_Analysis```

We're going to work with the bismark coverage files to create files for input into DSS.

As run, the bismark coverage file contains only information on CG context cytosines.

```gunzip *.bismark.cov.gz```
```awk 'BEGIN {FS="\t"}; {print $1, $2, $5+$6, $5}' FlowerRep1_R1.deduplicated.bismark.cov > DSS_Analysis/FlowerRep1_DSS.txt```

Repeat the above command for each flower and leaf bismark.cov file.

Install needed packages in R. To do this, start an instance of R.

```module load R/0.4.2-gnu9.1```
```R```
```install.packages("BiocManager")```
```BiocManager::install("DSS")```

After DSS is installed, quit out of R.

Move to your scripts directory and create a new directory called Rscripts.

```mkdir RScripts```

In the current directory, copy my script called: DSS_Rscript.sh

```cp /fs/scratch/PAS1752/osu9453/EpigeneticsLab/scripts/DSS_Rscript.sh .```

Then move into your RScripts dirctory and copy the script: DSS_Script_CG.R

```cd RScripts ```
```cp /fs/scratch/PAS1752/osu9453/EpigeneticsLab/scripts/RScripts/DSS_Script_CG.R .```

Move back into the scripts folder and submit DSS_RScript.sh as a job to OSC:
```cd ..```
```qsub DSS_RScript.sh```
