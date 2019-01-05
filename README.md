# adversarial_object_detection
Code for our WACV paper "Unsupervised Adversarial Visual Level Domain Adaptation for Learning Video Object Detectors from Images"

Paper Link: https://arxiv.org/pdf/1810.02074.pdf


GANs folder: gans/
Object Detectors folder: detectors/


# Proposed model:

1)	Firstly we use Adversarial Networks for domain adaptation. The folder gans/ contains codes of both Cycle GAN and Forward GAN which are tested in our paper for adaptation from image to video domains.


```
cd gans/
```

Download voc training set images into datasets/voc2yto folder. (only images are sufficient, as it is an unsupervised learning) 
```
wget http://host.robots.ox.ac.uk/pascal/VOC/voc2007/VOCtrainval_06-Nov-2007.tar
```

Download youtube training set images into datasets/voc2yto folder from below site.
```
https://data.vision.ee.ethz.ch/cvl/youtube-objects/
```

To train:
```
python train.py --dataroot ./datasets/voc2yto --name voc2yto_cyclegan --model cycle_gan 
```

To test:
```
python test.py --dataroot ./datasets/voc2yto --name voc2yto_cyclegan --model cycle_gan
```

Secondly train the transformed image domain jpgs using two object detectors present in the detectors/ folder. Later test the trained model on youtube test images.

```
cd detectors/
```

Faster RCNN:
```
cd Faster-RCNN_TF
```

To train and test:
```
cd $FRCN_ROOT
./experiments/scripts/faster_rcnn_end2end.sh $DEVICE $DEVICE_ID VGG16 pascal_voc
```

RFBNet:
```
cd PytorchSSD
```

To train and test:
```
python train_test.py -d VOC -v RFB_vgg -s 300
```


2) 	Second proposed idea contains use of conditional cycle GAN, which is use of cycle GAN to transform each class images separately, train them and test


Later we also used Corloc measure to compare segmentation results on both Youtube-Objects and Youtube-Objects Subset dataset.

Below grabcut algorithm is used while calculating Corloc measure: https://docs.opencv.org/trunk/d8/d83/tutorial_py_grabcut.html


# Baseline Results:
Use the object detectors in the detectors/ folder.
Test Set: Youtube Object Test Dataset

1) Train on Original VOC(image domain) images and test. (Lower bound)
2) Domain Adapt the VOC images using Forward GAN(without cycle consistent loss), train the object detectors using the transformed images and test.
3) Train on Original Youtube(video domain) images and test. (Upper bound)
