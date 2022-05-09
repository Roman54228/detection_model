# Detection model

<details open>
<summary>Install</summary>

Clone repo and install [requirements.txt](https://github.com/ultralytics/yolov5/blob/master/requirements.txt) in a
[**Python>=3.7.0**](https://www.python.org/) environment, including
[**PyTorch>=1.7**](https://pytorch.org/get-started/locally/).

```bash
git clone https://github.com/Roman54228/detection_model  # clone
cd detection_model
pip install -r requirements.txt  # install
```

</details>


### 1. Dataset

Configure root path path to your dataset in config `data/config.yaml`.

You need 2 folders: images and `.txt` annotations in yolo format: `class_id center_x center_y width height`

Download prepared dataset:

- [Train28](https://www.google.com/)
- [Val28](https://www.google.com/)
- [Train5](https://www.google.com/)
- [Val5](https://www.google.com/)

Running `train.py`, `eval.py` will scan dataset directory and put everything into `.cache` file which is used for training or eval. It is able to manage images with  no annotations and interpret as there's no objects.

There is possibility for more flexible dataset tuning. You can split data as you need and list all folders in config. It is important that the name of the folder with the images matches name of the folder with labels.
```bash
train: # train images (relative to 'path')  
  - images/train2012
  - images/train2007
  - images/val2012
  - images/val2007
val: # val images (relative to 'path')  
  - images/test2007
test: # test images (optional)
  - images/test2007
```
### 2. Checkpoints

|Model |size<br><sup>(pixels) |mAP<sup>val<br>0.5:0.95 |mAP<sup>val<br>0.5  |Speed<br><sup>V100 bs1<br>(ms) |params<br><sup>(M)|
|---                    |---  |---    |---      |---    |---    |
|[28classes_YOLOv5x](https://drive.google.com/file/d/1MLKcglp6ztW-cmW7E_ohXE00plnaPMxf/view?usp=sharing)      |832x448  |46.9   |59.0  |--|86.7|
|[5classes_YOLOv5x](https://drive.google.com/file/d/1sXnMCShBicZbrrEuoDWA_cgu_VKyFn88/view?usp=sharing)      |832x448  |40.5   |54.4    |--    |86.7  |  
|[28classes_YOLOv5x6](https://drive.google.com/file/d/1WG5IDw0e3o-zbT58VPs8tpdF_jiK9yBG/view?usp=sharing)      |1280x704  |41.0   |57.8     |--    |140.7   | 




### 3. Training
  
Automatically logs mAP, AP_per_class and media files into wandb.

```bash
python train.py --data config28.yaml --batch-size 16
```
All training results are saved to `runs/train/` with incrementing run directories, i.e. `runs/train/exp2`, `runs/train/exp3` etc.
Use the largest `--batch-size` possible, or pass `--batch-size -1` for YOLOv5 [AutoBatch](https://github.com/ultralytics/yolov5/pull/5092). 

Modify training hyperpaameters in `data/hyp` - augmentations, optimizer and loss.
  
Example of mosaic augmentation:

### 4. Evalutation

```bash
python val.py --data config28.yaml --weights yolov5x.pt
```







