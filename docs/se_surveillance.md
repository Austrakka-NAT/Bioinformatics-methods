# _Salmonella enterica_ Enteriditis surveillance


## Quality control

All sequences submitted to AusTrakka undergo quality assessment to determine the suitability of the sequences for further analysis.

| QC metric	| Criteria | Bioinformatics tool | 
|:-- | :-- | :-- |
|Species observed in sequence data |	Most abundant species Salmonella enterica | [kraken2](https://github.com/DerrickWood/kraken2) with latest [pluspf database](https://benlangmead.github.io/aws-indexes/k2) | 
| Serotype detected	| Enteritidis | [sistr](https://github.com/phac-nml/sistr_cmd) |
| Estimated genome size (reads) |	4.7 Mbp +/- 10% | [kmc](https://github.com/refresh-bio/KMC) | 
| Assembled genome size |	4.7 Mbp +/- 10% | [seqkit stats](https://github.com/shenwei356/seqkit) |
| Estimated average depth of coverage |	40x | number reads / esitmated genome size (reads)  |


Sequences which pass these criteria are used in downstream analsyis.

## Single sample results

MLST and detection of AMR mechanisms is also undertaken on all sequences which pass the quality assessment. 

## Core genome MLST

Core genome MLST is used to group sequences into cgMLST groups for further detailed analysis. This approach allows for maximisation of core genome recovery and high resolution interpretations of relatedness to aid in informing the degree of relatedness.

cgMLST as implemented by the ANAT, utilises a [scheme of 3016](https://zenodo.org/records/1323684) genes and the allele calling tool [chewBBACA](https://chewbbaca.readthedocs.io/en/latest/user/getting_started/overview.html) v2.6.0 to detect profiles.

Only sequences which have >90% alleles detected are used in further analysis.

Distances between profiles is calculated with cgmlst-dists (v1.2.0) and these distances are clustered using heirarchical complete linkage with a 50 allele threshold. This method identifies groups where all sequences within the group are <= 50 alleles from every other sequence in the group.

