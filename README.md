# The ANNOVAR databases for CHM13.v2.0 reference! 

<span style="font-size: 100px;"> 😊 Welcome!</span> 😊 <br />

This repository is about how to generate the ANNOVAR database💻 for hs1 (CHM13v2.0)🧬 and how to use this database. Please feel free to leave questions and problems while using this database in the Issues menu.

<details>
<summary>The details how to generate this ANNOVAR database</summary>  
<br />
The original files were listed below with the names of ANNOVAR databases, and the formats were transformed to match those of the ANNOVAR databases.<br />
If the original files are based on GRCh38 or another reference other than CHM13v2.0, the files will need to be liftovered to CHM13 using crossmap. The chain file can be downloaded from the [CHM13 GitHub page](https://s3-us-west-2.amazonaws.com/human-pangenomics/T2T/CHM13/assemblies/chain/v1_nflo/grch38-chm13v2.chain)<br />

## \[ Genome-based DB \]  
`hs1_refGene.txt`: [ANNOVAR homepage](http://www.openbioinformatics.org/annovar/download/hs1_refGene.txt.gz)<br />
`hs1_curGene.txt`: [CHM13 github](https://s3-us-west-2.amazonaws.com/human-pangenomics/T2T/CHM13/assemblies/annotation/chm13v2.0_RefSeq_Liftoff_v5.1.gff3.gz) - This contains curated annotations of the ampliconic genes on the Y chromosome, correcting annotation errors in GENCODEv35 CAT/Liftoff and RefSeqv110 annotation.<br />
* If the original file was formatted in GFF, I transformed it to GTF and then used [gtfToGenePred](https://bioconda.github.io/recipes/ucsc-gtftogenepred/README.html) to convert it into GenePred format.<br />
* The gene annotation databases in ANNOVAR website used to come with ${prefix}Mrna.fa. This files were generated using [`retrieve_seq_from_fasta.pl`](https://github.com/ronammar/Awesomeomics/raw/master/data/annovar_annotations/annovar/retrieve_seq_from_fasta.pl) script.<br />
  ```
  retrieve_seq_from_fasta.pl --format refGene --seqfile chm13v2.0.fa hs1_refGene.txt --out hs1_refGeneMrna.fa
  ```

* format(hs1_curGene.txt): <br />
  ```
     1  XR_002958507.2  chr1    -       6046    13941   13941   13941   4       6046,12077,13444,13679, 6420,12982,13579,13941, 0       LOC124900618    none    none    -1,-1,-1,>
     2  XR_007068557.1_1        chr1    +       15079   21429   21429   21429   2       15079,20565,    15564,21429,    0       LOC124905335_1  none    none    -1,-1,
     3  XM_047436352.1  chr1    -       20528   37628   20949   37628   5       20528,28446,34957,36085,37442,  21087,28626,35059,37081,37628,  0       LOC112268260    incmpl  i>
     4  NR_125957.1     chr1    -       52978   54612   54612   54612   3       52978,53559,54521,      53422,53826,54612,      0       LOC101928626    none    none    -1,-1,-1,
     5  NM_001005221.2  chr1    -       111939  112877  111939  112877  1       111939, 112877, 0       OR4F29  incmpl  incmpl  0,
     6  XR_001743907.1_1        chr1    -       115045  117120  117120  117120  2       115045,116798,  115300,117120,  0       LOC107986552_1  none    none    -1,-1,
  ```

## \[ Filter-based DB \]  
`hs1_dbsnp156.txt`: [NCBI DBsnp ftp server](https://ftp.ncbi.nih.gov/snp/latest_release/VCF/GCF_000001405.40.gz)<br />
`hs1_gwas_20231207.txt`: [GWAS Catalog](https://www.ebi.ac.uk/gwas/docs/file-downloads) v1.0-associations_e110_r2023-12-07<br />
`hs1_clinvar_20231217.txt`: [CHM13 github](https://s3-us-west-2.amazonaws.com/human-pangenomics/T2T/CHM13/assemblies/annotation/liftover/chm13v2.0_ClinVar20220313.vcf.gz)<br />
`hs1_${population}.sites.2023_12.txt`: [CHM13 github](https://s3-us-west-2.amazonaws.com/human-pangenomics/index.html?prefix=T2T/CHM13/assemblies/variants/1000_Genomes_Project/chm13v2.0/)<br /> - 1KGP allele frequency recalled on T2T-CHM13v2.0. Now available for all chromosomes, for the entire 3,202 samples or the unrelated 2504 samples. (popultation : ALL, AFR, AMR, EAS, EUR, and SAS)

* format(hs1_ALL.sites.2023_12.txt) :<br />
  ```
  chr1    131     A       C       0.00278552
  chr1    131     A       T       0.00278552
  chr1    878     A       AACCCTAACCCTCACCCTCACCCTCACCCTCACCCTCACCCTCACCCTC       0.00019976
  chr1    884     AACCCTCACCCTCACCCTCACCCTCACCCTCACCCTCACCCTCACCCTCACCCTCACCCTCACCCTCACCCTCACCCTCACCCTCACCCTCACCCTCACCCTCACCCTCACCCTCACCCTCACCCTC A       0.00020136
  ```
  
## \[ Region-based DB \]   
`hs1_cenSat.txt`: [CHM13 github](https://s3-us-west-2.amazonaws.com/human-pangenomics/T2T/CHM13/assemblies/annotation/chm13v2.0_censat_v2.1.bed) - A more comprehensive centromere/satellite repeat annotation.<br />
`hs1_nonSyntenic.txt`: [CHM13 github](https://s3-us-west-2.amazonaws.com/human-pangenomics/T2T/CHM13/assemblies/chain/v1_nflo/chm13v2-unique_to_hg38.bed) - Regions non-syntenic (unique) compared to GRCh38.<br />
`hs1_hg38_issues.txt`: (CHM13v1 publication)[https://s3-us-west-2.amazonaws.com/human-pangenomics/index.html?prefix=T2T/CHM13/publications/Nurk_2021/fig1/]<br />
`hs1_sraccess.txt`: [CHM13 github](https://s3-us-west-2.amazonaws.com/human-pangenomics/T2T/CHM13/assemblies/annotation/accessibility/combined_mask.bed.gz) - short read accessible regions on CHM13 <br />
`hs1_sraccess_hg38.txt`: [CHM13 amazon download server](https://s3-us-west-2.amazonaws.com/human-pangenomics/index.html?prefix=T2T/CHM13/assemblies/annotation/accessibility/) short read accessible regions on GRCh38 reference then, liftovered to CHM13 <br />
`hs1_sraccess_hs1Only.txt`: short read accessible regions only in CHM13, not in GRCh38 <br />

* format(hs1_cenSat.txt) :
  ```
  1       chr1    116796047       121405145       ct_1_1(p_arm)   100     .       116796047       121405145       224,224,224
  1       chr1    121405145       121406286       censat_1_1(rnd-6_family-4384)   100     .       121405145       121406286       0,204,204
  1       chr1    121406286       121619169       ct_1_2  100     .       121406286       121619169       224,224,224
  1       chr1    121619169       121625213       hor_1_1(S3C1H2-A,B,C)   100     .       121619169       121625213       255,146,0
  1       chr1    121625213       121667941       hor_1_2(S3C1H2-A,B)     100     .       121625213       121667941       255,146,0
  1       chr1    121667941       121788213       hor_1_3(S3C1H2-B)       100     .       121667941       121788213       255,146,0
  1       chr1    121788213       121790362       ct_1_3  100     .       121788213       121790362       224,224,224
  ```


</details>


## Usage

### 1. Downloading the Database

You can download pre-built databases and an example file from [here](https://s3-us-west-2.amazonaws.com/human-pangenomics/index.html?prefix=T2T/CHM13/assemblies/annotation/annovar/), along with original resources we used for generating those databases and operation details for each database from the [T2T-CHM13 Databases and operation](https://docs.google.com/spreadsheets/d/1sgjmGLLbXAZpyNiSUbxiEa1hJEVDxuOqL1yAmpDV5BA/edit?usp=sharing)

The directory structure should be like this:
```bash
- hs1
  - hs1_${Database_name_1}.txt
  - hs1_${Database_name_2}.txt
  - hs1_${Database_name_3}.txt
  ...
```

After downloading the databases, you should unzip each database into a .txt file.
```bash
bgzip -d filename.txt.gz
```

If you intend to annotate variants using the gene annotation databases such as `hs1_curGene.txt.gz` and `hs1_refGene.txt.gz`, please download `${Database_name}Mrna.fa.gz` file as well.

There are index file(`.txt.idx`) for filter-based databases, such as allele frequency(`hs1_ALL.sites.2023_12.txt`) and dbSNP(`hs1_snp156.txt`).  It is not a mandatory file, but it would be helpful to reduce computing time during variant annotation.

### 2. Make your data compatible with annovar

You should make your file compatible with ANNOVAR before annotating with this database. Use the `convert2annovar.pl` script to convert your VCF file to ANNOVAR input format:

```bash
perl convert2annovar.pl -format vcf4 ${prefix}.vcf > ${prefix}.avinput
```
Adjust the parameters based on your specific requirements. If you want to check the detailed command line, please visit the [ANNOVAR website](https://annovar.openbioinformatics.org/en/latest/).

You can also download the example file(`example.chr22.inp`) from [here](https://s3-us-west-2.amazonaws.com/human-pangenomics/index.html?prefix=T2T/CHM13/assemblies/annotation/annovar/). This file has been converted from VCF to Annovar-compatible format and contains only the data from chromosome 22. If you choose to start with this example file, you can skip this step.

### 3. Annotate the Variants
Annotate your variants using ANNOVAR with the downloaded CHM13 T2T AnnoVar Database. Here's an example command:

```bash
annovarDB="/data/usr/user1/annovar/hs1" # The folder where include hs1/ folder
build="hs1"
outPrefix="OUT" # the prefix you want. The ouput name would be ${OUT}.hs1_multianno.txt

table_annovar.pl \
--thread 10 \ 
example.chr22.inp \ # Input file from step 2
$annovarDB/hs1 \ # annovar database direcoty
-buildver $build \ # hs1 (database prefix)
-out ${outPrefix} \ # output prefix (example.chr22.out for the example output)
-remove \
-protocol refGene,curGene,dbsnp156,1000g2023dec_all,1000g2023dec_afr,1000g2023dec_amr,1000g2023dec_eas,1000g2023dec_eur,1000g2023dec_sas,clinvar_20231217,gwas_20231207,nonSyntenic,hg38_issues,feat,cenSat,sraccess,sraccess_hg38,sraccess_hs1Only \
-operation g,g,f,f,f,f,f,f,f,f,r,r,r,r,r,r,r,r \
-arg ',,,,,,,,,,,,,,,,,'
```

Keep in mind that operations such as `g`, `f`, or `r` should be matched with each database. You can find the correct operation for each annotation source on [T2T-CHM13 Databases and operation](https://docs.google.com/spreadsheets/d/1sgjmGLLbXAZpyNiSUbxiEa1hJEVDxuOqL1yAmpDV5BA/edit?usp=sharing)
