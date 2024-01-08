# CROP DETECTION USING RANDOM FOREST CLASSIFIER  

# Introduction
Crop detection involves the process of identifying and categorizing different types of crops or vegetation in a given area using remote sensing and data analysis techniques. This analysis helps in monitoring crop health, yield estimation, land use assessment, and other agricultural decisions. Remotely sensed data through optical and microwave imaging systems are generally used in this analysis. Typically, the nature of image data and acquired ground truth data affects the quality of the work.

# Problem Statement
To identify crop types using satellite imagery with the provided ground truth data.

# Study Area
The area of interest (AOI) is located near Kashkadarya in Uzbekistan. The AOI is about 20.65 km2. The landforms in the AOI are fallow, barren, built-up, and several croplands. The crops grown are cotton (summer), wheat (winter), alfalfa (permanent), and orchard (permanent). 

# Methodology
The process consists of 
- Data Sourcing
- Data Preparation
- Model Training & Testing
## Data Collection:
The crop type data is acquired from the CAWa project in the Central Asia region. The dataset consists of 8435 crop samples in total. Hence, the data undergoes several filtering steps, starting with the selection of the area of interest (AOI) and the corresponding year of acquisition, which in this case is 2018. Subsequently, I narrowed down the data to focus exclusively on summer crops cultivated in the AOI. Additionally, we account for the presence of permanent crops within the AOI. Furthermore, a specialized class for barren and built-up areas is established through manual annotation using Sentinel-2 imagery as a reference. Thus, the AOI encompasses cotton, alfalfa, and orchard crops, as well as fallow and built-up barren lands as shown in Figure 1. The number of features in each class is provided in Table 1.
<div align="center">
<img width="500" src= "https://github.com/aishwarya-10/crop_classification/assets/48954230/f82364da-72e3-4b7c-9de5-891b43a5c42d">
  
<p> Figure 1. The ground truth data overlaid on Sentinel-2 satellite imagery </p>
</div>

<div align="center">
<p> Table 1. Available Crop Classes in the AOI </p>

<img width="600" src= "https://github.com/aishwarya-10/crop_classification/assets/48954230/e2ed5359-b971-41f3-8aff-b3cfc10d0db6">
</div>

The satellite imagery considered in classifying the crop data is Sentinel-2 Surface Reflectance (SR) data product freely available in the Earth Engine cloud data. Table 2 provides the specifications of the satellite imagery used. The crop identification analysis considers time-series data hence, SR data products are used as the reflectance doesn’t vary w.r.t the temporal atmospheric effects. The bands considered are Blue, Green, Red, Red Edge 1, Red Edge 2, Red Edge 3, NIR, SWIR 1, and SWIR 2. The data is filtered to the date range in August of 2018 and clipped to the AOI. Additionally, the data is filtered to less than 5% cloud cover and selected as the first least cloud cover imagery.

<div align="center">
<p> Table 2. Specifications of Raster Dataset </p>
<img width="600" src="https://github.com/aishwarya-10/crop_classification/assets/48954230/cd6a5779-bcd4-40cb-aa4d-5a315ba6eaba">
</div>

## Classification Model:
The model training and testing phase involves the following steps:<br/>
**Classifier:** The Random Forest (RF) classifier known to be the best of the supervised classification algorithm is applied to classify the crops.<br/>
**Sample dataset:** Combines the features (Fallow, Cotton, Alfalfa, Orchard, and Built-up and barren) into a feature collection.<br/>
**Train-test split:** The data was split into 30% test and the remaining training samples.<br/>
**Accuracy:** A confusion matrix is formed from the test data and the accuracy of the model is calculated.

# Results and Discussions
## Crop Classification:
The Random forest algorithm achieved an accuracy of 82.8% in the classification task. The confusion matrix in Table 3 provides a detailed breakdown of the algorithm’s performance on the test data. 
The "Cotton" class exhibits a higher True Positive count, suggesting the model's proficiency in correctly identifying instances of this class. In contrast, "Alfalfa" and "Orchard" show lower True Positive values, possibly due to challenges in the model's ability to distinguish between these classes or discrepancies between the ground truth data and the satellite data used for classification.

<div align="center">
<p> Table 3. Confusion Matrix of the Model </p>
<img width="500" src="https://github.com/aishwarya-10/crop_classification/assets/48954230/1240307d-5184-4a95-946a-3e2fa5c8a28e">
</div>

The classified satellite image providing the crop map of the AOI is shown in Figure 2.

<div align="center">
<img width="500" src="https://github.com/aishwarya-10/crop_classification/assets/48954230/1e580ef0-95ab-42ff-9034-eb6d82ce037a">
<p> Figure 2. Crop Map of Study Area </p>
</div>

## Time Series Analysis:
Time series analysis by NDVI (Normalized Difference Vegetation Index) is carried out to know the presence of vegetation cover in the crop period (April-December 2018) considered. The NDVI is built with NIR and Red band of Sentinel-2 SR imagery. 
- The fallow region has an NDVI range of 0.09 to 0.2 indicating the presence of grass or stem projections of harvested crops.

<div align="center">
<img src="https://github.com/aishwarya-10/crop_classification/assets/48954230/f28d0443-969b-4943-b119-6ad8b2cecd55">
</div>

- Cotton’s NDVI value ranges from 0 to 0.52 indicating the presence of green vegetation from June 2018 to January 2019.
<div align="center">
<img src="https://github.com/aishwarya-10/crop_classification/assets/48954230/5951b486-c67c-4190-8102-42307cd5899d">
</div>

- Alfalfa has an NDVI value of 0 to 0.4 indicating green vegetation in the crop parcel. The crop shows an increase in NDVI from April to October 2018 and falls till January 2019.
<div align="center">
<img src="https://github.com/aishwarya-10/crop_classification/assets/48954230/3e24fe52-c595-47bb-8005-58dad1a1b5ac">
</div>

- Orchard has irregular NDVI values in the crop period considered.
<div align="center">
<img src="https://github.com/aishwarya-10/crop_classification/assets/48954230/df66e1b1-9be4-49a0-9573-7bec8f067af1">
</div>

- Barren shows the lowest NDVI values till the end of the crop period indicating no vegetation or crop growth.
<div align="center">
<img src="https://github.com/aishwarya-10/crop_classification/assets/48954230/0f69ffcc-e286-4a0e-9f54-965072fc9ddb">
</div>

# Conclusion
The crop map and time series analysis came by the ground truth data. The crop map has been successively mapped using a random forest classifier in Google Earth Engine API. 

<div align="center"> <b> **** End **** </b> </div>

