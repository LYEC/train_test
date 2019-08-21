# train_test

!pip install pillow

!pip install lxml

!pip install Cython

!pip install jupyter

!pip install matplotlib

!pip install pandas

!pip install opencv-python

!pip install tensorflow


!git clone https://github.com/tensorflow/models/

%cd models/research/object_detection

!wget http://download.tensorflow.org/models/object_detection/faster_rcnn_inception_v2_coco_2018_01_28.tar.gz

!tar -xvzf faster_rcnn_inception_v2_coco_2018_01_28.tar.gz

!rm -rf faster_rcnn_inception_v2_coco_2018_01_28.tar.gz

import os
os.environ['PYTHONPATH'] = "{}/content/models:/content/models/research:/content/models/research/slim".format(os.environ['PYTHONPATH'])

%cd ..

!protoc ./object_detection/protos/*.proto --python_out=.

!protoc --version

!python3 setup.py build

!python3 setup.py install

cd ..

!mkdir iha

cd iha

!mkdir iha_img

!cp -r /content/drive/My*Drive/detecnet_data/train_detect/images /content/iha/iha_img

import sys
import os

directory = "/content/iha/iha_img/images/"
test = os.listdir( directory )

for item in test:
    if item.endswith(".xml"):
        os.remove( os.path.join( directory, item ) )
print("sildim.")

cd /content/iha/iha_img/images

!sudo apt install unzip

!unzip train.zip

!mkdir test

cd test

!cp -r /content/drive/My*Drive/detecnet_data/val_detect/images  /content/iha/iha_img/test

import sys
import os

directory = "/content/iha/iha_img/test/images/"
test = os.listdir( directory )

for item in test:
    if item.endswith(".xml"):
        os.remove( os.path.join( directory, item ) )
print("sildim.")

cd /content/iha/iha_img/test/images

!unzip val.zip

cd /content/iha

!python xml_to_csv.py

// train için
!python generate_tfrecord.py

// test için
!python generate_tfrecord.py

!cp train.record  /content/drive/My*Drive/derin

!cp test.record  /content/drive/My*Drive/derin

!python train.py --logtostderr --train_dir=training_dir/ --pipeline_config_path=faster_rcnn_inception_v2_coco.config

https://colab.research.google.com/drive/1WcOqCoKV0BvrUnFSOxXz1glFaE3bUq4L
