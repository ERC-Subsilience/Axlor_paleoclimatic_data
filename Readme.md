# Multi-isotope approaches to Middle Palaeolithic palaeoenvironments - an example from Axlor (Bizkaia, Spain)

This repository contains data, analysis code, and manuscript and supplementary RMarkdown files for:

Pederzani, S., Britton, K., Jones, J., Agudo Pérez, L., Geiling, J. M., Marín-Arroyo, A. B. (2023). Late Pleistocene Neanderthal exploitation of stable, mosaic ecosystems in northern Iberia shown by multi-isotope evidence. Quaternary Research. 

An overview of all files can be found below. Variable names are explained in an additional codebook file (`AXL_codebook.xls`). 

The content of this repository was made possible thanks to funding from the European Research Council (ERC) under the European Union's Horizon 2020 research and innovation programme (grant agreement No. 818299) for the SUBSILIENCE project (https://www.subsilience.eu/).

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

## Prerequisites

In order to be able to run the code, you will need to have an up-to-date version of [R](https://www.r-project.org/) and [RStudio](https://rstudio.com/) or [pandoc](https://pandoc.org/) installed on your computer and a few CRAN packages (see below). 

All code and analyses were run using R version 4.2.0 (R Core Team 2020) on a Windows 10 operating system. 

### Install packages

```
install.packages(c("ggplot2", "dplyr", "tidyr", "cowplot", "captioner", "wesanderson", "knitr", "flextable", "stringr", "officer", "rstatix", "scales", "magick", "patchwork", "ggpubr", "Metrics", "matrixcalc"))
```

The following versions of these packages were used:

matrixcalc_1.0-5  
Metrics_0.1.4     
ggpubr_0.4.0      
patchwork_1.1.1   
magick_2.7.3     
scales_1.2.0      
rstatix_0.7.0     
officer_0.4.2     
stringr_1.4.0     
flextable_0.7.0  
knitr_1.39        
wesanderson_0.3.6   
captioner_2.2.3   
cowplot_1.1.1     
tidyr_1.2.0      
dplyr_1.0.9  
ggplot2_3.3.6  


## Files and code

The repository contains three folder containing relevant files for conducting the Passey et al. (2005) inverse modelling procedure (`run_inverse_model`), for producing palaeotemperature estimates (`reconstruct_temperature`), and for generating the article manuscript and supplementary information and all analyses contained therein (`generate_article`). 

Note that all R scripts and RMarkdown files use relative paths in reference to the location of each file to access data files contained in various repository folders and rely on the folder structure being preserved in the way that it is presented here. To exectute the R scripts, the working directory should be set to the source file location. 

In the following each file and its purpose is described. Please refer to the file `AXL_codebook.xls` for an explanation of the variable names used in the data files. 

### Inverse modelling

`run_inverse_model.r`

 - R script to execute the inverse modelling procedure. Please refer to the original publications by Passey et al. (2005) and Fraser et al. (2021) for detailed explanations of model equations and parameters. Input parameters need to be changed as needed and the script is run with adjusted parameters once for each specimen of interest. The parameters that were used in this study for each specimen are documented in the model report files contained in `run_inverse_model/output`. 

`make_model_report.Rmd` 

- RMarkdown template called by `run_inverse_model.R`
to print model report html files

#### run_inverse_model/input

`*Tooth Name*_inverse_model_input.csv`

- csv files containing sequential d18O data for each analysed tooth, as well as predicted d18Ophos trials from our prediction simulations (see main manuscript methods section for details). These files are structured to serve as the stable isotope input data for `run_inverse_model.r`. 

#### run_inverse_model/functions

`Emeas.R`

- R script containing the `Emeasfun` function called by the `run_inverse_model.r` script. This is equivalent to the Emeas portion of the codes provided by Passey et al. (2005)

`mSolv1.R`

- R script containing the `PasseyInverse` function called by the `run_inverse_model.r` script. This is equivalent to the mSolv portion of the codes provided by Passey et al. (2005) and has been adapted from the R translation of the the original Passey Matlab codes that has been published by Fraser et al. (2021). The model portions of this code are identical to those provided by Fraser, but have been updated with increased commenting and changed slightly so they can be called by an external script and output can be evaluated in a more automated way. 


#### run_inverse_model/output

`AXL_inverse_model_output_all_plot.png`

- Plot of the inverse model outcome of all specimens analysed

`AXL_inverse_model_out_all.csv`

- output of inverse model for all teeth aggregated into a single output file

`AXL_inverse_model_output_extrema.csv`

- summer peak and winter trough values extracted from the inverse model outcomes for all analysed teeth

`*Tooth Name*_inverse_model_output.csv`

- inverse model outcome files for all specimens. These files are generated by `run_inverse_model.r`

`*Tooth Name*_inverse_model_report.html`

- inverse model report files for all specimens. These files document the input parameters that were used to during the excution of `run_inverse_model.r` for the relevant specimen. These files are automatically generated by `run_inverse_model.r`. 

`AXL66_trials_inverse_model_out_all.csv`

- output of inverse model for all predicted d18Ophos time series trials generated in our prediction simulations. Output from all trials is aggregated into a single output file. 

`AXL66_trials_inverse_model_output_extrema.csv`

- summer peak and winter trough values extracted from the inverse model outcomes for all d18Ophos prediction trials. 


### Palaeotemperature reconstruction

`Axlor_Pryor_T_conversion_Layer_*_MAT.xls`

- Files conducting d18Odw and palaeotemperature estimates for annual means. Files are labelled with the relevant Layer number. Files use the template published in Pryor et al. (2014) with adapted calibration data. Calibration data is included in the file and separately available in `reconstruct_temperature/calibration_data`. 

`Axlor_Pryor_T_conversion_Layer_*_Summer.xls`

- Files conducting d18Odw and palaeotemperature estimates for the warmest month. File uses the template published in Pryor et al. (2014) with adapted calibration data. Calibration data is included in the file and separately available in `reconstruct_temperature/calibration_data`. 

`Axlor_Pryor_T_conversion_Layer_*_Winter.xls`

- Files conducting d18Odw and palaeotemperature estimates for the coldest month. File uses the template published in Pryor et al. (2014) with adapted calibration data. Calibration data is included in the file and separately available in `reconstruct_temperature/calibration_data`. 

#### reconstruct_temperature/calibration_data

`GNIP_coldest_month_calibration_data.csv`

- Winter d18Oprecip and temperature calibration data used for temperature estimations in `Axlor_Pryor_T_conversion_Layer_*_Winter.xls`. 

`GNIP_warmest_month_calibration_data.csv`

- Summer d18Oprecip and temperature calibration data used for temperature estimations in `Axlor_Pryor_T_conversion_Layer_*_Summer.xls`. 

`GNIP_MAT_month_calibration_data.csv`

- Mean annual d18Oprecip and temperature calibration data used for temperature estimations in `Axlor_Pryor_T_conversion_Layer_*_MAT.xls`. 

#### reconstruct_temperature/output

`Axlor_seasonal_T_reconstruction.csv`

- Aggregated outputs of d18Odw and palaeotemperature estimates made in the  `Axlor_Pryor_T_conversion_Layer_*_*.xls` files in `reconstruct_temperature`. 

### Manuscript and SI

#### generate_article/common

`AXL_librarby.bib`

- Bibtex file containing bibliographic information of references cited in the article manuscript and SI. 

`quaternary_research.csl`

- Citation style file used by Rmd files to format citations in the main text and SI correctly. 

`reference.docx`

- style reference file that defines Word formatting styles for the docx output of the main text Rmd file

`reference_SI.docx`

- style reference file that defines Word formatting styles for the docx output of the Supplementary Information Rmd file


#### generate_article/data

`AXL_carb_phos_d18O.csv`

- oxygen isotope data for the carbonate and phosphate moiety of sequential tooth enamel samples. Used for comparing/combining carbonate and phosphate d18O measurements 

`AXL_carbonate_d13C_d18O.csv`

- carbon and oxygen stable isotope data measured from bioapatite carbonates of sequential tooth enamel samples. Includes original measurements in the VPDB scale and conversions to the VSMOW scale 

`AXL_collagen_C_N_S_data.csv`

- all carbon, nitrogen and sulphur stable isotope data measured on collagen samples 

`AXL_collagen_samples.csv`

- overview of sample numbers for collagen d13C, d15N and d34S measurements used in this study, including a breakdown of published and new data points used 

`AXL_combined_phosphate_times_series.csv`

- measured and predicted d18Ophos values and combined d18O time series 

`AXL_d18O_unmodelled_extrema_and_mean_annual.csv`

- tooth enamel phosphate oxygen isotope data for summer peaks, winter troughs, and annual means derived from unmodelled d18Ophos measurement data

`AXL_literature_carb_phos_offsite.csv`

- a collection of published d18O carbonate and phosphate measurement pairs made on modern (non-archaeological) non-human terrestrial macro-mammals

`AXL_stratigraphy_table.csv`

- overview of stratigraphic levels of Axlor Cave with age information

`AXL_tooth_samples.csv`

- list of sample information for all aurochs/bison teeth analysed for d18O

`axl66_all_alt_phos_predictions.csv`

- 10 variations of d18O time series data made from combining d18Ophos measurements with d18Ophos values predicted from d18Ocarb. Different trials represent possible variations within prediction error of d18phos from d18Ocarb


#### generate_article/output

##### markdown_out_documents

`Pederzani_Axlor_Main_Text.docx`

- Main manuscript file generated by the main text RMarkdown file (`Pederzani_Axlor_Main_Text.Rmd`)

`Pederzani_Axlor_SI.docx`

- Supplementary Information file generated by the SI RMarkdown file (`Pederzani_Axlor_SI.Rmd`)

##### markdown_out_figures

`axl66_inverse-1.png` - Figure S4

`axl66_model_eval-1.png` - Figure S5

`carbonates-1.png` - Figure S7

`carb_v_phos-1.png` - Figure 2

`collagen_c_n_s-1.png` - Figure 5

`create_alt_combined_phos-1.png` - Figure S3

`c_v_o-1.png` - Figure S8

`d18Odw_plot-1.png` - Figure S6

`ellipses_cn-1.png` - Figure 6

`ellipses_cs-1.png` - Figure 7

`o_extrema-1.png` - Figure 3

`pred_vs_ms-1.png` - Figure S2

`temperatures-1.png` - Figure 4

#### generate_article/rmarkdown

`Pederzani_Axlor_Main_Text.Rmd`

- RMarkdown file that generates the manuscript main text, including figures and directly referenced analyses

`Pederzani_Axlor_SI.Rmd`

- RMarkdown file that generates the Supplementary Information, including figures and referenced analyses

##### rmd_images_import

`AXL_combined_map.png` - image imported for Figure 1

`OxA_40151_calibrated.png` - image imported for Figure S1
