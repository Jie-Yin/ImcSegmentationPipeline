[![DOI](https://zenodo.org/badge/103582813.svg)](https://zenodo.org/badge/latestdoi/103582813)
# A flexible  image segmentation pipeline for heterogeneous multiplexed tissue images based on pixel classification

## Introduction

The pipeline is based on CellProfiler (http://cellprofiler.org/, tested v4.0.6) for segmentation and Ilastik (http://ilastik.org/, tested v1.3.5) for pixel classification. 
It is streamlined by using the specially developed `imctools` python package (https://github.com/BodenmillerGroup/imctools, >v2.1) as well as custom CellProfiler modules (https://github.com/BodenmillerGroup/ImcPluginsCP, release v4.2.1).

This repository showcases the basis of the workflow with step-by-step instructions. 
For a dockerized version of the pipeline, check out [steinbock](https://github.com/BodenmillerGroup/steinbock).

This pipeline was developed in the Bodenmiller laboratory at the University of Zurich (http://www.bodenmillerlab.org/) to segment hundreds of highly multiplexed imaging mass cytometry (IMC) images.
However we think that this concept also works well for other multiplexed imaging modalities.

## Usage

For the main part of the analysis, you will need to install [Ilastik](https://www.ilastik.org/download.html) and [CellProfiler](https://cellprofiler.org/releases).

Before being able to pre-process the data, you will need to setup the environment:

1. [Install conda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/)

2. Clone the repository: 

```bash
git clone https://github.com/BodenmillerGroup/ImcSegmentationPipeline.git
```

3. Setup the conda environment: 

```bash
cd ImcSegmentationPipeline
conda env create -f conda_imctools.yml
```

4. Obtain the IMC-specific [CellProfiler plugins](https://github.com/BodenmillerGroup/ImcPluginsCP) by directly downloading them via:

```bash
git submodule update --init --recursive
```

5. Configure `CellProfiler` to use the plugins by opening the `CellProfiler` GUI, selecting `Preferences` and setting the `CellProfiler plugins directory` to `PATHTO/ImcSegmentationPipeline/resources/cp_plugins/ImcPluginsCP/plugins`

6. Activate the environment created in .3 and start a jupyter instance

```bash
conda activate ImcSegmentationPipeline
jupyter notebook
```

This will automatically open a jupyter instance at `http://localhost:8888` in your browser.
From there, you can open the `preprocessing.ipynb` notebook and start the data pre-processing.

In brief, the main analysis steps include:

1. Pre-processing of the raw images to create `.ome.tiffs` and `.tiff` stacks for ilastik training and measurement (python).   
2. Ilastik pixel classification based on random crops of the images (CellProfiler, Ilastik).  
3. Image segmentation based on the classification probabilities (CellProfiler).  
4. Measurement and export of cell-specific features, such as marker expression (CellProfiler).  

## Documentation

For a more detailed overview on the individual analysis steps, please visit [https://bodenmillergroup.github.io/ImcSegmentationPipeline/](https://bodenmillergroup.github.io/ImcSegmentationPipeline/).

This pipeline was presented at the 2019 Imaging Mass Cytometry User Group Meeting.
[The slides can be downloaded here](https://drive.google.com/file/d/1ajPzlJ2CUj6sFYSOq0HR2dOJehHIlCJt/view).
The slides briefly explain why we chose this approach to image segmentation and provide help to run the pipeline.

## Changelog

For changes in specific releases, please refer to the [CHANGELOG](CHANGELOG.md).
        
## License

We [freely share](LICENSE) this pipeline in the hope that it will be useful for others to perform high quality image segmentation and serve as a basis to develop more complicated open source IMC image processing workflows. 
In return we would like you to be considerate and give us and others feedback if you find a bug/issue and [raise a GitHub Issue](https://github.com/BodenmillerGroup/ImcSegmentationPipeline/issues) on the affected projects or on this page.

## Contributing

To contribute to this work, please fork the repository, make changes to it and open a pull request.

## Citation

If you use this workflow for your research, please cite us:

```
@misc{ImcSegmentationPipeline,
    author       = {Vito RT Zanotelli, Bernd Bodenmiller},
    title        = {{ImcSegmentationPipeline: A pixel-classification based multiplexed image segmentation pipeline}},
    month        = Sept,
    year         = 2017,
    doi          = {10.5281/zenodo.3841961},
    version      = {0.9},
    publisher    = {Zenodo},
    url          = {https://doi.org/10.5281/zenodo.3841961}
    }
```

