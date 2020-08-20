# cath-hmm-hmm


# Natalie's step-by-step method for calculating pairwise FunFam similarity scores (based on Clemens')

Please note this work was done only in the context of CATH superfamily 1.50.10.20.

1. installed hh-suite at:

```
/cath/homes2/ucbtnld/github/hh-suite/
```

2. MAFFT step already done by Nico as using his v4.3 FunFams

3. attempted writing a snakefile for hhconsensus, hhmake, hhalign (only got the hhconsensus section to work - creates a3m files)

    * working directory: `/cath/people2/ucbtnld/projects/triterpene_synthase_grant/`
    * run snakefile in this directory

4. hhmake

```
$ FILES=/cath/people2/ucbtnb4/funfams-4.3/1.50.10.20/full_alignments/1.50.10.20-FF-*.faa
$ for file in $FILES; do b=`basename $file .faa`; hhmake -i $file -o hhsuite/${b}.hhm -M 50 -name $b; done
```

5. hhalign

```
HHMS=hhsuite/*.hhm
for hhmfile1 in $HHMS
do
    for hhmfile2 in $HHMS
    do
        if [ "$hhmfile1" != "$hhmfile2" ]
        then
            echo $hhmfile1 $hhmfile2
            a=`basename $hhmfile1 .hhm`
            b=`basename $hhmfile2 .hhm`
            hhalign -i $hhmfile1 -t $hhmfile2 -o hhsuite/${a}${b}.hhr 
        fi
    done
done
```
