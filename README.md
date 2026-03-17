# RSI-like-ToyTwins-
**Background & motivation:** 
- Radiotherapy (RT) outcomes vary widely between patients; 
- Genomic radiosensitivity signatures like RSI (RadioSensitivity Index) can predict response in glioblastoma (GB) and breast cancer (triple negative breast cancer: TNBC) 
- Most radiosensitivity data comes from 2D cell cultures, but 3D spheroids/organoids better recapitulate tumor biology and show different radioresponses
**Gap 1:** No systematic comparison of RSI computed from 2D vs 3D models vs clinical tumor**

- [TumorTwin](https://oncologymodelinggroup.github.io/TumorTwin/) is an open‑source Python framework for building patient‑specific digital twins of solid tumors
- TumorTwin, as described in the [paper](https://arxiv.org/html/2505.00670v1) and GitHub docs, is built around imaging data (MRI) plus treatment history and a reaction–diffusion + LQ radiotherapy model; it does not currently use transcriptomic or other -omics data as inputs or parameters. 
- All model calibration in the example high-grade glioma (HGG) and TNBC cases is done against imaging‑derived tumor cellularity and treatment schedules, with parameters fitted to imaging, not to gene expression.
**Gap 2:**  **TumorTwin does not currently use transcriptomic or any -omics data as inputs/parameters**

**Project aims**: 

1. Build a toy digital twin framework that uses transcriptomic radiosensitivity scores (RSI‑like) to predict radiotherapy response in 3D tumor models, and test whether 3D gene‑expression profiles better recapitulate clinical radiosensitivity than traditional 2D cultures 
2. Link gene expression to TumorTwin parameters:  
- RSI‑like radiosensitivity score provides a principled way to initialize the  parameters TumorTwin can use (i.e. *TumorTwin's reaction–diffusion radiotherapy module uses αRT and βRT in a linear–quadratic survival term to model dose‑dependent cell kill at each fraction) from transcriptomic data (TCGA‑GBM, METABRIC)
- For each tumor (patient or cell‑line), we compute a hub‑gene–based RSI‑like score from baseline expression, normalize it, and map it to αRT and βRT, which are then used by TumorTwin to simulate radiotherapy response within the same framework currently calibrated to imaging and clinical data.

- **Future work** will replace generic αRT and βRT values in TumorTwin with gene‑expression‑derived priors, and test whether integrating RSI‑like radiosensitivity estimates improves the twin’s ability to reproduce observed control rates and progression patterns in GB and TNBC cancer cohorts

**What is RSI?**
RSI is a validated 10‑gene expression signature originallya,b trained to predict SF2 from baseline transcriptomic profiles 
SF2 (surviving fraction at 2 Gy) quantifies intrinsic cellular radioresistance in clonogenic assays
10 signature genes: AR, JUN, STAT1, PKCB, RELA (p65), ABL1, SUMO1, PAK2, HDAC1 and IRF1 
Higher RSI = more radioresistant (higher SF2)
Validated in clinical cohorts: RSI stratifies overall survival in GB and breast cancer patients receiving radiotherapy

RSI-like score pipeline - see docs/

**Done**: For this toy twin, we defined an ‘RSI‑like’ score as the mean expression of 9 canonical RSI hub genes (AR, JUN, STAT1, RELA, ABL1, SUMO1, PAK2, HDAC1, IRF1) per sample, then linearly mapped this score to α and β of the linear–quadratic model. This is an illustrative proxy, not the published 10‑gene rank‑based RSI. 
- signature RSI genes were indexed from the genomics data in the TCGA‑GBM, METABRIC databases

**Data sources:**
Patient level data: 
- TCGA‑GBM at GDC/Linkedomics: https://www.linkedomics.org/data_download/TCGA-GBM/ 
**Note**: TCGA‑GBM gene‑expression data were analyzed without pre‑filtering by recorded radiotherapy status, because the RNA‑seq matrices from Linkedomics aggregate all profiled tumors. However, radiotherapy is part of the standard of care for glioblastoma, and published analyses indicate that the vast majority of TCGA‑GBM patients received external‑beam radiotherapy (typically 60 Gy in 30 fractions) alongside temozolomide. In this poster, we therefore treat the TCGA‑GBM RSIlike distribution as representative of clinically irradiated GBM tumors, while acknowledging that a minority of non‑irradiated cases may be included.”

- METABRIC via cBioPortal: https://www.cbioportal.org/study/summary?id=brca_metabric
**Note:** In contrast to TCGA‑GBM, where radiotherapy is standard but not explicitly filtered, the METABRIC subset used here is strictly limited to triple‑negative breast cancers treated with radiotherapy, providing a more homogeneous clinical RT context.

**2D cell lines vs 3D spheroids/organoids/tumoroids** data: 
From peer-reviewed publications: 
---Lena Neufeld et al. ,Microengineered perfusable 3D-bioprinted glioblastoma model for in vivo mimicry of tumor microenvironment.Sci. Adv.7,eabi9119(2021).DOI:[10.1126/sciadv.abi9119]([https://doi.org/10.1126/sciadv.abi9119] & 
https://www.ncbi.nlm.nih.gov/geo/download/?acc=GSE182371 

in progress...




