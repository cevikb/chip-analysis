# CHIP Analysis Workflow

**Version:** 1.0  
**Date:** October 2025  
**Author:** Burcu Cevik
**Contact:** <burcukcevik@gmail.com>  
**Project:** CHIP / Variant Calling Workflow (UK Biobank RAP)

---

## Overview
This repository documents a complete **variant calling and filtering pipeline** performed on the **UK Biobank Research Analysis Platform (RAP)**.  
All steps were executed using official RAP apps such as *Swiss Army Knife*, *Mutectcaller (Parabricks accelerated)*, and *SnpEff Annotate*.

---

## Tools and Software
- **Swiss Army Knife** (samtools, bcftools, tabix, grep; v1.21)
- **Mutectcaller (Parabricks accelerated)** — *nvidia_ukb*, v4.1.0  
- **SnpEff Annotate** — v2.1.2  
- **Reference genome:** GRCh38 / GRCh38.p13  
- **Environment:** UK Biobank RAP (GPU-enabled), Windows cmd.exe (for indexing)

---

## Workflow Summary

| Step | Description | Tool |
|------|--------------|------|
| **1** | Convert CRAM → BAM | Swiss Army Knife (samtools) |
| **2** | Extract read group (RG) info | samtools + grep |
| **3** | Package BWA reference index into `.tar.gz` | Windows cmd.exe |
| **4** | Variant calling (BAM → VCF) | Mutectcaller (Parabricks) |
| **5** | Variant annotation | SnpEff Annotate |
| **6** | Region-based variant filtering | bcftools |
| **7** | gnomAD v4.1 population filtering | bcftools + tabix |
| **8** | Compress and index filtered VCFs | bgzip + tabix |
| **9** | Exclude common variants using gnomAD reference | bcftools |
| **10** | Apply quality filters (DP, AD, AF thresholds) | bcftools |

---

## Notes
- All **sample identifiers** are anonymized (e.g., `sample_id`, `UKB_XXXXX_XXXXX`).  
- Real data are **not shared** due to UK Biobank policy.  
- Commands and versions are documented in separate code files within this repository.  

---

## Citation

If you use this workflow or adapt parts of it in your research, please cite the related publication:

Çevik B, et al. *Clonal hematopoiesis is associated with the risk of Alzheimer's disease in the UK Biobank APOE ε3/ε3 genotype cohort*. **Blood**. 2025.  
https://doi.org/10.1182/blood-2025-4939

Related abstract / conference record:
https://www.sciencedirect.com/science/article/pii/S0006497125076864

https://meetings-api.hematology.org/api/abstract/vmpreview/293068

---

## License
MIT License
