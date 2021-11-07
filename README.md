# flexconn
===========================================================
When using this code, please cite the paper:

S. Roy, J. A. Butman, D. S. Reich, P. A. Calabresi, D. L. Pham
"Multiple Sclerosis Lesion Segmentation from Brain MRI via Fully Convolutional Neural Networks",
submitted to NeuroImage.

===========================================================

FLEXCONN is Fast Lesion  EXtraction using COnvolutional Neural Networks.
There are two scripts, FLEXCONN_Train.py (for training) and FLEXCONN_Test.py
(for prediction). The scripts are written in python and the neural network is 
implemented in Tensorflow/Keras.

1) Please update the python package requirements with the provided requirement.txt,
    pip install -r requirements.txt
    
2) 21 atlases (from 5 subjects) are provided with this code. The images are
same as the "training data" of the ISBI 2015 lesion segmentation challenge, 
and can also be obtained from here,
    https://smart-stats-tools.org/lesion-challenge-2015
    
3) Two trained models with 35x35 patches (in voxels) using these 21 atlases 
are provided.  Since the atlases contain two sets of masks, two CNN models 
are trained separately with each set of masks.

4) A separate set of two trained models using 61 atlases (14 subjects) are 
also provided. These atlas images and masks are not publicly released. They are
the "test data" of the ISBI 2015 lesion segmentation challenge. 

5) Please see the usage of training and prediction via
    python FLEXCONN_Train.py -h
    python FLEXCONN_Test.py -h
    
The trained models can be generated via the following command,
    python FLEXCONN_Train.py --atlasdir ./atlas_with_mask1/ --natlas 21 \ 
                --psize 35x35 --o ./atlas_with_mask1/
    python FLEXCONN_Train.py --atlasdir ./atlas_with_mask2/ --natlas 21 \ 
                --psize 35x35 --o ./atlas_with_mask2/      
       
An example subject is also provided with T1-w MPRAGE and FLAIR. The associated
lesion masks and memberships can be generated via the following command,
    python FLEXCONN_Test.py --models Trained_models/21atlases/atlas_with_mask*/*.h5 \ 
                --t1 MPRAGE.nii.gz --fl FLAIR.nii.gz --o ./
 
6) Note that both of these trained models were trained on 1mm^3 images. Therefore 
if your test data has different resolution, you have to retrain the models on 
the desired resolution with a reasonable patch size. An easy way would be to 
resample the atlases and masks to the desired resolution. Also 35x35 patch size 
(in voxels) corresponds to 3.5cm x 3.5cm patches. Please use comparable patch 
sizes if training or testing with different resolution images.

   
7) If you want to use your own atlases, please rename them to the following
naming procedure, atlasXX_T1.nii.gz, atlasXX_FL.nii.gz, atlasXX_mask.nii.gz, XX=1,2,3..
