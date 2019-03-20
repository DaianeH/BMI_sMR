# BMI_sMR
sMR analysis on BMI variants

### DATA
eQTL identified by Dobin et al (2018) (Landscape of Conditional eQTL in Dorsolateral Prefrontal Cortex and Co-localization with Schizophrenia GWAS): post-mortem human brain samples (n = 467) reported by the CommonMind Consortium (CMC)
The CommonMind Consortium sequenced RNA from dorsolateral prefrontal cortex of schizophrenia cases (N = 258) and control subjects (N = 279)

Lude Franke: Unraveling the polygenic architecture of complex traits using blood eQTL meta analysis
eQTSs identify key driver genes for polygenic traits: To ascertain the coordinated effects of trait-associated variants on gene expression, we used available GWAS summary statistics to calculate PGSs for 1,263 traits in 28,158 samples. We reasoned that when a gene shows expression levels that significantly correlate with the PGS for a specific trait (an expression quantitative trait score; eQTS), the downstream trans-eQTL effects of the individual risk variants converge on that gene,and hence, that the gene may be a driver of the disease. Our meta-analysis identified 18,210 eQTS effects (FDR < 0.05), representing 689 unique traits (54%) and 2,568 unique genes (13%; Supplementary Table 15, Figure 1A). Only thing found here related to BMI: The downregulated NRG1 (neuregulin 1; strongest eQTS P=4.5×10-7), encodes a well-established growth factor involved in neuronal development and has been
associated to synaptic plasticity57. NRG1 was also positively associated with the PGS for monocyte
levels20 (strongest eQTS P=1.5×10-7), several LDL cholesterol traits (e.g. medium LDL particles44;
strongest eQTS P=6.2×10-8), coronary artery disease33 (strongest eQTS P=1.5×10-6) and body
mass index in females58 (strongest eQTS P=9.2×10-12)".




-- test for pleiotropic association between the expression level of a gene and a complex trait of interest using summary-level data from GWAS and expression quantitative trait loci (eQTL) studies
-- analysis to test if the effect size of a SNP on the phenotype is mediated by gene expression. This tool can therefore be used to prioritize genes underlying GWAS hits for follow-up functional studies.


===== RUNNING SMR ======

smr --bfile mydata --gwas-summary mygwas.ma --beqtl-summary myeqtl --out mysmr --thread-num 10

smr --bfile /sc/orga/projects/loosr01a/Arden/UKBB/UKBBRef --gwas-summary SNP_gwas_mc_merge_nogc.tbl.uniq --beqtl-summary EQTL_FILE --out 





ssh hemerd01@minerva.hpc.mssm.edu
ssh loosr01-1
cd /sc/orga/loosr01a/daiane/projects/smr/


### RUN 1
## GWAS Locke et al, eQTL blood westra
./smr_Linux --bfile /sc/orga/projects/loosr01a/Arden/UKBB/UKBBRef --gwas-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/gwas/All_ancestries_SNP_gwas_mc_merge_nogc.tbl.uniq --beqtl-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/eqtl/westra_eqtl_hg19 --out /sc/orga/projects/loosr01a/daiane/projects/smr/output/locke_westra  --thread-num 10 


### RUN 2
## GWAS Locke et al on UKB, eQTL blood westra
./smr_Linux --bfile /sc/orga/projects/loosr01a/Arden/UKBB/UKBBRef --gwas-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/gwas/Meta-analysis_Locke_et_al+UKBiobank_2018_UPDATED_smr.txt --beqtl-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/eqtl/westra_eqtl_hg19 --out /sc/orga/projects/loosr01a/daiane/projects/smr/output/locke_ukb_westra  --thread-num 10 

### RUN 3
## GWAS Locke et al on UKB, eQTL brain eMeta
./smr_Linux --bfile /sc/orga/projects/loosr01a/Arden/UKBB/UKBBRef --gwas-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/gwas/Meta-analysis_Locke_et_al+UKBiobank_2018_UPDATED_smr.txt --beqtl-summary /hpc/users/hemerd01/daiane/projects/smr/data/eqtl/Brain-eMeta/Brain-eMeta --out /sc/orga/projects/loosr01a/daiane/projects/smr/output/locke_ukb_brainemeta  --thread-num 10 

### RUN 4
## GWAS Locke et al on Gtex 7, replicating Yengo et al. 2018
while read tissue ; do ./smr_Linux --bfile /sc/orga/projects/loosr01a/Arden/UKBB/UKBBRef --gwas-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/gwas/Meta-analysis_Locke_et_al+UKBiobank_2018_UPDATED_smr.txt --beqtl-summary /hpc/users/hemerd01/daiane/projects/smr/data/eqtl/GTEx_V7_cis_eqtl_summary_lite/$tissue --out /sc/orga/projects/loosr01a/daiane/projects/smr/output/locke_ukb_$tissue  --thread-num 10 ; done < /sc/orga/projects/loosr01a/daiane/projects/smr/data/eqtl/GTEx_V7_cis_eqtl_summary_lite/listTissues.txt

### RUN 5
## GWAS Locke et al on UKB, eQTLgen
File with significant (FDR<0.05) cis-eQTL results: cis-eQTL_significant_20181017.txt.gz
https://molgenis26.gcc.rug.nl/downloads/eqtlgen/cis-eqtl/README_cis
These files contain all cis-eQTL results from eQTLGen, accompanying the article.
19,960 genes that showed expression in blood were tested.
Every SNP-gene combination with a distance <1Mb from the center of the gene and  tested in at least 2 cohorts was included.
Associations where SNP/proxy positioned in Illumina probe were not removed from combined analysis.
./smr_Linux --bfile /sc/orga/projects/loosr01a/Arden/UKBB/UKBBRef --gwas-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/gwas/Meta-analysis_Locke_et_al+UKBiobank_2018_UPDATED_smr.txt --beqtl-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/eqtl/cis-eQTLsFDR0.05-ProbeLevel.txt_besd --out /sc/orga/projects/loosr01a/daiane/projects/smr/output/locke_ukb_eqtlgen  --thread-num 10 

### RUN 6
## GWAS Locke UKB signifiacant from run on eQTLgen, on CAGE
./smr_Linux --bfile /sc/orga/projects/loosr01a/Arden/UKBB/UKBBRef --gwas-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/gwas/Meta-analysis_Locke_et_al+UKBiobank_2018_UPDATED_smr.txt --beqtl-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/eqtl/cage_eqtl_data_lite_hg19/CAGE.sparse.lite --extract-snp /sc/orga/projects/loosr01a/daiane/projects/smr/output/lockeUKB_eqtlgen_sigSNPs.list --out /sc/orga/projects/loosr01a/daiane/projects/smr/output/locke_ukb_CAGE_rep --thread-num 10

smr --bfile mydata --gwas-summary mygwas.ma --beqtl-summary myeqtl --extract-snp mysnp.list --extract-probe myprobe.list --out mysmr 


### RUN 7
## GWAS Locke UKB signifiacant from run on CAGE, on eQTLgen
./smr_Linux --bfile /sc/orga/projects/loosr01a/Arden/UKBB/UKBBRef --gwas-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/gwas/Meta-analysis_Locke_et_al+UKBiobank_2018_UPDATED_smr.txt --beqtl-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/eqtl/cis-eQTLsFDR0.05-ProbeLevel.txt_besd --extract-snp /sc/orga/projects/loosr01a/daiane/projects/smr/output/cage_sigsnps_list.txt --out /sc/orga/projects/loosr01a/daiane/projects/smr/output/locke_ukb_eQTLgen_rep --thread-num 10


### RUN 8
## GWAS Locke UKB on CAGE complete (not the lite version)
./smr_Linux --bfile /sc/orga/projects/loosr01a/Arden/UKBB/UKBBRef --gwas-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/gwas/Meta-analysis_Locke_et_al+UKBiobank_2018_UPDATED_smr.txt --beqtl-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/eqtl/cage_eqtl_data/CAGE.sparse --out /sc/orga/projects/loosr01a/daiane/projects/smr/output/locke_ukb_CAGE_complete --thread-num 10


### RUN 9
## GWAS Locke UKB on Gtex brain only
./smr_Linux --bfile /sc/orga/projects/loosr01a/Arden/UKBB/UKBBRef --gwas-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/gwas/Meta-analysis_Locke_et_al+UKBiobank_2018_UPDATED_smr.txt --beqtl-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/eqtl/GTEx-brain/GTEx-brain_std --out /sc/orga/projects/loosr01a/daiane/projects/smr/output/locke_ukb_Gt --thread-num 10

### RUN 10
## GWAS Locke UKB on CMC only
./smr_Linux --bfile /sc/orga/projects/loosr01a/Arden/UKBB/UKBBRef --gwas-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/gwas/Meta-analysis_Locke_et_al+UKBiobank_2018_UPDATED_smr.txt --beqtl-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/eqtl/CMC_2/CMC_eqtl --out /sc/orga/projects/loosr01a/daiane/projects/smr/output/locke_ukb_CMC --thread-num 10


### RUN 11
## GWAS Locke UKB on Rosmap only
./smr_Linux --bfile /sc/orga/projects/loosr01a/Arden/UKBB/UKBBRef --gwas-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/gwas/Meta-analysis_Locke_et_al+UKBiobank_2018_UPDATED_smr.txt --beqtl-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/eqtl/ROSMAP_2/Rosmap_eQTL_std --out /sc/orga/projects/loosr01a/daiane/projects/smr/output/locke_ukb_ROSMAP --thread-num 10



###### COMPARISON: RUNNING THE SAME ANALYSIS BUT WITH WAIST-HIP RATIO AS GWAS #######
whradjbmi.giant-ukbb.meta-analysis.combined.23May2018.HapMap2_only.txt.gz

awk '{print $3, $4, $5, $6, $7, $8, $9, $10}' Whradjbmi.giant-ukbb.meta-analysis.combined.23May2018.HapMap2_only.txt > Whradjbmi.giant-ukbb.meta-analysis.combined.23May2018.HapMap2_only_smr.txt 

Whradjbmi.giant-ukbb.meta-analysis.combined.23May2018.HapMap2_only_smr.txt

## GWAS WHR, eQTL brain eMeta
./smr_Linux --bfile /sc/orga/projects/loosr01a/Arden/UKBB/UKBBRef --gwas-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/gwas/Whradjbmi.giant-ukbb.meta-analysis.combined.23May2018.HapMap2_only_smr.txt --beqtl-summary /hpc/users/hemerd01/daiane/projects/smr/data/eqtl/Brain-eMeta/Brain-eMeta --out /sc/orga/projects/loosr01a/daiane/projects/smr/output/whr_brainemeta  --thread-num 10 

## GWAS WHR, eQTL eQTLgen
./smr_Linux --bfile /sc/orga/projects/loosr01a/Arden/UKBB/UKBBRef --gwas-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/gwas/Whradjbmi.giant-ukbb.meta-analysis.combined.23May2018.HapMap2_only_smr.txt --beqtl-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/eqtl/cis-eQTLsFDR0.05-ProbeLevel.txt_besd --out /sc/orga/projects/loosr01a/daiane/projects/smr/output/whr_eqtlgen  --thread-num 10 

## GWAS WHR on CMC only
./smr_Linux --bfile /sc/orga/projects/loosr01a/Arden/UKBB/UKBBRef --gwas-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/gwas/Whradjbmi.giant-ukbb.meta-analysis.combined.23May2018.HapMap2_only_smr.txt --beqtl-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/eqtl/CMC_2/CMC_eqtl --out /sc/orga/projects/loosr01a/daiane/projects/smr/output/WHR_CMC --thread-num 10



#### TO RUN
## GWAS WHR on Rosmap only
./smr_Linux --bfile /sc/orga/projects/loosr01a/Arden/UKBB/UKBBRef --gwas-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/gwas/Whradjbmi.giant-ukbb.meta-analysis.combined.23May2018.HapMap2_only_smr.txt  --beqtl-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/eqtl/ROSMAP_2/Rosmap_eQTL_std --out /sc/orga/projects/loosr01a/daiane/projects/smr/output/WHR_ROSMAP --thread-num 10

## GWAS WHR on Gtex brain only
./smr_Linux --bfile /sc/orga/projects/loosr01a/Arden/UKBB/UKBBRef --gwas-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/gwas/Whradjbmi.giant-ukbb.meta-analysis.combined.23May2018.HapMap2_only_smr.txt --beqtl-summary /sc/orga/projects/loosr01a/daiane/projects/smr/data/eqtl/GTEx-brain/GTEx-brain_std --out /sc/orga/projects/loosr01a/daiane/projects/smr/output/WHR_GtexBrain --thread-num 10


#### TO DO

- Check which of the genes are new (Of the 104 highly prioritized genes, 22 are new candidates: that is, there was no GWAS SNP achieving PGWAS < 5 × 10−8 within 0.5 Mb of the probe )

- Compare results of Brain e-Meta and 3 brain cohorts separetely

- Overlap the amount of genes found for BMI x WHR

- Locus plots

- Enrichment in regulatory regions?

- PICS probability / FINEMAP

- Manuscript

- ppt presentation




RESULTS

 There were 14,329 probes in total in the Westra eQTL data. We included only probes with at least one cis-eQTL at PeQTL < 5 × 10−8 and excluded probes in the major histocompatibility complex (MHC) region19 because of the complexity of this region. We retained 5,967 probes for analysis.
 
After data processing, there were 5967 probes left. So the genome-wide significance level for SMR test was Psmr < 8.4 × 10−6 (0.05/5967, Bonferroni Correction).
PHEIDI > 0.05

 For each probe that passed the genome-wide significance threshold for the SMR test, we tested the heterogeneity in the bxy values estimated for multiple SNPs in the cis-eQTL region using the HEIDI method. We detected heterogeneity for 185 of the 289 genes at PHEIDI < 0.05. We used a P-value threshold of 0.05 for the HEIDI test, without correcting for multiple tests, which is conservative for gene discovery because it retains fewer genes than when correcting for multiple testing. For the remaining 104 genes (Supplementary Table 6) that passed the HEIDI test (PHEIDI ≥ 0.05), we could not reject the null hypothesis that there is a single causal variant affecting both gene expression and trait variation. Hence, these 104 genes (tagged by 112 probes) are the most functionally relevant genes underlying the GWAS hits (68 for height, 9 for BMI, 2 for WHRadjBMI, 9 for rheumatoid arthritis and 16 for schizophrenia; Table 1) and could be prioritized in follow-up functional studies. There were three non-annotated genes. Interestingly, of the 101 annotated genes, about two-thirds (62 of 101) were not the nearest annotated gene to the top associated GWAS SNP (Table 1). The SMR analysis (including an SMR test followed by a HEIDI test), which only uses summary data in the public domain, provides a useful tool to prioritize genes at a known trait- or disease-associated locus for functional studies (Fig. 3).


