# DeepTouch

This is the source code to train and evaluate VQ-VAE on haptic stimuli explored
by human participants.

## Downloading the Dataset

The dataset can be downloaded from this link 
http://www.allpsych.uni-giessen.de/DeepTouch/DeepTouch.zip . The password for
extraction is "AnnaMatteo".

The content of this zip file:
 - gt (the directory containing touch durations explored by participants)
 - img (the directory containing haptic stimuli, the map reliefs)
 - all_imgs.txt (each line corresponds to one image and ground-truth. lines are
 comma separated: <img_index>,<participant_number>,<trial_number>,<gt_index>.)
 - gts.txt (list of png files in the gt folder)
 - imgs.txt (list of png in the img folder)

## Requirements

We have run this code with PyTorch 1.5.1 but it should work with other versions
as well. 

## Train 

Navigate to the "src" folder and execute the following command:

`python main.py <DATA_DIR> --test_inds 1 --batch-size 2 --epochs 100 
-k 64 -kl 64 --hidden 64`

 - `<DATA_DIR>` is the path to the extracted dataset containing the above 
 described folders.
 - `test_inds` is the flag for stating which participant should be used for 
 testing. There are in total 12 participants. For instance, `--test_inds 1 8 12`
 means the training pipeline excludes the data of three participants (1, 8, 12),
 and uses them for validation. This is useful for n-fold cross-validation.
  - `k` corresponds to the number of vectors in the embedding space.
  - `kl` corresponds to the lenght of vectors in the embedding space.
  - `hidden` corresponds to the number of kernels in de/convolution layers. 

The output is stored in "results" directory.

To see a list of all supporting flags execute `python main.py -h`

## Test

To visualise networks prediction navigate to the "src" folder and execute the
following command:

`python main.py <DATA_DIR> --pred <MODEL_PATH>  --test_inds 1 8 12`

 - `<DATA_DIR>` as described above.
 - `test_inds` as described above.
 - `<MODEL_PATH>`path of the saved checkpoitns (those analaysed by use are in
 "models" directory).

The output is stored in "results" directory.