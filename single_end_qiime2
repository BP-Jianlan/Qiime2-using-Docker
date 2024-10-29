# Step 1: Import the data
echo "Step 1: Importing data"
# single end
qiime tools import \
  --type 'SampleData[SequencesWithQuality]' \
  --input-path manifest \
  --output-path single-end-demux.qza \
  --input-format SingleEndFastqManifestPhred33V2
  
# Create folder
mkdir Vis_files

# Step 2: Generate vizu
echo "Step 2: Generate visual folder"
qiime demux summarize \
--i-data single-end-demux.qza \
--o-visualization Vis_files/demux.qzv

# Step 3: Qiime data2 QC
echo "Step 3: Qiime data2 QC"
### example: denoise single
qiime dada2 denoise-single \
--i-demultiplexed-seqs single-end-demux.qza \
--p-trim-left 0 \
--p-trunc-len 120 \
--o-representative-sequences rep-seqs.qza \
--o-table table.qza \
--o-denoising-stats denoising-stats.qza

# Step 4: Qiime data2 Summarize
echo "Step 3: Qiime data2 Summarize"
qiime feature-table summarize \
--i-table table.qza \
--o-visualization Vis_files/table.qzv

qiime feature-table tabulate-seqs \
--i-data rep-seqs.qza \
--o-visualization Vis_files/rep-seqs.qzv

qiime metadata tabulate \
--m-input-file denoising-stats.qza \
--o-visualization dada2-stats-sum.qzv

# Step 5: Generate a tree for phylogenetic diversity
qiime phylogeny align-to-tree-mafft-fasttree \
--i-sequences rep-seqs.qza \
--o-alignment aligned-rep-seqs.qza \
--o-masked-alignment masked-aligned-rep-seqs.qza \
--o-tree unrooted-tree.qza \
--o-rooted-tree rooted-tree.qza

# Step 6: Alpha rarefaction
qiime diversity alpha-rarefaction \
--i-table table.qza \
--i-phylogeny rooted-tree.qza \
--p-max-depth 20000 \
--o-visualization alpha-rarefaction.qzv

# Step 7: Alpha and Beta analysis
# Step 8: Plot the results of the Alpha and Beta analysis

# Step 9: Taxonomic analysis
echo "Step 9: Taxonomic Analysis"
qiime feature-classifier classify-sklearn \
--i-classifier /home/jiapengc/DockerQiime2/re-TrainQiime/HOMD_15.23_classifier.qza \
--i-reads rep-seqs.qza \
--p-n-jobs 77 \
--o-classification taxonomy.qza

# Step 10: qza 2 csv
echo "Step 10: qza 2 csv"
mkdir -p results
qiime tools export \
--input-path taxonomy.qza \
--output-path results


