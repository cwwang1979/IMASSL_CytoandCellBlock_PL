# Interpretable-Multi-stage-Attention-DL-Network-to-Predict-Malignancy-in-Cyto-Smears-and-CB-of-PE
In this study, we proposed a deep learning framework, namely Interpretable Multi-stage Attention deep learning Network (IMAN), to predict pleural effusion status using 194 Cytological smears WSIs and 188 cell blocks WSIs from the Biobank of Tri-Service General Hospital, Taipei (TSGH). 


## Associated Publications
Wang et al. (In submission) Interpretable Multi-stage Attention Network to Predict Cancer Subtype and Molecular Status of Microsatellite Instability, TP53 mutation and Tumor Mutational Burden of Endometrial and Colorectal Cancer

## Cytological Smears Dataset
In this study, we collected 194 cytological smear slides from the Department of Pathology at Tri-Service General Hospital, Taipei, Taiwan and the National Defense Medical Center, Taipei, Taiwan. This cohort covers individuals aged 23 to 109 with 80 male and 114 female patients, respectively. The class distribution is presented  positive for malignancy (n=74); negative for malignancy (n=120)]. 

### Cell Blocks Dataset
Moreover, we also collected 188 cell blocks slides from the Department of Pathology at Tri-Service General Hospital, Taipei, Taiwan and the National Defense Medical Center, Taipei, Taiwan. This cohort covers individuals aged 23 to 109 with 76 male and 112 female patients, respectively. The class distribution is presented  positive for malignancy (n=70); negative for malignancy (n=118)].

## Experiment Setup

#### Requirements
- Ubuntu 18.04
- RAM >= 64 GB
- GPU Memory >= 12 GB
- GPU driver version >= 525.125.06
- CUDA version >= 12.0

Import the IMAN virtual environment in conda
```
conda env create --file=iman.yaml
```
then enter the environment:
```
conda activate iman
```

#### Download
The source code file, configuration file, and models (./IMAN/run/.../checkpoint.pth) can be downloaded from the [zip](https://drive.google.com/file/d/1C_SDPP1oDaiAmmzJsJ30eYIOPt7vmcMe/view?usp=drive_link) file. (For reviewers, the password of the zip file is provided in the "Code Availability" section of the associated manuscript.)

## Steps

#### 1. Bag-wise foreground extraction

Place the Whole slide images in ./WSI/TCGA
```
./WSI/TCGA/
├── slide_1.svs
├── slide_2.svs
│        ⋮
└── slide_n.svs
  
```

Execute the extraction code in a terminal as follows:
```
cd pre
python run_preprocess.py
```

The foreground bag files are saved in desired directory as arranged as follows.
```
./csv/Target_csv_Folder/
├── slide_1.csv
├── slide_2.csv
│        ⋮
└── slide_n.csv
  
```
Ensure the csv files contain the following example structure:

| bag_id | x | y |
|--|--|--|
| 6 | 12288 |0 |
| 30 |61440 |0 |
|....|...|
| 2385 |51200 |81920 |
  
#### 2. Divide training, validation and testing set

The format of the label file can refer to `IMAN/csv/label_example/sheet/train.csv` and `IMAN/csv/label_example/sheet/test.csv`:
| File Name | Sample Type |
|--|--|
| slide_1.svs | pos |
| slide_2.svs |neg  |
|....|...|
| slide_n.svs |neg |

Execute the code in a terminal as follows:
```
python pro_train.py
python pro_test.py
```

Ensure the output files (split folder) followed the directory structure below.

```
./csv/label_example/
    ├──sheet
        ├── train.csv (label)
        ├── test.csv (label)
        └── 91 (output files)
             └── 0
                 └── case_train.csv
                 └── case_val.csv
                 └── case_test.csv
    └──split (output files)
        └── 91
             └── 0
                 └── case_train.csv
                 └── case_val.csv
                 └── case_test.csv
    
```


#### 3. Training and inference step

#### Train IMAN
Adjust the `main.yaml` to set parameters before start training.
```
python main.py
```


#### Inference IMAN
```
python test.py
```



#### 4. Interpretability Analysis
For generating attention heatmaps, adjust the corresponding parameters on `heatmap.py` and run the code as follows.
```
python heatmap.py
```


## License
This Python source code is released under a creative commons license, which allows for personal and research use only. For a commercial license please contact Prof. Ching-Wei Wang. You can view a license summary here:  
http://creativecommons.org/licenses/by-nc/4.0/


## Contact
Prof. Ching-Wei Wang  
  
cweiwang@mail.ntust.edu.tw; cwwang1979@gmail.com  
  
National Taiwan University of Science and Technology

