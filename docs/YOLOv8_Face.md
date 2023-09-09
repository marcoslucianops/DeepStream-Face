# YOLOv8-Face usage

**NOTE**: The yaml file is not required.

* [Convert model](#convert-model)
* [Edit the config_infer_primary_yoloV8_face file](#edit-the-config_infer_primary_yolov8_face-file)

##

### Convert model

#### 1. Download the YOLOv8 repo and install the requirements

```
git clone https://github.com/ultralytics/ultralytics.git
cd ultralytics
pip3 install -r requirements.txt
python3 setup.py install
pip3 install onnx onnxsim onnxruntime
```

**NOTE**: It is recommended to use Python virtualenv.

#### 2. Copy conversor

Copy the `export_yoloV8_face.py` file from `DeepStream-Yolo-Face/utils` directory to the `ultralytics` folder.

#### 3. Download the model

Download the `pt` file from [YOLOv8-Face](https://github.com/derronqi/yolov8-face) repo.

**NOTE**: You can use your custom model.

#### 4. Convert model

Generate the ONNX model file (example for YOLOv8n-Face)

```
python3 export_yoloV8_face.py -w yolov8n-face.pt --dynamic
```

**NOTE**: To change the inference size (defaut: 640)

```
-s SIZE
--size SIZE
-s HEIGHT WIDTH
--size HEIGHT WIDTH
```

Example for 1280

```
-s 1280
```

or

```
-s 1280 1280
```

**NOTE**: To simplify the ONNX model (DeepStream >= 6.0)

```
--simplify
```

**NOTE**: To use dynamic batch-size (DeepStream >= 6.1)

```
--dynamic
```

**NOTE**: To use explicit batch-size (example for batch-size = 4)

```
--batch 4
```

#### 5. Copy generated files

Copy the generated ONNX model file to the `DeepStream-Yolo-Face` folder.

##

### Edit the config_infer_primary_yoloV8_face file

Edit the `config_infer_primary_yoloV8_face.txt` file according to your model (example for YOLOv8n-Face)

```
[property]
...
onnx-file=yolov8n-face.onnx
...
```

**NOTE**: The **YOLOv8-Face** resizes the input with center padding. To get better accuracy, use

```
[property]
...
maintain-aspect-ratio=1
symmetric-padding=1
...
```
