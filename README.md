# Interpretable Multi-stage Attention DL Network to Predict Malignancy in Cell Blocks and  Cytological Smears of Pleural Effusion
In this study, we proposed an Interpretable Multi-stage Attention Deep Learning (IMADL) network to predict malignancy in cost-efficient cytological smears and cell blocks of pleural effusion from the Biobank of Tri-Service General Hospital, Taipei (TSGH). 


## Associated Publications
Wang et al. (In submission) Interpretable Multi-stage Attention DL Network to Predict Malignancy in Cell Blocks and  Cytological Smears of Pleural Effusion

## Datasets


### Cell Blocks Dataset
Moreover, we also collected 188 cell blocks slides from the Department of Pathology at Tri-Service General Hospital, Taipei, Taiwan and the National Defense Medical Center, Taipei, Taiwan. This cohort covers individuals aged 23 to 109 with 76 male and 112 female patients, respectively. The class distribution is provided as follows, [positive for malignancy (n=70); negative for malignancy (n=118)].

### Cytological Smears Dataset
In this study, we collected 194 cytological smear slides from the Department of Pathology at Tri-Service General Hospital, Taipei, Taiwan and the National Defense Medical Center, Taipei, Taiwan. This cohort covers individuals aged 23 to 109 with 80 male and 114 female patients, respectively. The class distribution is described as follows, [positive for malignancy (n=74); negative for malignancy (n=120)]. 


## Experiment Setup

#### Requirements
- Ubuntu 18.04
- RAM >= 64 GB
- GPU Memory >= 12 GB
- GPU driver version >= 525.125.06
- CUDA version >= 12.0

Import the IMADL virtual environment in conda
```
conda env create --file=IMADL.yaml
```
then enter the environment:
```
conda activate IMADL
```

#### Download
The source code file, configuration file, and models (./IMADL_Cyto_CB/run/.../checkpoint.pth) can be downloaded from the [zip](https://drive.google.com/file/d/1IJXr0naAuo3wHRFGR4U2YZc-1vTDkHCp/view?usp=sharing) file. (For reviewers, the password of the zip file is provided in the "Code Availability" section of the associated manuscript.)

## Steps

#### 1. Bag-wise foreground extraction

Place the Whole slide images in ./WSI/
```
./WSI/
├── slide_1.ndpi
├── slide_2.ndpi
│        ⋮
└── slide_n.ndpi
  
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

The format of the label file can refer to `IMADL/csv/label_example/sheet/train.csv` and `IMADL/csv/label_example/sheet/test.csv`:
| File Name | Sample Type |
|--|--|
| slide_1.ndpi | pos |
| slide_2.ndpi |neg  |
|....|...|
| slide_n.ndpi |neg |

Execute the code in a terminal as follows:
```
python pro_train.py
python pro_test.py
```

Ensure the output files (split folder) follow the directory structure below.

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

#### Train IMADL
Adjust the `main.yaml` to set parameters before start training.
```
python main.py
```


#### Inference IMADL
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

