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

[MLST](https://github.com/tseemann/mlst) and detection of AMR mechanisms is also undertaken, using [abritamr](https://github.com/MDU-PHL/abritamr) on all sequences which pass the quality assessment. 

## Core genome MLST

Core genome MLST is used to group sequences into cgMLST groups for further detailed analysis. This approach allows for maximisation of core genome recovery and high resolution interpretations of relatedness to aid in informing the degree of relatedness.

cgMLST as implemented by the ANAT, utilises a [scheme of 3016](https://zenodo.org/records/1323684) genes and the allele calling tool [chewBBACA](https://chewbbaca.readthedocs.io/en/latest/user/getting_started/overview.html) to detect profiles.

Only sequences which have >90% alleles detected are used in further analysis.

Distances between profiles is calculated with cgmlst-dists (v1.2.0) and these distances are clustered using heirarchical complete linkage with a 50 allele threshold. This method identifies groups where all sequences within the group are <= 50 alleles from every other sequence in the group.

## Core SNP analysis

For each cgMLST group (cgT) which contains >= 5 sequences a comparative core genome SNP analysis is undertaken using the reference genome NC 011294.1 Salmonella enterica subsp. enterica serovar Enteritidis str. P125109. 

Paired-end reads are aligned, variants identified and a core genome calculated using [snippy](https://github.com/tseemann/snippy). Pairwise SNP distances and phylogenetic trees are calculated using [snp-dists](https://github.com/tseemann/snpdists).

## Interpetation of genomic relatedness

For each cgT, heirarchical singl-linkage clustering with a 5 SNP treshold is used to determine the degree of genomic relatedness. This threshold has been shown to identify epidemiologically relevant relationships. Single-linkage clustering identifies groups of sequences which are <= 5 SNPs from at least one other sequence in the cgT.

## Software versions

All tools (except cgMLST) are implemented within the [bohra pipeline](https://mdu-phl.github.io/bohra/) v 3.4.3
|Tool| Version | Reference	| Database |
|:-- |:-- | :-- | :-- |
| chewBBACA | v 2.16.0 | Publication - https://academic.oup.com/nar/article/49/D1/D660/5929238?login=false Tool - https://chewbbaca.readthedocs.io/en/latest/user/getting_started/overview.html | https://zenodo.org/records/1323684 downloaded 2023-10-01 | 
|seqkit	| seqkit v2.12.0 | Publication - https://doi.org/10.1002/imt2.191 Tool - https://bioinf.shenwei.me/seqkit/	||
| kmc| K-Mer Counter (KMC) ver. 3.2.4 (2024-02-09)	| Publication - https://doi.org/10.1093/bioinformatics/btx304 Tool - https://github.com/refresh-bio/KMC	||		
| shovill|	shovill 1.4.2	| Tool - https://github.com/tseemann/shovill	||
|kraken2 |Kraken version 2.17.1	| Publication - https://doi.org/10.1186/s13059-019-1891-0 Tool - https://github.com/DerrickWood/kraken2	| /opt/resources/k2_pluspfp_20240605|
|abritamr	|abritamr 1.0.20 | Publication - https://doi.org/10.1038/s41467-022-35713-4 Tool - https://zenodo.org/records/12514579	||
| mobsuite	| 	mob_recon 3.1.9	| Publication - https://doi.org/10.1099/mgen.0.000435 Tool - https://github.com/phac-nml/mob-suite ||	
| mlst	| 	mlst 2.19 | Tool - https://github.com/tseemann/mlst	||
| sistr	|	(sistr 1.1.1) | Tool - https://github.com/phac-nml/sistr_cmd ||

