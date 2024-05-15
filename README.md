# Pseudo-Anonymised ID Generation

This interface enables the use of the SHA-1 hashing algorithm on CSV files for the generation of pseudo-anonymised IDs, currently used for the AIMBraTS project. The application operates entirely client-side, ensuring that no data is transmitted outside of the local machine. To begin, simply go to: [Pseudo-Anonymised ID Generator](https://cai4cai.ml/sha1inbrowser/)

## Motivation

For the entirety of the AIMBraTS project, we aim to have a pseudo-anonymised ID, that is unique to each person, but also allows us to cross reference this ID with the original patient information, if required. 

The way we have decided to do this is by using a hashing algorithm, specifically SHA-1, to hash the NHS number. This hashed value is then truncated to only include the first 10 values of the generated hash, for readability.

The key advantage of this approach to generating pseudo-anonymised IDs is that with the ID, it is impossible to recreate the original input, and sensitive, data. But if someone has access to the original data, then they can use that to cross reference which patient has which pseudo-anonymised ID, thus providing a failsafe. 

## How to Use the Application

### Step 0: Preliminary Data Check
Ensure each NHS number in your dataset is 10 digits long without any spaces. Errors in this data will lead to incorrect hashing.

### Step 1: Access the Application
Navigate to the [Pseudo-Anonymised ID Generator](https://cai4cai.ml/sha1inbrowser/).

> **Note:** This HTML application, which is accessed and viewed via a web browser, runs locally on your own machine, and no data is transmitted outside of the local machine, when used. 

### Step 2: Load Your Spreadsheet
The application currently supports `.csv` files only. Make sure your data is saved in this format before proceeding. Select your file by clicking on `Choose File`.

### Step 3: Configure Data Columns
Assign roles to each column in your dataset, specifying which should be hashed, excluded, or kept. Specifically, assign the NHS number column to `Hash and Exclude` and all identifiable information to `Exclude`. Relevant clinical information, but not patient identifiable, can be assigned to `Keep`. Any junk that you do not want, in the anonymised spreadsheet, can be set to `Exclude`. Columns that you want a hashed version of, but you also want to appear in the anonymised spreadsheet can be set to `Hash`

### Step 4: Process the Data
Click `Process` to start the local hashing. This generates two `.csv` files:
- **original_with_hash.csv**: Contains all original data along with the generated hashes.
- **unidentifiable.csv**: Contains only non-identifiable data and hashes.

### Data Handling
- **Internal Use**: Keep `original_with_hash.csv` within the NHS trust.
- **External Sharing**: `unidentifiable.csv` is the anonymised spreadsheet and can be shared with researchers at KCL, following approved ethics and data sharing agreements.

## Support and Contact
For any inquiries or support requests, please contact:
- Theodore Barfoot at [theodore.d.barfoot@kcl.ac.uk](mailto:theodore.d.barfoot@kcl.ac.uk)
- OR: [theodore.barfoot1@nhs.net](mailto:theodore.barfoot1@nhs.net)


### Example Python Implementation

This operation performed by this application is equivalent to the following:

```python
def hash_algo(nhs_number):
    return hashlib.sha1(nhs_number.encode()).hexdigest()[:10]
```
