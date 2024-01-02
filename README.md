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

If you intend to annotate variants using the gene annotation databases such as `hs1_draftGene.txt.gz` and `hs1_refGene.txt.gz`, please download `${Database_name}.fa.gz` file as well.
There are index file(`.txt.idx`) for filter-based databases, such as allele frequency(`hs1_ALL.sites.2023_12.txt`) and dbSNP(`hs1_dbsnp156.txt`).  It is not a mandatory file, but it would be helpful to reduce computing time during variant annotation.

### 2. Make your data compatible with annovar

You should make your file compatible with ANNOVAR before annotating with this database. Ensure that your VCF file is properly formatted and contains information about variants such as chromosome, position, reference allele, alternate allele, and additional annotations you want to include in your custom database. Use the `convert2annovar.pl` script to convert your VCF file to ANNOVAR input format:

```bash
perl convert2annovar.pl -format vcf4 ${prefix}.vcf > ${prefix}.avinput
```
Adjust the parameters based on your specific requirements. If you want to check the detailed command line, please visit the [ANNOVAR website](https://annovar.openbioinformatics.org/en/latest/).

You can also download the example file(`example.chr22.inp`) from here. This file has been converted from VCF to Annovar-compatible format and contains only the data from chromosome 22. If you choose to start with this example file, you can skip this step.

### 3. Annotate the Variants
Annotate your variants using ANNOVAR with the downloaded CHM13 T2T AnnoVar Database. Here's an example command:

```bash
annovarDB="/data/usr/user1/annovar/hs1" # The folder where include hs1/ folder
build="hs1"
outPrefix="OUT" # the prefix you want. The ouput name would be ${OUT}.hs1_multianno.txt

table_annovar.pl \
--thread 10 \ 
example.chr22.inp \ # Input file from step 2
$annovarDB/filterDB \ # annovar database direcoty
-buildver $build \ # hs1 (database prefix)
-out ${outPrefix} \ # output prefix (example.chr22.out for the example output)
-remove \
-protocol refGene,curGene,dbsnp156,1000g2023dec_all,1000g2023dec_afr,1000g2023dec_amr,1000g2023dec_eas,1000g2023dec_eur,1000g2023dec_sas,clinvar_20231217,gwas_20231207,nonSyntenic,hg38_issues,feat,cenSat,sraccess,sraccess_hg38,sraccess_hs1Only \
-operation g,g,f,f,f,f,f,f,f,f,r,r,r,r,r,r,r,r \
-arg ',,,,,,,,,,,,,,,,,'
```

Keep in mind that operations such as `g`, `f`, or `r` should be matched with each database. You can find the correct operation for each annotation source on [T2T-CHM13 Databases and operation](https://docs.google.com/spreadsheets/d/1sgjmGLLbXAZpyNiSUbxiEa1hJEVDxuOqL1yAmpDV5BA/edit?usp=sharing)
