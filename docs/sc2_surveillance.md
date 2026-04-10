# SARS-CoV-2 Surveillance


## Lineage assessment

Sequences submitted to AusTrakka are in the form of FASTA sequences, whereby uploaders only provide sequences that meet their own minimum required depth coverage. 

FASTA sequences are assessed through Nextclade with the latest dataset to determine lineage.


## Collapsing lineage 

The pango-collapse tool is used to make meaningful assessments of assigned lineages. 

For AusTrakka purposes, the lineages are collapsed twice; 1) to a "Family" level, equivalent to VOCs/VOIs, and 2) to circulating variants under monitoring (VUMs) as reported by the [WHO](https://www.who.int/activities/tracking-SARS-CoV-2-variants) 


## Phylogenetic tree

[Problematic sites](github.com/W-L/ProblematicSites_SARS-CoV2/blob/master/problematic_sites_sarsCov2.vcf) are masked before constructing a phylogenetic tree through [UShER](https://github.com/yatisht/usher)


## Quality control

All sequences submitted to AusTrakka undergo quality assessment to determine the suitability of the sequences for reporting.

| QC metric	| Criteria | Lineage Value | Bioinformatics tool | 
|:-- | :-- | :-- | :-- |
| Genome Coverage (%) | $\ge90$ | "LowCoverage" | [nextclade](https://github.com/nextstrain/nextclade) with the MN908947.3.fna reference| 
| Nextclade Quality Status | "bad" | "Unassigned" | [nextclade](https://github.com/nextstrain/nextclade) with the MN908947.3.fna reference| 

Any sequence that falls outside this range will be flagged as 'Low Coverage' or 'Unassigned' and will be excluded from phylogenetic analysis and reporting. 


## Software versions

All tools are implemented through the [austrakka-sc2-tree pipeline](https://github.com/AusTrakka/austrakka-sc2-tree) v 0.14.2

|Tool| Version | Reference	| Database |
|:-- |:-- | :-- | :-- |
| nextclade | v 3.3.1 | https://github.com/nextstrain/nextclade | latest through nextclade dataset get | 
| pango-collapse	| v 0.8.2 | https://github.com/MDU-PHL/pango-collapse	||
| phytest | v 1.3.0	| 	| |		
| usher | | https://github.com/yatisht/usher | |


