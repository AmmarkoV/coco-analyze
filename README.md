## coco-analyze Repository
This repository contains the code release from the paper [***Benchmarking and Error Diagnosis in Multi-Instance Pose Estimation***](http://www.vision.caltech.edu/~mronchi/projects/PoseErrorDiagnosis).

If you find this work useful please cite our paper:
```
@InProceedings{Ronchi_2017_ICCV,
author = {Ronchi, Matteo Ruggero and Perona, Pietro},
title = {Benchmarking and Error Diagnosis in Multi-Instance Pose Estimation},
booktitle = {The IEEE International Conference on Computer Vision (ICCV)},
month = {Oct},
year = {2017}
}
```

### Important Content:
 - `pycocotools/COCOanalyze.py`: wrapper of the COCOeval class for multi-instance keypoint estimation error analysis.
 - `COCOanalyze_demo.ipynb`: ipython notebook showing how to use COCOanalyze as a standalone class.
 - `analysisAPI`: API using COCOanalyze for an extended analysis.
 - `run_analysis.py`: script generating a pdf summary of the extended analysis.

### Installation
Use the Makefile to install the coco-analyze api:
 - `make all` will compile and install locally. (<b>RECOMMENDED</b>)
 - `make install` will install the api to the Python site-packages folder. <b>NOTE</b> This might override your current pycocotools installation.

### Usage
To run the extended multi-instance keypoint estimation error analysis: update the paths of the detections and annotations and execute the command line.

    [annFile]  -> ./annotations/person_keypoints_val2014.json
    [dtsFile]  -> ./detections/fakekeypoints100_keypoints_val2014_results.json
    [saveDir]  -> ./results/fakekeypoints100
    [teamName] -> fakekeypoints100
    [version]  -> 1.0
    $ python3 run_analysis.py [annFile] [dtsFile] [saveDir] [teamName] [version]

### Results
 - A summary file called `[teamName]_performance_report.tex` will be created once the analysis is complete.
 - All the generated plots are stored using `[saveDir]` as the base directory.
 - Additional *std_output* information regarding the analysis can be found in the text files named `std_out.txt`.

### Automatically Generated Performance Reports
You can find examples of the reports generated by the analysis code:
 - [Mask-RCNN](http://www.vision.caltech.edu/~mronchi/projects/PoseErrorDiagnosis/Reports/2017_MASKRNN.pdf)
 - [CMU](http://www.vision.caltech.edu/~mronchi/projects/PoseErrorDiagnosis/Reports/2016_CMU.pdf)
 - [GRMI](http://www.vision.caltech.edu/~mronchi/projects/PoseErrorDiagnosis/Reports/2016_GRMI.pdf)

### Notes:
 - The [`./pycocotools/COCOeval`](https://github.com/matteorr/coco-analyze/blob/release/pycocotools/cocoeval.py) class contained in this repository is a modified version of the original [mscoco COCOeval class](https://github.com/pdollar/coco/blob/master/PythonAPI/pycocotools/cocoeval.py).
 - The duration of the full analysis depends on the number of detections and size of the ground-truth split.
 - You can comment out parts of [`run_analysis.py`](https://github.com/matteorr/coco-analyze/blob/release/run_analysis.py#L91-L120) to run the analysis only for specific types of error.
 - Set `USE_VISIBILITY_FOR_PLOTS=True` in [localizationErrors.py](https://github.com/matteorr/coco-analyze/blob/release/analysisAPI/localizationErrors.py#L159) if during the analysis you wish to visualize only the keypoints whos visibility flag is 1 (visible but occluded), or 2 (visible). Check [issue #14](https://github.com/matteorr/coco-analyze/issues/14) for more details.
