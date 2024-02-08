# GBM annotation
This is a repository that contains the script and files that help to search for KO, EGGNOG and TigerFAM functional categories which are missing in Humann3 utility_mapping databses against Uniprot database.


For GBM annotation, we need to generate the abundance table of KO, EGGNOG and TigerFAM functional categories, which consist the Gut Brain Moduels according to the [GBM database](https://raeslab.org/software/gbms.html) (version1.0). Therefore we planned to:
1. Annotate samples with Humann3, which generates the profile table of gene families
2. Regroup gene family profile to profile tables of KO, EGGNOG and TigerFAM functional categories with map_ko_uniref90.txt.gz, map_eggnog_uniref90.txt.gz (Humann3 version 3.6) as well as the humann_regroup_table function from Humann3 version 3.6.
3. Map profile tables of KO, EGGNOG and TigerFAM functional categories to GBM profile table with [Omixer-RPM](https://github.com/raeslab/omixer-rpm).


However, we found that there 137 functional categories (KO, EGGNOG and TigerFAM) from the GBM database missing in the map_ko_uniref90.txt.gz, map_eggnog_uniref90.txt.gz (Humann3 version 3.6), which could be due to the version difference of uniprot in GBM databases and Humann3 regroup databses. Thus we wrote serveral jupyter notebooks to query the missing functional categories from Uniprot (release-2023_04) to acquire the gene-failies:functional-category pairs.


The missing 137 functional categories includes:

1. 51 NOG entries: "bactNOG00014","bactNOG00441","bactNOG00852","bactNOG00947","bactNOG01259","bactNOG01662","bactNOG01793","bactNOG01844","bactNOG02159","bactNOG02194","bactNOG02239","bactNOG02592","bactNOG02881","bactNOG02937","bactNOG03269","bactNOG03766","bactNOG04578","bactNOG05056","bactNOG05829","bactNOG06811","bactNOG07153","bactNOG07881","bactNOG08340","bactNOG10247","bactNOG10565","bactNOG12453","bactNOG12836","bactNOG14098","bactNOG15341","bactNOG16627","bactNOG18192","bactNOG18519","bactNOG18630","bactNOG20249","bactNOG24711","bactNOG26316","bactNOG27043","bactNOG28876","bactNOG30464","bactNOG31116","bactNOG36984","bactNOG48307","bactNOG51678","bactNOG62245","bactNOG69335","bactNOG82617","firmNOG00626","firmNOG04290","NOG132553","NOG133663","proNOG30191"
2. 1 KO entry: "K00492"
3. 17 TigerFAM entries: "TIGR00078","TIGR00541","TIGR00550","TIGR00551","TIGR00552","TIGR01034","TIGR01122","TIGR01123","TIGR01269","TIGR01350","TIGR02422","TIGR02423","TIGR02617","TIGR03346","TIGR03811","TIGR03812","TIGR04380"

However after querying, there are still 2 TigerFAM (TIGR01269, TIGR03812) entries could not be found on Uniprot (release-2023_04), they are not included in the downstream analysis. They are the essential components for MGB012, Dopamine synthesis. This means MGB012, Dopamine synthesis would be ignored for the downstream analysis, leaving 55 GBMs left for annotation.


For missing NOG entries, ParseEggNog3.ipynb was used for uniprot querying. See the notebook for details. 
For missing Kegg entries, ParseKegg.ipynb was used for uniprot querying. See the notebook for details. 
For missing TIGRFAM entries, ParseTIGRFAM.ipynb was used for uniprot querying. See the notebook for details.


Eventually, the three query results were concatenated into Pesudo_map_eggnong_ko_tigrfam_uniref90.txt as the mapping file of humann_regroup_table function, which ensuers the completeness of the regrouping.


**Note that the uniprot version used for the paper is release-2023_04, different version may result in different query result.**