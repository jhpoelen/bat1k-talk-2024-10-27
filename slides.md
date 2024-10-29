---
author:
  - Jorrit Poelen (UC Santa Barbara, Ronin Institute, GloBI)
title: "Mobilizing Bat1K"
subtitle: "through versioned, machine readable and automatically generated data publications."
date: 2024-10-27
aspectratio: 169
---

## Guiding Questions

### How to keep track of Bat1k data corpus?

### How to cite specific versions of the Bat1k data corpora?

### How to share specific versions of the Bat1k data corpora?

## Reuse, reuse, reuse.

 * Darwin Core Archive -> GBIF, GloBI 
 * Taxonomic Alignement Tools ^[https://github.com/globalbioticinteractions/nomer] -> align with specific versions MDD, NCBI Taxonomy
 * Signed Data Citations ^[Elliott M.J., Poelen, J.H. & Fortes, J.A.B. (2023) Signing data citations enables data verification and citation persistence. *Sci Data*. https://doi.org/10.1038/s41597-023-02230-y [hash://sha256/f849c870565f608899f183ca261365dce9c9f1c5441b1c779e0db49df9c2a19d](https://linker.bio/hash://sha256/f849c870565f608899f183ca261365dce9c9f1c5441b1c779e0db49df9c2a19d)]


## At NASBR 2024 

Jorrit -> Ariadna -> Sonja -> Meike -> Bat1k data 

## Google Sheet

![Best103assembly_metadata_phase1_v1.2 accessed at https://docs.google.com/spreadsheets/d/1kDVtj_D71oGMz8vH_sLA4AMp8AxmMA7YWqBowOI2PFM/edit?gid=0#gid=0 on 2024-10-27.](./img/google-sheets.png){height=75%}

## Google Sheet -> Versioned, Machine Readable Data Package

```
preston track\
 --message "BatLit genome index"\
https://docs.google.com/spreadsheets/d/1kDVtj_D71oGMz8vH_sLA4AMp8AxmMA7YWqBowOI2PFM/edit?gid=0#gid=0\
 | sha256sum
```

![signature of data1k data package: hash://sha256/710cccc378e6d41e7d2e214bcaf08af76886d9df6e389dc0177c1460fb5c3999](img/qrcode.png){height=75%}
]


## Deriving bat1k.tsv 

```
preston cat\
 hash://sha256/710cccc378e6d41e7d2e214bcaf08af76886d9df6e389dc0177c1460fb5c3999\
 | grep hasVersion\
 | grep tsv\
 | preston cat\
 | tail -n+2\
 | tee bat1k.tsv
```

  


## Taxonomic Alignement through Nomer - Find (mis-)Alignments

Using Nomer ^[Poelen, J. H. (ed . ) . (2024). Nomer Corpus of Taxonomic Resources hash://sha256/b60c0d25a16ae77b24305782017b1a270b79b5d1746f832650f2027ba536e276 hash://md5/17f1363a277ee0e4ecaf1b91c665e47e (0.27) [Data set]. Zenodo. https://doi.org/10.5281/zenodo.12695629]

```
cat bat1k.tsv\
 | nomer append\
 --properties <(echo 'nomer.schema.input=[{"column":0,"type":"externalId"},{"column": 1,"type":"name"}]') mdd\
 | grep -v HAS_ACCEPTED_NAME\
 | cut -f2\
 | tail -n+2
```

```
Lasiurus ega
Hipposideros swinhoii  
```

## Next Steps

 * Versioned Bat1K -> DwC-A - Add meta.xml and eml.xml to describe schema according to Darwin Core Archive to enable:
   * Indexing by GBIF as bat occurrences through vouchered specimen/genome
   * Indexing by GloBI as bat<>human interactions evidenced by vouchered specimen/genomes to enable automated data reviews ^[Geiselman, Cullen K. & Sarah Younger. 2020. Bat Eco-Interactions Database. www.batbase.org https://github.com/globalbioticinteractions/batbase/archive/9c65cfeee1a054f9db8cd8bf6892017fd1b3c840.zip 2024-10-25T22:39:59.352Z 6755e9ff065849a8a7472858e98b62458fab93e4c20006f823e844a3ee77f5f2 see also https://depot.globalbioticinteractions.org/reviews/globalbioticinteractions/batbase/]

## Take Aways

 * track, version and package original data
 * implement automated data review workflow
 * implement automated data product workflow

![Geiselman, Cullen K. & Sarah Younger. 2020. Bat Eco-Interactions Database. www.batbase.org https://github.com/globalbioticinteractions/batbase/archive/9c65cfeee1a054f9db8cd8bf6892017fd1b3c840.zip 2024-10-25T22:39:59.352Z 6755e9ff065849a8a7472858e98b62458fab93e4c20006f823e844a3ee77f5f2 see also https://depot.globalbioticinteractions.org/reviews/globalbioticinteractions/batbase/](img/datareview.png){height=75%}
