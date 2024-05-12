# scrap-pangolin
**Introduction**


This is a rerun of the data from the paper "Genomic analyses reveal poaching hotspots and illegal trade in pangolins from Africa to Asia." The specific pangolin from which the data comes from the White-bellied pangolin also known as the Tree pangolin, is the most widespread species of pangolin in the African continent and consequently is the most widely illegally traded. 
Being a vcf file and from the methods it has been quality checked but I was not completely a 100% sure that the SNPs and Indels were filtered for.


bcftools was used to change the provided vcf file into the required gziped file and tabix was used to index the file to create a tbi file. The results are as seen below and again they were not included in the repository because they were too big and even though these files were placed into the .gitignore, it interfered with the pushing up of the files and commits into the repository. This was part of the reason why pangolin_project is being redone as scrap_pangolin, the other part being my inexperience in solving multiple divergent branches of the pangolin_project. 

![data snap](https://github.com/leezhimeimaria/scrap-pangolin/assets/157052567/c82bdc42-53b2-48a0-8b00-5ab347ffd0d3)

This is why I modified the Snakefile workflow from class to rerun the data through the filter to check if this was indeed the case since 1 of my goals have been to filter data that they have provided. 
The files that I have for this are listed under the results directory under the rerun_snps_and_indels_merge. I want unable to push the files up into this git hub repository because the files were so big, however, down below is the tree of my results after this step is rerunned. 

![results image](https://github.com/leezhimeimaria/scrap-pangolin/assets/157052567/56fbfeb3-1a2d-49f6-8336-b1c3d6fcfd72)


A similar usage of bcftools also took place in my second part I tried to run a PCA through the convertion of the vcf file into a bcf file. 







Part of the goal was to observe a change in the 

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


