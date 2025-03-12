# BCH_analysis_pipeline
Preliminary workflow analysis for BCH single nuclei data

File names here are hard coded in, this is just to serve as a temporary reference to what is being run in the pipeline. I will clean this up and make it easier to run in the future.

Workflow 
1. Run starsolo_soupx.R on GeneFull/ or Gene/ directory from STARsolo otuput to remove ambient mRNAs
2. Run through seurat_testing.Rmd with output soupx/ directory from step 1 (standard seurat workflow)
3. Run DoubletFinder on seurat object generated from step 2 to identify and filter doublets
4. Run harmony_testing.R to produce a seurat object with all samples integrated and recluster based on new seurat object


Cellbender as an alternative to SoupX - 

On McCleary - 

conda create -n cellbender python=3.9
conda activate cellbender
pip install --user cellbender

Example cellbender run to remove ambient RNA - 
sbatch --wrap "cellbender remove-background --cuda --input CTRL38/CTRL38-starSolo.out/GeneFull/raw/ --output CTRL38/test.h5" --mem 32G -t 2:00:00 --gpus 1 --partition gpu

To load the cellbender .h5 files into Seurat - 
install.packages("scCustomize")
library(scCustomize)
