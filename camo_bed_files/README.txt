# Description of Camo .bed Files

To run our camo variant rescue pipeline we provide three bed files for each genome build.
Following the description below, these three files can be used to call camo variants in 
CDS camo regions of the genome

All 3 .bed files contain the same column descriptions. 

The first 3 columns specify genomic coordinates

The fourth column contains a semi-colon delimited list of region_IDs. The first ID in 
the list is the region specified by that line's coordinates, all the other IDs are 
regions that are in the same cam group and are all camouflaged to each other

The fifth column shows repeat number for that camo group (number of times this 
camouflaged region is repeated)


## align_to.bed

Should be used in masking the genome to create a camo mask genome. Shows the one region in each
camo group where all reads for that group should align. This bed is expanded by 50 bp, complemented,
and then passed into bedtools maskFasta to mask reference

## realign.bed

Shows which regions should be realigned. Should be passed as input into samtools view -L option
to extract low quality MAPQ reads from camo regions

## GATK.bed

This bed specifies the interval GATK will use to call variants once the reads are realigned to 
the camo-masked genome. It is similar to the align_to.bed the only difference is the GATK.bed only
has CDS regions listed and is restricted to the actual camo boundaries and not the boundaries of the 
gene body element that contain the camo region. 
