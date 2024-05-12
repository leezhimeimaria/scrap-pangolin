# Running an existing dataset on confiscated pangolins from Africa and Asia for a PCA. 
**Introduction**


This is a rerun of the data from the paper "Genomic analyses reveal poaching hotspots and illegal trade in pangolins from Africa to Asia." The specific pangolin from which the data comes from the White-bellied pangolin also known as the Tree pangolin, is the most widespread species of pangolin in the African continent and consequently is the most widely illegally traded. 
Being a vcf file and from the methods it has been quality checked but I was not completely a 100% sure that the SNPs and Indels were filtered for.


bcftools was used to change the provided vcf file into the required gziped file and tabix was used to index the file to create a tbi file. The results are as seen below and again they were not included in the repository because they were too big and even though these files were placed into the .gitignore, it interfered with the pushing up of the files and commits into the repository. This was part of the reason why pangolin_project is being redone as scrap_pangolin, the other part being my inexperience in solving multiple divergent branches of the pangolin_project. 

![data snap](https://github.com/leezhimeimaria/scrap-pangolin/assets/157052567/c82bdc42-53b2-48a0-8b00-5ab347ffd0d3)

This is why I modified the Snakefile workflow from class to rerun the data through the filter to check if this was indeed the case since 1 of my goals have been to filter data that they have provided. 
The files that I have for this are listed under the results directory under the rerun_snps_and_indels_merge. I want unable to push the files up into this git hub repository because the files were so big, however, down below is the tree of my results after this step is rerunned. 

![results image](https://github.com/leezhimeimaria/scrap-pangolin/assets/157052567/56fbfeb3-1a2d-49f6-8336-b1c3d6fcfd72)

A similar usage of bcftools also took place in my second part I tried to run a PCA through the convertion of the vcf file into a bcf file. A few files had to be created and these files are listed under the directory "pca." The list is as follows: 

![error](https://github.com/leezhimeimaria/scrap-pangolin/assets/157052567/206cdd69-aa78-412a-a9b9-3e5702fb620a)

Only the scaffolds with the highest reads were selected for and this meant that from the dataset provided only HiC_scaffold_1 to 57 was seclect for to create the table below for the running of the PCA workflow. 

```{r}
sg <- read_table(r"(C:\Users\zmmar\Documents\pangolin_scafold.R)", col_names = c("chrom", "stop", "junk")) %>% 
  select(-junk) %>%
  mutate(
    start = 1, 
    angsd_chrom = str_replace_all(chrom, "_", "-"), 
    mh_label = 1:n(), 
    id=sprintf("scaf_group_%03d", 1:n()) 
  ) %>%
    select(id,chrom,start,stop,angsd_chrom,mh_label)

write_tsv(sg, file = r"(C:\Users\zmmar\Documents\pangolin_scaftable.tsv)")
```
The impass after the resolution of the divergent branches and remaking the repository is as shown below

![error screenshot](https://github.com/leezhimeimaria/scrap-pangolin/assets/157052567/c8c460ea-e98e-445e-8d1a-c366b65074b7)


The goal of creating the map below was to observe a correlation with the PCA. As it stands now current the map simply shows where the samples were confiscated and their country origin. The code I have listed below is what I have used to generate the map below. It should be noted because many samples are confiscated from the same location, the number of points do not indicate the number of samples they are. In other words, even though there are many more points of Nigeria, on the map it may not mean that the majority of samples came from Nigeria only that the illegal trade of it is more widespread. 

```{r}
pangolin_data=read.csv(r"(C:\Users\zmmar\Downloads\doi_10_5061_dryad_zkh1893g7__v20231219\PangHKsamples2.csv)")

ggplot(data=pangolin_data, aes(x=LONG,y=LAT))+
  annotation_map_tile(type = "osm", progress = "none")+
  geom_spatial_point(aes(colour=ORIGIN), alpha = 1)+
  labs(y="Latitude",x="Longitude")+
  annotation_north_arrow(location = "bl", which_north = "true", twidth = unit(1,"cm"), style = north_arrow_nautical)+
  theme_bw()
```

![map](https://github.com/leezhimeimaria/scrap-pangolin/assets/157052567/33de761f-55a8-4e28-bef9-3b47efbe0278)


**Reference**

Tinsman, Jen C et al. “Genomic Analyses Reveal Poaching Hotspots and Illegal Trade in Pangolins from Africa to Asia.” Science (American Association for the Advancement of Science) 382.6676 (2023): 1282–1286. Web.


