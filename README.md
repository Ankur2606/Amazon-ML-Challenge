### Problem Statement: Feature Extraction from Images

#### Overview:
The goal of this hackathon is to develop a machine learning model capable of extracting entity values from images. This task is crucial in domains such as healthcare, e-commerce, and content moderation, where accurate product information is essential. As digital marketplaces grow, some products lack detailed textual descriptions, making it necessary to derive key details directly from images. These details include information like weight, volume, voltage, wattage, dimensions, and more, which are critical for digital stores.

#### Data Description:
The dataset consists of the following columns:
1. **index**: A unique identifier (ID) for each data sample.
2. **image_link**: A public URL where the product image is available for download.  
   Example: `https://m.media-amazon.com/images/1/71XfHPR36-L.jpg`.  
   To download images, use the `download_images` function from `src/utils.py`. Refer to the sample code in `src/test.ipynb`.
3. **group_id**: Category code of the product.
4. **entity_name**: Product entity name (e.g., "item_weight").
5. **entity_value**: Product entity value (e.g., "34 gram").  

   **Note**: In `test.csv`, the column `entity_value` will not be present, as it is the target variable.

#### Output Format:
The output file must be a CSV with the following two columns:
1. **index**: The unique identifier (ID) of the data sample. It must match the test record index.
2. **prediction**: A string formatted as `"x unit"`, where `x` is a float number in standard formatting, and `unit` is one of the allowed units (the list of allowed units is provided in the Appendix). Ensure there is a space between `x` and the `unit`.

   **Valid examples**:
   - `"2 gram"`
   - `"12.5 centimetre"`
   - `"2.56 ounce"`

   **Invalid examples**:
   - `"2 gms"`
   - `"60 ounce/1.7 kilogram"`
   - `"2.2e2 kilogram"`

**Important**:
- You must provide predictions for all indices. If no value is found in the image for a test sample, return an empty string `""`.
- The number of output samples must match the number of records in `test.csv`. If there are fewer or more output samples, your submission will not be evaluated.

#### File Descriptions:
1. **Source Files**:
   - `src/sanity.py`: Sanity checker to ensure that the final output file passes all formatting checks.
   - `src/utils.py`: Helper functions for downloading images from the `image_link`.
   - `src/constants.py`: Contains the allowed units for each entity type.
   - `sample_code.py`: Sample dummy code to generate an output file in the correct format (optional usage).

2. **Dataset Files**:
   - `dataset/train.csv`: Training file with labels (`entity_value`).
   - `dataset/test.csv`: Test file without labels (`entity_value`). Use this file to generate predictions.
   - `dataset/sample_test.csv`: Sample test input file.
   - `dataset/sample_test_out.csv`: Sample output for `sample_test.csv`. Format your predictions for `test.csv` in the same way.

#### Constraints:
1. The sample output file and sanity checker (`sanity.py`) are provided. Ensure your output file passes through the sanity checker.
   - The sanity checker will not validate if the number of predictions is fewer or greater than the test file.
   - Successful parsing will display: `Parsing successful for file: ...csv`.
2. Only the allowed units from `constants.py` (or the Appendix) must be used. Predictions with other units will be considered invalid.

#### Evaluation Criteria:
Submissions will be evaluated based on the **F1 Score**, a standard metric for classification and extraction problems.

**Classification Logic**:
1. **True Positives (TP)**: If `OUT != ""` and `GT != ""` and `OUT == GT`.
2. **False Positives (FP)**: 
   - Case 1: If `OUT != ""` and `GT != ""` and `OUT != GT`.
   - Case 2: If `OUT != ""` and `GT == ""`.
3. **False Negatives (FN)**: If `OUT == ""` and `GT != ""`.
4. **True Negatives (TN)**: If `OUT == ""` and `GT == ""`.

**F1 Score Formula**:
\[
F1\ Score = \frac{2 \times \text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}
\]
Where:
- **Precision**: \( \frac{True\ Positives}{True\ Positives + False\ Positives} \)
- **Recall**: \( \frac{True\ Positives}{True\ Positives + False\ Negatives} \)

#### Submission:
Submit a `test_out.csv` file with the exact same format as `sample_test_out.csv`. Ensure that it passes the sanity checker before submission.

--- 
**Good Luck!**
