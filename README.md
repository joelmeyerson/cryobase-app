# CryoBase

CryoBase is an application to manage cryo-EM data in the cloud with Amazon Web Service (AWS) Simple Storage Solution (S3). The goal is to provide a convenient way to access low-cost cloud storage to store cryo-EM datasets. The application has an interface for entering metadata for a cryo-EM dataset and uploading the dataset to S3. It supports the `STANDARD` storage class, and the `DEEP_ARCHIVE` storage class which is priced at about $1/TB as of 2/2021. There is also an interface for browsing and downloading datasets stored on S3. CryoBase is designed to interact with the user's own AWS account so the user has complete control over the data and can access it even without CryoBase. 

Downloads for macOS and Linux are found under Releases.

This work is licensed under Attribution-NoDerivatives 4.0 International (CC BY-ND 4.0). To view a copy of this license, visit https://creativecommons.org/licenses/by-nd/4.0/.

## Questions and Feedback
Questions or problems can be posted on the Discussions page. Feedback and feature requests can also be posted there and are greatly appreciated as a way to improve the application.

## How to use CryoBase
### Step 1. Creating an AWS account
1. Go to the Amazon AWS Management Console website and click `Create an AWS Account`.
2. After creating the account, click on your username in the top menu bar of the AWS Management Console website and select `My Security Credentials`.
3. Under the `Access keys (access key ID and secret access key)` section, click `Create New Access Key`. This produces produces an `AWS Access Key` and `AWS Secret Key`. You will use these keys later to configure CryoBase.

### Step 2. Creating an AWS storage bucket
1. Within the AWS Management Console page navigate to the S3 section (found under the Storage service category).
2. Here you will create a bucket, which is conceptually like a directory. Click `Create bucket`. Enter a bucket name (for example, `cryo-em-data`). Select the nearest AWS Region. Customize the bucket settings as desired and click `Create bucket` at the bottom of the page.

### Step 3. Configuring CryoBase
1. Open CryoBase and register an account or login to your account.
2. Click `Settings` (the gear icon). Enter a bucket name, AWS Access Key, and AWS Secret Key.
3. CryoBase will notify you if your AWS configuration details are valid. If you have already uploaded data to the target bucket using CryoBase then the `Data Archive` section will automatically populate to show the available datasets.

### Step 4. Uploading data
1. Click `Upload Data` (the cloud icon). Enter the details for the cryo-EM dataset to be uploaded.
2. Select the desired storage class (`STANDARD` or `DEEP_ARCHIVE`). The details and costs of these classes is provided on the AWS S3 website. Essentially `STANDARD` is higher cost but can be downloaded on-demand, while `DEEP_ARCHIVE` is low-cost but requires a 12-48 hour retrieval step before data can be downloaded.
3. Click `Start Upload`. While the upload is in progress you can freely switch to the `Data Archive` section to confirm that a new dataset entry is visible in the table.

## Step 5. Downloading data
