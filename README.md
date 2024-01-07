# crop_classification

CROP DETECTION USING RANDOM FOREST CLASSIFIER


1. INTRODUCTION
Crop detection involves the process of identifying and categorizing different types of crops or vegetation in a given area using remote sensing and data analysis techniques. This analysis helps in monitoring crop health, yield estimation, land use assessment, and other agricultural decisions. Remotely sensed data through optical and microwave imaging systems are generally used in this analysis. Typically, the nature of image data and acquired ground truth data affects the quality of the work.

2. PROBLEM STATEMENT
To identify crop types using satellite imagery with the provided ground truth data.

3. STUDY AREA
The area of interest (AOI) is located near Kashkadarya in Uzbekistan. The AOI is about 20.65 km2. The landforms in the AOI are fallow, barren, built-up, and several croplands. The crops grown are cotton (summer), wheat (winter), alfalfa (permanent), and orchard (permanent). 

4. METHODOLOGY
The process consists of 
Data Sourcing
Data Preparation
Model Training & Testing
4.1. DATA COLLECTION:
The crop type data is acquired from the CAWa project in the Central Asia region. The dataset consists of 8435 crop samples in total. Hence, the data undergoes several filtering steps, starting with the selection of the area of interest (AOI) and the corresponding year of acquisition, which in this case is 2018. Subsequently, I narrowed down the data to focus exclusively on summer crops cultivated in the AOI. Additionally, we account for the presence of permanent crops within the AOI. Furthermore, a specialized class for barren and built-up areas is established through manual annotation using Sentinel-2 imagery as a reference. Thus, the AOI encompasses cotton, alfalfa, and orchard crops, as well as fallow and built-up barren lands as shown in Figure 1. The number of features in each class is provided in Table 1.

Figure 1. The ground truth data overlaid on Sentinel-2 satellite imagery

Table 1. Available Crop Classes in the AOI
Crop Type
Available Polygons
Fallow
3
Cotton
28
Alfalfa
2
Orchard
1
Built-up & Barren
5


The satellite imagery considered in classifying the crop data is Sentinel-2 Surface Reflectance (SR) data product freely available in the Earth Engine cloud data. Table 2 provides the specifications of the satellite imagery used. The crop identification analysis considers time-series data hence, SR data products are used as the reflectance doesn’t vary w.r.t the temporal atmospheric effects. The bands considered are Blue, Green, Red, Red Edge 1, Red Edge 2, Red Edge 3, NIR, SWIR 1, and SWIR 2. The data is filtered to the date range in August of 2018 and clipped to the AOI. Additionally, the data is filtered to less than 5% cloud cover and selected as the first least cloud cover imagery.

Table 2. Specifications of Raster Dataset
Category
Description
Satellite Image
Sentinel-2 Level-2A SR
Bands
Blue, Green, Red, Red Edge 1, Red Edge 2, Red Edge 3, NIR, SWIR 1, and SWIR 2
Date
August 2018
Area
20.65km2
Resolution
10m


4.2. CLASSIFICATION MODEL:
The model training and testing phase involves the following steps:
Classifier: The Random Forest (RF) classifier known to be the best of the supervised classification algorithm is applied to classify the crops.
Sample dataset: Combines the features (Fallow, Cotton, Alfalfa, Orchard, and Built-up and barren) into a feature collection.
Train-test split: The data was split into 30% test and the remaining training samples.
Accuracy: A confusion matrix is formed from the test data and the accuracy of the model is calculated.

5. RESULTS AND DISCUSSION
5.1. CROP CLASSIFICATION:
The Random forest algorithm achieved an accuracy of 82.8% in the classification task. The confusion matrix in Table 3 provides a detailed breakdown of the algorithm’s performance on the test data. 
The "Cotton" class exhibits a higher True Positive count, suggesting the model's proficiency in correctly identifying instances of this class. In contrast, "Alfalfa" and "Orchard" show lower True Positive values, possibly due to challenges in the model's ability to distinguish between these classes or discrepancies between the ground truth data and the satellite data used for classification.
Table 3. Confusion Matrix of the Model


Fallow
Cotton
Alfalafa
Orchard
Builtup & Barren
Fallow
8
809
3
0
61
Cotton
47
4850
90
1
18
Alfalafa
0
128
0
0
0
Orchard
0
0
0
0
0
Builtup & Barren
0
21
0
5
871


The classified satellite image providing the crop map of the AOI is shown in Figure 2.

Figure 2. Crop Map of Study Area


5.2. TIME-SERIES ANALYSIS:
Time series analysis by NDVI (Normalized Difference Vegetation Index) is carried out to know the presence of vegetation cover in the crop period (April-December 2018) considered. The NDVI is built with NIR and Red band of Sentinel-2 SR imagery. 
The fallow region has an NDVI range of 0.09 to 0.2 indicating the presence of grass or stem projections of harvested crops.

Cotton’s NDVI value ranges from 0 to 0.52 indicating the presence of green vegetation from June 2018 to January 2019.




Alfalfa has an NDVI value of 0 to 0.4 indicating green vegetation in the crop parcel. The crop shows an increase in NDVI from April to October 2018 and falls till January 2019.

Orchard has irregular NDVI value in the crop period considered.









Barren shows the lowest NDVI values till the end of the crop period indicating no vegetation or crop growth.


6. CONCLUSION
The crop map and time series analysis came in accordance with the ground truth data. The crop map has been successively mapped using random forest classifier in Google Earth Engine API. 


*** End***
