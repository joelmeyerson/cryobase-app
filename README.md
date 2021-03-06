# CryoBase

CryoBase is a graphical application to store and manage cryo-EM data using Amazon Web Services (AWS) Simple Storage Solution (S3). The goal is to provide a convenient way to store cryo-EM data using low-cost cloud storage. The application has an interface for entering metadata for a cryo-EM dataset and uploading the dataset to S3. It supports the AWS S3 `STANDARD` storage class, and the `DEEP_ARCHIVE` storage class which is priced at about $1/TB/month. There is also an interface for browsing and downloading datasets stored on S3. CryoBase is designed to interact with the user's own AWS account so the user has complete control over the data even without CryoBase. 

Builds for macOS and Linux can be downloaded in Releases.

CryoBase is made with React and Electron frameworks.

This work is licensed under Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0). To view a copy of this license, visit https://creativecommons.org/licenses/by-nc-nd/4.0/.

## Questions and Feedback
Questions can be posted on the Discussions page or emailed to jrmeyerson@gmail.com. Feedback and feature requests are also greatly appreciated as a way to improve the application.

## How to use CryoBase
NOTE: Before using AWS S3 or CryoBase please familiarize yourself with the data storage and retrieval costs of AWS S3 `STANDARD` and `DEEP_ARCHIVE`.

### Step 1. Creating an AWS account
1. Go to the AWS Management Console website and click `Create an AWS Account`.
2. After creating the account, click on your username in the top menu bar of the AWS Management Console website and select `My Security Credentials`.
3. Under the `Access keys (access key ID and secret access key)` section, click `Create New Access Key`. This generates an `AWS Access Key` and `AWS Secret Key`. You will use these keys later to configure CryoBase.

### Step 2. Creating an AWS storage bucket
1. Within the AWS Management Console page navigate to the S3 section (found under the Storage service category).
2. Here you will create a bucket, which is conceptually like a directory to store your data. Click `Create bucket`. Enter a bucket name (for example, *cryo-em-data*). Select the nearest AWS Region from the dropdown menu. Customize the bucket settings as desired and click `Create bucket` at the bottom of the page.

### Step 3. Configuring CryoBase
1. Open CryoBase and register an account or login to your account.
2. Click `Settings` (the gear icon). Enter the bucket name, AWS Access Key, and AWS Secret Key.
3. CryoBase will notify you if your AWS configuration details are valid. If you have already uploaded data to the target bucket using CryoBase then the `Data Archive` section will automatically populate to show the available datasets.

![alt text](https://github.com/joelmeyerson/cryobase-app/blob/main/settings.png?raw=true)

### Step 4. Uploading data
1. Click `Upload Data` (the cloud icon). Enter the details for the cryo-EM dataset to be uploaded.
2. Select the desired storage class (`STANDARD` or `DEEP_ARCHIVE`). The details and costs of these classes is provided on the AWS S3 website. Essentially `STANDARD` is higher cost but can be downloaded on-demand, while `DEEP_ARCHIVE` is low-cost but requires a 12-48 hour retrieval step before data can be downloaded.
3. Click `Start Upload`. While the upload is in progress you can freely switch to the `Data Archive` section to see the new dataset entry in the table.

![alt text](https://github.com/joelmeyerson/cryobase-app/blob/main/upload.png?raw=true)

### Step 5. Downloading data
Data stored in the `STANDARD` storage class
1. Click `Data Archive` and select a dataset from the table.
2. Choose a local download path.
3. Click `Start Download`.

Data stored in the `DEEP_ARCHIVE` storage class
1. Click `Data Archive` and select a dataset from the table.
2. There are different `Data Status` categories relevant to interacting with data stored in the `DEEP_ARCHIVE` storage class.
* `Archived` means a data retrieval process must be initiated to make it available for download. Click the `Archived` button and wait until a notification confirms the data is being restored. Depending on the number of files in the dataset it may take a few minutes for this process to complete and the notification to display.
* `Restoring` means that AWS has marked the data to be restored. Clicking the `Restoring` button will check the status of the restoration process. Once the data is restored, clicking this button will confirm the restoration and the button status will change to `Restored`.
* `Restored` means the data has been retrieved and is available for download. After selecting the table row, choose a local download path and click `Start Download`. Clicking the `Restored` button will display a notification with the estimate for when the data will return to `Archived` status (3 days from the time data retrieval has completed).
* `Archiving` means the recovered data has partially expired and is being returned to `Archived` status. Once the data has completely returned to `Archived` status it will again be available for retrieval.

![alt text](https://github.com/joelmeyerson/cryobase-app/blob/main/download.png?raw=true)

## Other topics

### How to delete data
As a precaution CryoBase was designed without an interface for deleting data. However, data can easily be deleted from the AWS S3 web console.
1. Navigate to the S3 section of the AWS console.
2. Locate the bucket used by CryoBase (e.g. *cryo-em-data*). Within this bucket select the dataset you want to delete, and click `Delete`. AWS will go through a quick confirmation step to verify you actually want to delete the data.
3. In addition, you should delete the associated metadata for the target dataset. This will ensure that CryoBase no longer displays the dataset as an entry in the Archive table. The metadata can be found in your bucket within the metadata path (e.g. *cryo-em-data/metadata*). Select the metadata for the target dataset and click `Delete`.
