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

You need 2 folders: images and txt annottations in yolo format: `class_id center_x center_y width height`

Download prepared dataset:

- [Train28](https://www.google.com/)
- [Val28](https://www.google.com/)
- [Train5](https://www.google.com/)
- [Val5](https://www.google.com/)


### 2. Checkpoints

|Model |size<br><sup>(pixels) |mAP<sup>val<br>0.5:0.95 |mAP<sup>val<br>0.5 |mAP_5<sup>val<br>0.5:0.95 |mAP_5<sup>val<br>0.5:0.95 |Speed<br><sup>V100 b32<br>(ms) |params<br><sup>(M)|
|---                    |---  |---    |---    |---    |---    |---    |---    |
|[YOLOv5x][assets]      |832x448  |28.0   |45.7   |**45** |**6.3**|**0.6**|**1.9**|
|[YOLOv5x][assets]      |832x448  |37.4   |56.8   |98     |6.4    |0.9    |86.7  |  
|[YOLOv5x6][assets]      |1280x704  |37.4   |56.8   |98     |6.4    |0.9    |140.7   | 
|[YOLOv5x6][assets]      |1280x704  |37.4   |56.8   |98     |6.4    |0.9    |140.7   | 



### 3. Training

```bash
python train.py --data config28.yaml --batch-size 16
```

### 4. Evalutation

```bash
python val.py --data config28.yaml --weights yolov5x.pt
```







