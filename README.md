# yoloproject
from google.colab import drive
drive.mount('/content/gdrive')

# Leave this code uncommented on the very first run of your notebook or if you ever need to recompile darknet again.
# Comment this code on the future runs.
#!git clone https://github.com/kriyeng/darknet/
#%cd darknet

# Check the folder
#!ls

# I have a branch where I have done the changes commented above
#!git checkout feature/google-colab

#Compile Darknet
#!make



# Uncomment after the first run, when you have a copy of compiled darkent in your Google Drive

# Makes a dir for darknet and move there

# Copy the Darkent compiled version to the VM local drive
!cp -r '/content/drive/My Drive/project_folder2/darknet' '/content/'

# Set execution permissions to Darknet
!chmod +x ./darknet


#download files
def imShow(path):
  import cv2
  import matplotlib.pyplot as plt
  %matplotlib inline

  image = cv2.imread(path)
  height, width = image.shape[:2]
  resized_image = cv2.resize(image,(3*width, 3*height), interpolation = cv2.INTER_CUBIC)

  fig = plt.gcf()
  fig.set_size_inches(18, 10)
  plt.axis("off")
  #plt.rcParams['figure.figsize'] = [10, 5]
  plt.imshow(cv2.cvtColor(resized_image, cv2.COLOR_BGR2RGB))
  plt.show()
  
  
def upload():
  from google.colab import files
  uploaded = files.upload() 
  for name, data in uploaded.items():
    with open(name, 'wb') as f:
      f.write(data)
      print ('saved file', name)
def download(path):
  from google.colab import files
  files.download(path)

# Not necessary cell
# Get yolov3 weights
!wget https://pjreddie.com/media/files/yolov3.weights

# Not necessary cell
# Execute darknet using YOLOv3 model with pre-trained weights to detect objects on 'person.jpg'
!./darknet detect cfg/yolov3.cfg yolov3.weights data/person.jpg -dont-show

# Show the result using the helper imgShow()
imShow('predictions.jpg')

!./darknet detect cfg/yolov3.cfg yolov3.weights data/eagle.jpg

imShow('predictions.jpg')


%cd ..

%cd darknet

!wget https://pjreddie.com/media/files/darknet53.conv.74

!git clone https://github.com/EscVM/OIDv4_ToolKit.git

%cd OIDv4_ToolKit/

pip install -r requirements.txt

%cd OIDv4_ToolKit/

!python3 main.py

 !python3 main.py downloader --classes Fish --type_csv train --limit 1000 --multiclass 1

!ls

!python convert_annotations.py

!mv '/content/darknet/OIDv4_ToolKit/OID/Dataset/train/Fish/Label' '/content/darknet/trash'

!mv  '/content/darknet/OIDv4_ToolKit/OID/Dataset/train/Fish/' '/content/darknet/data/obj'

%cd /content/darknet/data/obj/Fish

mv * '/content/darknet/data/obj'

#delete the fish folder

%cd /content/darknet

%cd content/

%cd gdrive

%cd ..

%cd '/content/darknet'

!python generate_train.py

!wget https://pjreddie.com/media/files/darknet53.conv.74

!./darknet detector train data/obj.data cfg/yolov3-custom.cfg backup/yolov3-custom_1000.weights -dont_show


!./darknet detector test data/obj.data cfg/yolov3-custom-test.cfg backup/yolov3-custom_1000.weights fish.jpg 
from IPython.display import Image
Image('predictions.jpg')

!./darknet detector test data/obj.data cfg/yolov3-custom-test.cfg backup/yolov3-custom_1000.weights fish2.jpg 
from IPython.display import Image
Image('predictions.jpg')

!./darknet detector demo data/obj.data cfg/yolov3-custom-test.cfg backup/yolov3-custom_1000.weights Test_ROV_video_h264_decim.mp4 -out_filename results.avi -dont_show



!cp -r '/content/darknet' '/content/gdrive/My Drive/project_folder'
