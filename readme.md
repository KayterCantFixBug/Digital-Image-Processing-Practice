|                 | Digital Image Processing              |
| :-------------- | :------------------------------------ |
| **Library**     | OpenCV2                               |
| **Run Program** | Open every single folder to run demo. |

---

|                                        |                                                Directory                                                | Description                                                                                   |
| :------------------------------------- | :-----------------------------------------------------------------------------------------------------: | --------------------------------------------------------------------------------------------- |
| **Basic**                              |          [DIR](https://github.com/kaytervn/Digital-Image-Processing-Practice/tree/main/co_ban)          | Display images, face and eyes regconition, take camera screenshots.                           |
| **Face Detection**                     |     [DIR](https://github.com/kaytervn/Digital-Image-Processing-Practice/tree/main/dnn_face_detect)      | Face detection with presenting eye, nose, and mouth coordinates.                              |
| **Object Detection**                   |    [DIR](https://github.com/kaytervn/Digital-Image-Processing-Practice/tree/main/dnn_object_detect)     | Import custom datasets, create tkinter GUI, local web service to upload images for detection. |
| **Face Detection with Custom Dataset** | [DIR](https://github.com/kaytervn/Digital-Image-Processing-Practice/tree/main/nhan_dang_khuon_mat_onnx) | Collect image stocks from people to create a dataset for training detection.                  |
| **Negative Image Processing**          |     [DIR](https://github.com/kaytervn/Digital-Image-Processing-Practice/tree/main/xu_ly_anh_am_ban)     | Browse an image to export negative version.                                                   |

<h1 align="center">Object Detection</h1>

<h2>Run file `object_detection.py` on CMD:</h2>

**Image Detection:**

```cmd
python object_detection.py --input=image01.jpg --model=yolov8n.onnx --scale=0.00392 --width=640 --height=640 --rgb --postprocessing=yolov8 --classes=object_detection_classes_yolo.txt
```

**Real time Camera:**

```cmd
python object_detection.py --input= --model=yolov8n.onnx --scale=0.00392 --width=640 --height=640 --rgb --postprocessing=yolov8 --classes=object_detection_classes_yolo.txt
```

<h2>Run on VS Code (Code Editor):</h2>

**1.** At `Debug` section: Current File -> Create file `launch.json`, it automatically appear in the folder `.vscode`

**2.** Open `launch.json`, add arguments with a specific `model` and a `classes` file name:

```json
   "args": [
   "--input",
   "image06.jpg",
   "--model",
   "ktr_dataset.onnx",
   "--scale",
   "0.00392",
   "--width",
   "640",
   "--height",
   "640",
   "--rgb",
   "--postprocessing",
   "yolov8",
   "--classes",
   "ktr_dataset.txt"
   ]
```

- Real time Camera:
  - Change the figure of video capture to 0 in file `object_detection.py`:

```py
cap = cv.VideoCapture(0)
```

**3.** Click `Run` on the top menu bar -> Run Without Debugging

<h1>Web Service</h1>

[<i>You can change the model `best.pt`</i>]

**1.** Run CMD and cd to the path containing the folder `web_service`:

```cmd
cd D:\..\..\dnn_object_detect\web_service
python object_detector.py
```

**2.** Finally, access this URL: `http:///localhost:8080`

<h1>Labeling Images</h1>

**1.** Format all the images file into 640x640 images by running file `chuan_hoa_anh_640x640.py` in the folder `nhan_dang_trai_cay`.

**2.** Install source code: https://github.com/HumanSignal/labelImg

**3.** Run CMD and cd to the folder `labelImg`:

```cmd
cd D:\..\..\labelImg
```

**4.** Then, enter this command line:

```cmd
pyrcc5 -o libs/resources.py resources.qrc
```

**5.** Finally, run file `labelImg.py` to start the image labeling app (cd to the path containing an `images folder` and a `class name` file):

```cmd
python labelImg.py D:\..\..\trai_cay_640x640\sau_rieng D:\..\..\trai_cay.txt
```

<h1>Training YOLOv8</h1>

|Tutorial|                                                                                                                                                            |
| :-------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Free Code Camp**                | [LINK](https://www.freecodecamp.org/news/how-to-detect-objects-in-images-using-yolov8/)                                                                                |
| **Roboflow (tác giả của yolov8)** | [LINK](https://colab.research.google.com/github/roboflow-ai/notebooks/blob/main/notebooks/train-yolov8-object-detection-on-custom-dataset.ipynb#scrollTo=FyRdDYkqAKN4) |

<h2>Training on Google Colaboratory</h2>

**1.** Upload the dataset to Google Drive.

**2.** Create a notebook file `.ipynb`.

**3.** On the menu bar, Edit -> Notebook settings -> tick `T4 GPU`.

**4.** Enter these command lines:

**Connect to Google Drive**

```py
from google.colab import drive
drive.mount('/content/drive')
```

**Move to the path containing your dataset**

```py
%cd '/content/drive/MyDrive/TrainingYOLOv8/trai_cay_yolo8'
```

**Install library `ultralytics`**

```py
!pip install ultralytics
```

**Import model `yolov8m.pt`**

```py
from ultralytics import YOLO
model = YOLO("yolov8m.pt")
```

**Start training**

```py
model.train(data="data.yaml", epochs=30)
```

**Move to the folder containing trained model**

```py
%cd '/content/drive/MyDrive/TrainingYOLOv8/trai_cay_yolo8/runs/detect/train2/weights'
```

**Format the model to `.onnx`**

```py
model = YOLO("best.pt")
path = model.export(format="onnx")
```

**5.** Finally, download model `best.onnx`.
