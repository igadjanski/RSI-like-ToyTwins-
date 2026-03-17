# Radiosensitivity (RSI like) pipeline
To compute a within sample rank based RSI like score for all TCGA GBM and METABRIC TNBC samples, then map it to a normalized sensitivity S and LQ model parameters α,β.
	Start from gene expression matrices (genes × samples, log2 scale) for TCGA GBM and METABRIC TNBC.
	Subset to the 10 canonical RSI genes: AR, JUN, STAT1, PRKCB, RELA, ABL1, SUMO1, PAK2, HDAC1, IRF1.
	For each sample, rank these genes by expression (1 = lowest, 10 = highest).
	Define RSI_like as the mean rank across the available RSI genes (toy implementation; can be replaced by published RSI coefficients later).
	Normalize RSI_like within each cohort:
  RSI_norm=(RSI_like-min⁡(RSI_like))/(max⁡(RSI_like)-min⁡(RSI_like))
  Define radiosensitivity S=1-RSI_norm.
	Map S to LQ parameters using a linear rule α=α_min+(α_max-α_min)⋅S,β=0.03
  with α_min=0.15 Gy-1, α_max=0.45 Gy-1.
  
This procedure is applied identically to all cohorts (TCGA GBM, METABRIC TNBC, and later 2D/3D datasets) to keep analyses consistent with TumorTwin toy experiments


