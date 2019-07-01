# Improved MalenoV
<h3>The original MalenoV data, source code and instructions can be found at: https://github.com/bolgebrygg/MalenoV </h3>

The souce code was developed on Python3. First, ensure that GPU resources are available on the server. Scond, run `pip install -r requirements.txt` to install all necessary packages. The project directory is structured as follows:

```
project
│   README.md
│   requirements.txt
|   train_demo.py
│   predict_demo.py
└───data
    │   F3_entire.segy
    │   *.pts
```

<h3> Training models </h3>
To run the training job, run `python train_demo.py`. Inside `train_demo.py`, one can specify input parameters, and customize the CNN model. Speficially, on the bottom part of the code block (~line 1555), one can find `filenames`, which specifies the relative path to the segy data; `cube_incr` specifies the **radius** of the cubes. 

In `train_dict`, `files` specifies the list of files that are labeled data points (please refer to data provided from https://github.com/bolgebrygg/MalenoV for labeled data format); `num_tot_iterations` specifies the number of times we draw samples from the seismic cube (typically leave it to 1); `epochs` specifies the number of epochs for training; `num_train_ex` specifies the total number of training and validation data (a training/validation split of 0.2 is used but can be easily changed); `batch_size` specifies the size of the mini-batch for each iteration; `data_augmentation` is set to `False` since it is not implemented at this moment; `save_model` specifies if we'd like to save the keras model into .h5 format; `save_location` specifies the path to the saved model if we set `save_model` to `True`; `test_size` specifies the number of test data; `sample_step` specifies the step size used in sparse sampling (set to 1 if one wish to do continous sampling).

<h3> Predicting models </h3>

To run the predicting job, run `python predict_demo.py`. This file is very similar to `train_demo.py`; we will eventually merge the two files in the future. Again, on the bottom of the code block, one can find `pred_dict`. In this variable, `keras_model` specifies the relative path to the saved .h5 model; `section_edge` specifies the four coordinates of the 2D seismic section that is to be classified/visualized; `plot_type`, `plot_ref` and `cord_syst` are additional parameters that contrain the 2D slice which is to be examined, and they have to be consistent with `section_edge`; `num_class` and `sample_step` need to be consistent with the parameters defined during the model training; `save_pred` and `save_location` specify whether or not, and where to save the predictions.

<h3> Notes </h3>

Only `train_dict` is used during training, and only `pred_dict` is used in the prediction process. However, be sure to select the correct `mode` in `output_dict1` before running `train_demo.py` or `predict_demo.py`.
