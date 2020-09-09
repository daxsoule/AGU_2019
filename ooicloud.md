OOICloud Overview

1-paragraph description of what the data is with links out to appropriate deeper descriptions, description of the file structure, a preferred image, and a contact point), and either send back by email or – slightly preferred – publish in the camhd repo somewhere?  Please credit whoever is appropriate (any combination of your own institutions, OOI, OOICloud, Pangeo, etc., at the top

The [OOICloud Project](https://github.com/ooicloud) is working to make data from the Ocean Observatories Initiative ([OOI](https://oceanobservatories.org)) publically available in the cloud and accessible through a [Pangeo](http://pangeo.io/) interface. A primary goal is to provide these data to the scientific community using a cloud-performant object storage model, and to provide large-scale remote compute capabilities for research investigations. The OOI comprises 89 scientific platforms with approximately 830 instruments, and provides nearly 5 TB of data each month for the study of the ocean-atmosphere system from the continental margins to the mid-ocean ridges. A core component of OOI is the [Regional Cabled Array](https://oceanobservatories.org/regional-cabled-array/) which uses a seafloor fiber-optic cable to connect and power the largest array of seafloor oceanographic instruments in the world, delivering data in real-time to shore. 

[CamHD](https://oceanobservatories.org/instrument-class/camhd/) is a high-definition video camera connected to the OOI's fiber optic cable ate Axial Seamount which is ideal for a wide range of oceanographic, biological and geophysical investigations. This Jupyter notebook shows how to load video data from the OOI Seafloor Camera system deployed at Axial Volcano on the Juan de Fuca Ridge. It demonstrates the basic usage of the pycamhd library, which can be used to extract frames from the ProRes encoded Quicktime files. These data are hosted on Microsoft's [AIforEarth Open Datasets](https://azure.microsoft.com/en-us/services/open-datasets/).


#### Storage resources 

All available video files are listed in a [JSON](https://ooiopendata.blob.core.windows.net/camhd/dbcamhd.json) that has useful information such as the Unix timestamp (seconds) of the first frame in each video, and the total number of frames in each video.  Data are stored in blobs [blob](https://ooiopendata.blob.core.windows.net) format in the East US data center, in the following blob container:

`https://ooiopendata.blob.core.windows.net`

Within that container, data are named as:

`[product]/[year]/[month]/[day]/[filename]`

* <i>product</i> is a product name; this should always be "rainfall"
* <i>year</i> is a four-digit year
* <i>month</i> is a two-digit month-of-year code, starting with 01
* <i>day</i> is a two-digit day-of-month code, starting with 01
* <i>filename</i> encodes the product, date, and time, with the last four digits encoding 24-hour time on 15-minute boundaries

For example, this filename:

`https://ghe.blob.core.windows.net/noaa-ghe/rain_rate/2020/04/02/NPR.GEO.GHE.v1.S202004020030.nc.gz`

...contains the 15-minute rainfall estimate for April 2, 2020, at 00:30 UTC.

Latitude and longitude are not perfectly uniformly sampled, so an additional file is available to specify the precise lat/lon grid associated with all GHE files (~160MB):

<https://ghe.blob.core.windows.net/noaa-ghe/NPR.GEO.GHE.v1.Navigation.netcdf.gz>

A complete Python example of accessing and plotting a GHE image (i.e., an instantaneous global estimate) is available in the notebook provided under &ldquo;<a href="https://azure.microsoft.com/en-us/services/open-datasets/catalog/ghe?tab=data-access">data access</a>&rdquo;.

We also provide a read-only SAS (shared access signature) token to allow access to GHE data via, e.g., BlobFuse, which allows you to mount blob containers as drives:

`st=2020-04-14T00%3A09%3A17Z&se=2034-04-15T00%3A09%3A00Z&sp=rl&sv=2018-03-28&sr=c&sig=%2F1X7FhDPqwF9TYzXVvB8D%2BX%2F%2B3OYbDdMkXpKU37T6eI%3D`

Mounting instructions for Linux are [here](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-how-to-mount-container-linux).

Large-scale processing using this dataset is best performed in the East US Azure data center, where the data is stored.  If you are using GHE data for environmental science applications, consider applying for an [AI for Earth grant](http://aka.ms/ai4egrants) to support your compute requirements.


#### Pretty picture

<img src="https://ai4edatasetspublicassets.blob.core.windows.net/assets/aod_images/ghe.png" width=350px;><br/>

<p style="font-size:80%;margin-left:15px;">Global daily precipitation on April 9, 2020.</p>


#### Contact

For questions about this dataset, contact [`aiforearthdatasets@microsoft.com`](mailto:aiforearthdatasets@microsoft.com?subject=ghe%20question).


#### Notices

MICROSOFT PROVIDES AZURE OPEN DATASETS ON AN "AS IS" BASIS. MICROSOFT MAKES NO WARRANTIES, EXPRESS OR IMPLIED, GUARANTEES OR CONDITIONS WITH RESPECT TO YOUR USE OF THE DATASETS. TO THE EXTENT PERMITTED UNDER YOUR LOCAL LAW, MICROSOFT DISCLAIMS ALL LIABILITY FOR ANY DAMAGES OR LOSSES, INCLUDING DIRECT, CONSEQUENTIAL, SPECIAL, INDIRECT, INCIDENTAL OR PUNITIVE, RESULTING FROM YOUR USE OF THE DATASETS. 

This dataset is provided under the original terms that Microsoft received source data. The dataset may include data sourced from Microsoft.
