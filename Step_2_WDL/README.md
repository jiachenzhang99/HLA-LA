# Workflow Overview

The `hla_la_wf.wdl` workflow wraps the HLA-LA Docker container from step 1 (`jiachenzdocker/hla-la:latest`) to provide a scalable solution for HLA typing on cloud platforms. The workflow:

- Takes CRAM/BAM files and reference genome as input
- Runs HLA-LA typing using the containerized environment
- Outputs best HLA allele calls and all possible alleles


## Required Inputs

| Input | Description |
| --- | --- |
| `cram_file` | Input CRAM or BAM file containing sequencing reads |
| `cram_index` | Index file for the CRAM/BAM (.crai or .bai) |
| `ref_genome` | Reference genome FASTA file (e.g., Homo_sapiens_assembly38.fasta.gz) https://github.com/broadinstitute/gatk/raw/master/src/test/resources/large/Homo_sapiens_assembly38.fasta.gz |
|`ref_genome_index` | Reference genome index (.fai file) https://github.com/broadinstitute/gatk/raw/master/src/test/resources/large/Homo_sapiens_assembly38.fasta.gz.fai |
| `ref_genome_gzi` | Reference genome gzip index (.gzi file) https://github.com/broadinstitute/gatk/raw/master/src/test/resources/large/Homo_sapiens_assembly38.fasta.gz.gzi |
| `nr_threads` | Number of CPU threads to use for processing |

Note:

- CRAM and CRAI files are normally stored in the same folder under the `Bulk` folder.
- Adjust `nr_threads` input based on the defined `dx_instance_type` parameter in the .wdl file

## Expected Outputs

| Output | Description |
| --- | --- |
| `hla_best_guess` | Best HLA allele calls (G-group resolution) |
| `hla_all_alleles` | All possible HLA alleles with confidence scores |

Output files are named using the sample ID derived from the input CRAM filename:

- `{sample_id}_output_G.txt` - Best HLA calls
- `{sample_id}_output.txt` - All possible alleles
