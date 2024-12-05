# CC-GPX: Extracting High-Quality Annotated Geospatial Data from Common Crawl

[![DOI](https://zenodo.org/badge/802180311.svg)](https://doi.org/10.5281/zenodo.14243609)
[![ACM Digital Library](https://img.shields.io/badge/ACM%20Digital%20Library-10.1145/3678717.3691215-green)](https://dl.acm.org/doi/10.1145/3678717.3691215)

📄 This is the official code repository for the short paper titled 'CC-GPX: Extracting High-Quality
Annotated Geospatial Data from Common Crawl', presented at SIGSPATIAL'24 in Atlanta, GA.
The pre-print is available [on arXiv](https://arxiv.org/abs/2405.11039), and the final
paper in the [ACM Digital Library](https://dl.acm.org/doi/10.1145/3678717.3691215).

✍️ Authors: [Ilya Ilyankou](https://ilyankou.com), [Meihui Wang](https://github.com/Ceciliawangwang), Stefano Cavazzi, and James Haworth

## Abstract
The Common Crawl (CC) corpus is the largest open web crawl
dataset containing 9.5+ petabytes of data captured since 2008. The
dataset is instrumental in training large language models, and as
such it has been studied for (un)desirable content, and distilled for
smaller, domain-specific datasets. However, to our knowledge, no
research has been dedicated to using CC as a source of annotated
geospatial data. In this paper, we introduce an efficient pipeline
to extract annotated user-generated tracks from GPX files found
in CC, and the resulting multimodal dataset with 1,416 pairings
of human-written descriptions and MultiLineString vector data
from the 6 most recent CC releases. The dataset can be used to
study people's outdoor activity patterns, the way people talk about
their outdoor experiences, and for developing trajectory generation
or track annotation models.

![Example routes with descriptions from the paper](./other/figures.png)

## Setup

We recommend running the notebooks in a separate virtual environment. Using [`conda`](https://docs.conda.io/projects/conda/en/stable/user-guide/install/index.html),

```shell
# Navigate to the project folder
cd cc-gpx

# Create a new virtual environment
conda env create -f environment.yml

# Activate that new virtual environment
conda activate cc-gpx

# Run Jupyter (will open in your default browser)
jupyter lab
```

## Dataset

Run the notebooks in order to build the final GeoPackage dataset with the following fields:

|#|Property|Description|
|--|--|--|
1 | url | URL of the GPX file
2 | warc_file | CC WARC file with GPX file
3 | warc_offset | GPX file position in WARC
4 | warc_len | GPX file byte length
5 | country | Country name as determined by the first point in the track intersecting [geoBoundaries](https://www.geoboundaries.org/)
6 | desc | Original track description
7 | desc_lang | Track description language code, as determined by [pycld2](https://github.com/aboSamoor/pycld2)
8 | desc_en | Track description translated into English
9 | elev_source | GPS if elevation is recorded by device; DEM if determined later from Shuttle Radar Topography Mission
10 | elev_highest | Track’s highest point, m
11 | elev_lowest | Track’s lowest point, m
12 | uphill | Cumulative elevation gain, m
13 | downhill | Cumulative elevation loss, m
14 | length_2d | Track length disregarding elevation, m
15 | length_3d | Track length accounting for elevation, m
16 | is_circular | *True* if start and end points are within 350 m from each other, *False* otherwise
17 | geometry | MultiLineString Z geometry in GPS coordinates: (lat, lon, elevation)


## Cite

If you find this dataset or workflow useful for your research, please cite us!
```
@inproceedings{ilyankou2024ccgpx,
      author = {Ilyankou, Ilya and Wang, Meihui and Cavazzi, Stefano and Haworth, James},
      title = {CC-GPX: Extracting High-Quality Annotated Geospatial Data from Common Crawl},
      year = {2024},
      isbn = {9798400711077},
      publisher = {Association for Computing Machinery},
      address = {New York, NY, USA},
      url = {https://doi.org/10.1145/3678717.3691215},
      doi = {10.1145/3678717.3691215},
      booktitle = {Proceedings of the 32nd ACM International Conference on Advances in Geographic Information Systems},
      pages = {693–696},
      numpages = {4},
      keywords = {Common Crawl, GIS, GPS, GPX, hiking, user-generated routes},
      location = {Atlanta, GA, USA},
      series = {SIGSPATIAL '24}
}
```