## Usage

### 1. Downloading the Database

You can download pre-built databases from [here](https://s3-us-west-2.amazonaws.com/human-pangenomics/index.html?prefix=T2T/CHM13/assemblies/annotation/annovar/), along with references and operation details for each database from the [T2T-CHM13 Databases and operation](https://docs.google.com/spreadsheets/d/1sgjmGLLbXAZpyNiSUbxiEa1hJEVDxuOqL1yAmpDV5BA/edit?usp=sharing)

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

### 2. Make your data compatible with annovar

You should make your file compatible with ANNOVAR before annotating with this database. Ensure that your VCF file is properly formatted and contains information about variants such as chromosome, position, reference allele, alternate allele, and additional annotations you want to include in your custom database. Use the `convert2annovar.pl` script to convert your VCF file to ANNOVAR input format:

```bash
perl convert2annovar.pl -format vcf4 ${prefix}.vcf > ${prefix}.avinput
```
Adjust the parameters based on your specific requirements. If you want to check the detailed command line, please visit the [ANNOVAR website](https://annovar.openbioinformatics.org/en/latest/).

### 3. Annotate the Variants
Annotate your variants using ANNOVAR with the downloaded CHM13 T2T AnnoVar Database. Here's an example command:

```bash
annovarDB="/data/usr/user1/annovar/hs1" # The folder where include hs1/ folder
build="hs1"
outPrefix="OUT" # the prefix you want. The ouput name would be ${OUT}.hs1_multianno.txt

table_annovar.pl ${prefix}.avinput $annovarDB/$build \
-buildver $build \
-out ${outPrefix} \
-remove \
-protocol draftGene,mappable.in.chm13,dbSNPv155,chm13v2-unique_to_hg38,chm13v2.0_GRCh38issues_lifted.20230315,1000g_ALL.2023,1000g_AFR.2023,1000g_AMR.2023,1000g_EAS.2023,1000g_EUR.2023,1000g_SAS.2023 \
-operation g,r,f,r,r,f,f,f,f,f,f \
-arg ',,,,,,,,,,'
```

Keep in mind that operations such as `g`, `f`, or `r` should be matched with each database. You can find the correct operation for each annotation source on [T2T-CHM13 Databases and operation](https://docs.google.com/spreadsheets/d/1sgjmGLLbXAZpyNiSUbxiEa1hJEVDxuOqL1yAmpDV5BA/edit?usp=sharing)
