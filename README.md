## Channel-Aware Cross-Fused Transformer-style Networks (C2T-Net)

<img src="https://caodoanh2001.github.io/assets/img/upar-certificate.jpg" data-canonical-src="https://caodoanh2001.github.io/assets/img/upar-certificate.jpg" width="750" height="500" />

Doanh C. Bui, Thinh V. Le and Hung Ba Ngo

### 1. Prepare the dataset from UPAR challenge

Follow the instruction of data download of organizer [website](https://github.com/speckean/upar_challenge).

The data should be arranged as below tree directory:

```
data
├── phase1
│   ├── annotations
│   ├── Market1501
│   ├── market_1501.zip
│   ├── PA100k
│   └── PETA
├── phase2
│   ├── annotations
│   ├── MEVID
│   └── submission_templates_test
```

### 2. Prepare docker image

Download docker image [here](https://drive.google.com/file/d/1sht0y_6lhzP1IAwUb_CRNtuZom6JZnkx/view).

Run the below command to load the docker image:

```
sudo docker load < upar_hdt.tar
```

Go into the `data` folder, run below command to create a container

```
sudo docker run -d --shm-size 8G --gpus="all" -it --name upar_hdt --mount type=bind,source="$(pwd)",target=/home/data upar_hdt:v0
```

Run the container

```
sudo docker exec -ti upar_hdt /bin/bash
```

Then, follow the step 3 for reproducing the results, and step 4 for training.

### 3. Inference for testing dataset in phase 2:

Download our best checkpoint [here](https://drive.google.com/file/d/1YCHeRhEPcyb6fD9byi3flNFSQDsY2qA0/view?usp=drive_link) (`best_model.pth`). Place it under `checkpoints` folder (we already put it in the docker image).

Run the below file for inference:

```
CUDA_VISIBLE_DEVICES=0 python infer_upar_test_phase.py
```

The results are written in `predictions.csv` file. This file is valid for submission in the codalearn portal.


### 3. Training model

Run the below command for training:

```
CUDA_VISIBLE_DEVICES=0 bash run.sh
```

The checkpoints and logs would be saved at `exp_results/upar/`
