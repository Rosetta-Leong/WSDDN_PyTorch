# WSDDN_Pytorch
Weakly Supervised Deep Detection Networks(CVPR 2016): Implementation in PyTorch 
***
# Project Basically Completed :)
## Environment(Common packages are not listed here)
    chainercv
    Pillow
    black
    isort
    albumentations==0.4.3
    Cython
    rope
    tqdm
    tensorboardX

## Implementation Details

### 1) Training and Model:
- First 10 epochs `lr = 10^-5`, last 10 epochs `lr = 10^-6`
- Batch size: **1**(and its all regions)
- Spatial regulariser isn't added
- Using EdgeBoxes(**EB**) to generate candidate regions
- Using **EB Score** to add a scaling layer in this model
- Base_net contains `vgg16` and `alexnet`

### 2) Data Processing:
- Resize images to five different scales : {480, 576, 688, 864, 1200}
- Apply random horizontal flips



## Dataset Download
```bash
./dataset.sh
```


## Training Steps

```bash
python train.py --base_net vgg
```

## Evaluation Steps

```bash
python test.py --base_net vgg --state_path weight/vgg_epoch_20.pt
```

## Experiments

- Our Result (`base_net = VGG16`)  **31.0** mAP
- Close to `EB + Box Sc.` case with model **L**, which reported **30.4** mAP in the paper

| aero | bike  | bird | boat | bottle | bus  | car  | cat  | chair | cow  | table | dog  | horse | mbike | person | plant | sheep | sofa | train | tv   | mean     |
|------|-------| ---- | ---- | ------ | ---- | ---- | ---- | ----- | ---- | ----- | ---- | ----- | ----- | ------ | ----- | ----- | ---- | ----- | ---- | -------- |
| 37.6 | 44.3  | 22.7 | 28.1 | 12.9   | 56.0 | 49.3 | 29.2 | 6.3   | 32.8 | 22.1  | 22.5 | 33.8  | 51.6  | 7.0    | 14.3  | 29.9  | 31.7 | 47.4  | 40.5 | **31.0** |