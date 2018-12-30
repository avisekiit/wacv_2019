# adversarial_object_detection
Code for our WACV paper "Unsupervised Adversarial Visual Level Domain Adaptation for Learning Video Object Detectors from Images"

Paper Link: https://arxiv.org/pdf/1810.02074.pdf


GANs folder: gans/
Object Detectors folder: detectors/


# Baseline Results:
Use the object detectors in the detectors/ folder.
Test Set: Youtube Object Test Dataset

1) Train on Original VOC(image domain) images and test. (Lower bound)
2) Domain Adapt the VOC images using Forward GAN(without cycle consistent loss), train the object detectors using the transformed images and test.
3) Train on Original Youtube(video domain) images and test. (Upper bound)

# Proposed model:

1)	Firstly we use Adversarial Networks for domain adaptation. The folder gans/ contains codes of both Cycle GAN and Forward GAN which are tested in our paper for adaptation from image to video domains.

	Secondly train the transformed image domain jpgs using two object detectors present in the detectors/ folder. Later test the trained model on youtube test images.

2) 	Second proposed idea contains use of conditional cycle GAN, which is use of cycle GAN to transform each class images separately, train them and test


Later we also used Corloc measure to compare segmentation results on both Youtube-Objects and Youtube-Objects Subset dataset.

Below grabcut algorithm is used while calculating Corloc measure: https://docs.opencv.org/trunk/d8/d83/tutorial_py_grabcut.html


