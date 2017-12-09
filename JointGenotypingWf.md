## Workflow overview

This WDL pipeline implements joint calling across multiple samples according to the GATK Best Practices (June 2016) for germline SNP and Indel discovery in human whole-genome sequencing (WGS) data.

### Data requirements/expectations :
- One or more human whole-genome per-sample GVCF files

### List of Generated Outputs: 

VCF Output Files
- output vcf
- output vcf index

VCF Metrics
- detail_metrics file
- summary metrics file

Output the interval list generated/used by this run workflow
- output intervals

### Version notes

This is a pre-release version of the pipeline which does not include a fully runnable example dataset. 

