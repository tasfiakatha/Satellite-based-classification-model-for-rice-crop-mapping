# Satellite-based model for rice crop mapping and monitoring

![vietnam-rice-field](https://vietnam.travel/sites/default/files/styles/top_banner/public/2021-02/Vietnam%20Rice%20terraces__0.jpg?itok=qjTCZxVa)

## Authors
[@tasfiakatha](https://github.com/tasfiakatha)

## Table of contents
- [Business problem statement](https://github.com/tasfiakatha/Satellite-based-classification-model-for-rice-crop-mapping/blob/main/README.md#business-problem-statement)
- [Data source](https://github.com/tasfiakatha/Satellite-based-classification-model-for-rice-crop-mapping/blob/main/README.md#data-source)
- [Methods](https://github.com/tasfiakatha/Satellite-based-classification-model-for-rice-crop-mapping/blob/main/README.md#methods)
- [Quick look at the results](https://github.com/tasfiakatha/Satellite-based-classification-model-for-rice-crop-mapping/blob/main/README.md#quick-look-at-the-results)
- [Value case summary](https://github.com/tasfiakatha/Satellite-based-classification-model-for-rice-crop-mapping/blob/main/README.md#value-case-summary)
- [Explore the notebook](https://github.com/tasfiakatha/Satellite-based-classification-model-for-rice-crop-mapping/blob/main/README.md#explore-the-notebook)
- [Repository structure](https://github.com/tasfiakatha/Satellite-based-classification-model-for-rice-crop-mapping/blob/main/README.md#repository-structure)
- [Contribution](https://github.com/tasfiakatha/Satellite-based-classification-model-for-rice-crop-mapping/blob/main/README.md#contribution)
- [License](https://github.com/tasfiakatha/Satellite-based-classification-model-for-rice-crop-mapping/blob/main/README.md#license)

## Business problem statement
Vietnam's rice industry, centered in the Mekong Delta, faces a critical juncture. While responsible for half the nation's rice production, 95% of exports, and a significant portion of agricultural GDP, the Delta is under siege by land degradation, rising sea levels, and climate change. These factors threaten not only Vietnam's food security for its growing population (outpacing rice production increases), but also its position as a major rice exporter. The Mekong Delta crisis jeopardize the food security of 89 million Vietnamese who rely on rice as a staple, especially in light of a 2% population growth rate that outstrips current development efforts. By 2030, Vietnam faces potential agricultural losses of up to 5.6%. Traditional planning methods for rice production and sales are inadequate. This project aims to leverage the power of predictive forecasting to address this challenge. By enabling data-driven decisions throughout the rice crop production and sale cycle, our project seeks to improve market planning and trade decisions in Vietnam, ensuring food security and navigating the complexities of climate change and population growth.

## Data source
- [Sentinel-1 Synthetic Aperture Radar (SAR) by European Commission (EC) and the European Space Agency (ESA)](https://planetarycomputer.microsoft.com/dataset/group/sentinel-1)
- [Landsat 8 and 9 Optical Data by NASA](https://landsat.gsfc.nasa.gov/)

## Methods
**Data Acquisition:**
Satellite Imagery
1. Optical Data: Utilize high-resolution optical data from NASA's Landsat-8 and 9 satellites to capture detailed information about land cover and vegetation health.
2. Radar Data: Leverage radar data from Sentinel-1 for its all-weather capability to penetrate cloud cover and provide valuable insights during monsoon seasons.

**Feature Extraction and Selection:**
1. Spectral Features: Extract relevant spectral information from the optical data, such as reflectance values across different wavelengths.
2. Textural Features: Analyze the spatial arrangement of pixels within the image to capture information about field size, crop uniformity and crop presence.
3. Temporal Features: Exploit the temporal dimension of the data by incorporating multi-temporal imagery spanning different growth stages of the rice crop.

**Enhancing Preprocessing Techniques:**

1. Vegetation Indices: Incorporate informative vegetation indices like NDVI, RVI, SAVI, LAI, and EVI derived from both optical and radar data to capture various aspects of crop health and growth.
2. Soil Moisture Indices: Utilize soil moisture indices to assess water availability, a crucial factor for rice production.
3. Extracting Radar Backscatter Values: Extract VV (vertical polarization) and VH (horizontal polarization) backscatter values from Sentinel-1 data to analyze vegetation structure and biomass.
4. Bounding Boxes: Create larger bounding boxes (e.g., 3x3 or 5x5 pixels) around each known rice field location to capture spatial context and improve data trend analysis.
5. Cloud Filtering: Implement a cloud filtering algorithm to remove obstructing clouds from optical data, ensuring a clearer view of the underlying land cover.
6. Data Scaling: Standardize the range of input features using techniques like Standard Scaler, Robust Scaler, or MinMax Scaler. This helps improve model convergence and training efficiency.

**Temporal Analysis:**

1. Cropping Cycles: Consider the three distinct rice cropping cycles in Vietnam (November-April, April-August, July-December) when analyzing the data.
2. Time Series Analysis: Explore different combinations of data timeframes, including 1-month, 2-month, 3-month, 4-month, 6-month, and yearly intervals to capture relevant temporal trends in rice growth.

**Clustering Optical Data:**

K-means Clustering: Apply K-means clustering to group similar optical data points together, potentially revealing distinct land cover types within the study area. This can further refine the model's understanding of the agricultural landscape.

**Model Development and Training:**

1. Geolocation Data: Utilize the 600 known rice field locations across Vietnam to create "ground truth" data for model training.
2. Algorithmic Exploration: Experiment with different machine learning algorithms and combinations, potentially including Random Forests, Extreme Gradient Boosting, and K-Nearest Neighbors models.
3. Permutations and Combinations: Train various models with different feature sets (spectral, textural, temporal) and combinations to identify the most effective approach.

**Validation and Testing:**

1. New Locations: Evaluate the performance of the trained models on rice fields in unseen locations to assess their generalizability.
2. Accuracy Assessment: Employ standard metrics like accuracy, F1 score or confusion matrix to quantify the accuracy of the model predictions.

## Quick look at the results
Data is available for Landsat-8 from April-2013 to now. Data is available for Landsat-9 from Feb-2022 to now. So, for the selected time window and missions there are typically views of our region every 8 days. But, due to scene overlaps, there are few more scenes within those 8-day increments. For this example over 5 months, there are 31 time slices that touch our region. Unfortunately, there are only 7 very clear scenes and several other partially cloudy scenes.

![scene array](https://github.com/tasfiakatha/Satellite-based-classification-model-for-rice-crop-mapping/blob/main/Assets/scene_array.png)

Closer look at scene 5 RGB (real color) images from the time series

![scene-5](https://github.com/tasfiakatha/Satellite-based-classification-model-for-rice-crop-mapping/blob/main/Assets/scene_5.png)

Receiver Operating Characteristic (ROC) curve for the base logistic regression model

![ROC curve](https://github.com/tasfiakatha/Satellite-based-classification-model-for-rice-crop-mapping/blob/main/Assets/ROC_logistic%20regression.png)

In-sample confusion matrix for k-nearest neighbors model

![in-sample KNN](https://github.com/tasfiakatha/Satellite-based-classification-model-for-rice-crop-mapping/blob/main/Assets/KNN_insample.png)

Out-sample confusion matrix for k-nearest neighbors model

![out-sample KNN](https://github.com/tasfiakatha/Satellite-based-classification-model-for-rice-crop-mapping/blob/main/Assets/KNN_outsample.png)

- The final model used for this project: K-nearest neighbors
- Metrics used:

| Metric    | Score |
|-----------|-------|
| Accuracy  | 77%   |
| Precision | 78%   |
| Recall    | 77%   |
| F1 Score  | 77%   |


## Value case summary
Our value case underscores the strategic integration of satellite data and advanced machine learning techniques across three crucial domains within the rice industry:

- **Precision Agriculture:** In this realm, we empower farmers with invaluable real-time insights and precise yield predictions. Through the fusion of satellite data and sophisticated machine learning algorithms, farmers are equipped to make informed decisions swiftly, thereby enhancing overall productivity and efficiency within their operations.

- **Agricultural Policy:** Leveraging the wealth of crop data gleaned from satellite
imagery, governments are empowered to craft evidence-based policies that foster sustainable farming practices. By delving into detailed analyses of crop health and environmental impacts, policymakers can ensure the long-term viability of rice- growing regions while promoting resilience and disaster preparedness.

- **Market Intelligence:** Our platform facilitates stakeholders' access to critical market trends and supply chain insights, enabling informed decision-making and heightened competitiveness. By harnessing satellite data analytics, businesses can forecast
market dynamics, optimize procurement strategies, and streamline supply chain operations, ultimately enhancing efficiency and driving growth in the rice industry.

- **Water Resource Management** allows stakeholders to optimize irrigation strategies, minimize water usage, and bolster environmental sustainability. By tailoring irrigation plans to crop distribution, we enhance water efficiency, reduce costs, and fortify resilience against climate fluctuations. Through this precision allocation, we mitigate ecological harm and ensure enduring water security for agricultural and environmental interests.

The integration of satellite data for predicting rice crop presence unlocks substantial opportunities for refining market planning and trade strategies as a business case. Targeting food distributors, retailers, commodity traders, and market analysts, this analysis delivers precise market trend predictions by forecasting rice crop presence and yield. By anticipating supply fluctuations, demand dynamics, and price trends, stakeholders can optimize procurement decisions, boost competitiveness, and capitalize on emerging opportunities. To effectively market and publicize this analysis, tailored outreach campaigns, thought leadership content, strategic collaborations, and success stories will be employed. Funding for the project will be pursued through strategic partnerships, venture capital investment, and government grants, aiming to advance market transparency, efficiency, and sustainability.

To enhance outcomes, we propose strategic measures: expanding training data, exploring diverse bounding box configurations, adopting ensemble learning, and optimizing machine learning algorithms and feature selection. These steps aim to drive innovation, efficiency, and sustainability in the rice industry, benefiting stakeholders at all levels.

## Explore the notebook
Explore the notebook file [here](https://nbviewer.org/github/tasfiakatha/Satellite-based-classification-model-for-rice-crop-mapping/blob/main/Satellite-based%20model%20for%20rice%20crop%20mapping%20and%20monitoring.ipynb)

## Repository structure

![image](https://github.com/tasfiakatha/Satellite-based-classification-model-for-rice-crop-mapping/assets/120822849/06c3ede7-1c4d-4a9a-9a0a-83fcd9b1f57f)


## Contribution
Pull requests are welcome! For major changes, please open an issue first to discuss what you would like to change or contribute.

## License
MIT License

Copyright (c) 2024 Tasfia Katha

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

Learn more about [MIT](https://choosealicense.com/licenses/mit/) license
