# prod-wgs-germline-snps-indels
### Purpose : 
Workflows used in production at Broad for germline short variant discovery in WGS data. 

### PairedSingleSampleWF :
This WDL pipeline implements data pre-processing and initial variant calling (GVCF
generation) according to the GATK Best Practices (June 2016) for germline SNP and
Indel discovery in human whole-genome sequencing (WGS) data.

#### Requirements/expectations
- Human whole-genome pair-end sequencing data in unmapped BAM (uBAM) format
- One or more read groups, one per uBAM file, all belonging to a single sample (SM)
- Input uBAM files must additionally comply with the following requirements:
- - filenames all have the same suffix (we use ".unmapped.bam")
- - files must pass validation by ValidateSamFile
- - reads are provided in query-sorted order
- - all reads must have an RG tag
- Reference genome must be Hg38 with ALT contigs
#### Outputs 
- Cram, cram index, and cram md5 
- GVCF and its gvcf index 
- BQSR Report
- Several Summary Metrics 

### joint-discovery-gatk :
The second WDL implements the joint discovery and VQSR 
filtering portion of the GATK Best Practices (June 2016) for germline SNP and Indel 
discovery in human whole-genome sequencing (WGS) and exome sequencing data.

#### Requirements/expectations
- One or more GVCFs produced by HaplotypeCaller in GVCF mode.
- Bare minimum 1 WGS sample or 30 Exome samples. Gene panels are not supported.
#### Outputs 
- VCF  and its vcf index
 *Note: The gvcf is filtered using variant quality score recalibration  
  (VQSR) with genotypes for all samples present in the input VCF. All sites that  
  are present in the input VCF are retained; filtered sites are annotated as such  
  in the FILTER field.*
- Summary Metrics

### Software version requirements :
- GATK 4.beta.3 or later 
- Picard 2.x
- Samtools (see gotc docker)
- Python 2.7

Cromwell version support 
- Successfully tested on v29
- Does not work on versions < v23 due to output syntax
