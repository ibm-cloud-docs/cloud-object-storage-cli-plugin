---

copyright:
  years: 2017, 2018, 2019
lastupdated: "22-01-2019"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}

# Use the IBM Cloud CLI
{: #ic-use-the-ibm-cli}

The Cloud Object Storage plugin for command-line interface (CLI) provides extra capabilities for working with IBM� Cloud Object Storage. You can use the Cloud Object Storage plugin for CLI to manage and maintain buckets and objects within IBM� Cloud Object Storage.

The Cloud Object Storage plugin for command-line interface (CLI) is compatible with Windows, Linux, MacOS V10 and must be a 64-bit machine.

The initial version of a {{site.data.keyword.cos_short}} plugin [{{site.data.keyword.cloud}} Platform CLI](https://clis.ng.bluemix.net/ui/home.html) is available for anyone interested in trying it out. If you have any comments or suggestions on the CLI plugin, click on the "Feedback" button on this page and select the relevant section of the documentation.
{:note}

## Installation and configuration
{: #ic-installation}

Install the plugin using the `plugin install` command.

```
ibmcloud plugin install cloud-object-storage
```

Configure the plugin with `ibmcloud cos config`.  This will populate your credentials or repopulate them if your config file has reset. 


The program also offers the ability for you to set the default local directory for downloaded files, and to set a default region. To set the default download location, type `ibmcloud cos config ddl` and input into the program a valid file path. To set a default region, type `ibmcloud cos config region` and provide a input into the program a region code, such as `us-south`. By default, this value is set to `us-geo`.


### HMAC Credentials
{: #ic-hmac-credentials}

If preferred, HMAC credentials associated with a Service ID can be used to connect to object storage in lieu of the user API key used to authenticate to the CLI itself. To generate HMAC credentials, you can add the `{"HMAC":true}` parameter when generating a [service credential](/docs/services/cloud-object-storage/hmac/credentials.html). Then you can run `ibmcloud cos config hmac` to input your HMAC credentials into the program (please note that you must switch priority to HMAC credentials using `ibmcloud cos config auth` after inputing HMAC credentials). If you choose to use IAM authentication (the standard IBM way to authenticate), you do not need to provide any credentials � the program will authenticate you automatically.

At any time, to switch between HMAC and IAM authentication, you can type `ibmcloud cos config auth`. For more information on IAM-based authentication, click [here](https://console.bluemix.net/docs/iam/quickstart.html#getstarted).

## Command index
{: #ic-command-index}

| Commands |  |  |
| --- | --- | --- |
| [abort-multipart-upload](#abort-a-multipart-upload) | [complete-multipart-upload](#complete-a-multipart-upload) | [config](#configure-the-program) |
| [copy-object](#copy-object-from-bucket) | [create-bucket](#create-a-new-bucket) | [create-multipart-upload](#create-a-new-multipart-upload) |
| [delete-bucket](#delete-an-existing-bucket) | [delete-bucket-cors](#delete-bucket-cors) | [delete-object](#delete-an-object) |
| [delete-objects](#delete-multiple-objects) | [get-bucket-class](#get-a-buckets-class) | [get-bucket-cors](#get-bucket-cors) |
| [get-bucket-location](#find-a-bucket) | [get-object](#download-an-object) | [head-bucket](#get-a-buckets-headers) |
| [head-object](#get-an-objects-headers) | [list-buckets](#list-all-buckets) | [list-multipart-uploads](#list-in-progress-multipart-uploads) |
| [list-objects](#list-objects) | [list-parts](#list-parts) | [put-bucket-cors](#set-bucket-cors) |
| [put-object](#upload-an-object) | [upload-part](#upload-a-part) | [upload-part-copy](#upload-a-part-copy) |
| [wait](#wait) |  |  |

Each operation listed below has an explanation of what it does, how to use it, and any optional or required parameters. Unless specified as optional, any listed parameters are mandatory.

The IBM Cloud CLI mandates that commands start with `ibmcloud`. However, until the "Bluemix" brand is phased out, you can also start commands by `bx` and `bluemix`. So, you can do `ibmcloud cos`, `bluemix cos`, or `bx cos` to start a command.

### Abort a multipart upload
{: #ic-abort-multipart-upload}
* **Action:** Abort a multipart upload instance by ending the upload to the bucket in the user's IBM Cloud Object Storage account.
* **Usage:** `ibmcloud cos abort-multipart-upload --bucket BUCKET_NAME --key KEY --upload-id ID [--region REGION]`
* **Parameters to provide:**
	* The name of the bucket.
		* Flag: `--bucket BUCKET_NAME`
	* The KEY of the object.
		* Flag: `--key KEY`
	* Upload ID identifying the multipart upload.
		* Flag: `--upload-id ID`
	* _Optional_: The REGION where the bucket is present. If this flag is not provided, the program will use the default option specified in config.
		* Flag: `--region REGION`


### Complete a multipart upload
{: #ic-complete-multipart-upload}
* **Action:** Complete a multipart upload instance by assembling the currently uploaded parts and uploading the file to the bucket in the user's IBM Cloud Object Storage account.
* **Usage:** `ibmcloud cos complete-multipart-upload --bucket BUCKET_NAME --key KEY --upload-id ID [--multipart-upload VALUE] [--region REGION]`
* **Parameters to provide:**
	* The name of the bucket.
		* Flag: `--bucket BUCKET_NAME`
	* The KEY of the object.
		* Flag: `--key KEY`
	* Upload ID identifying the multipart upload.
		* Flag: `--upload-id ID`
	* _Optional_: The VALUE of MultipartUpload to set.
		* Flag: `--multipart-upload VALUE`
	* _Optional_: The REGION where the bucket is present. If this flag is not provided, the program will use the default option specified in config.
		* Flag: `--region REGION`


### Configure the Program
{: #ic-config}
* **Action:** Configure the program's preferences.
* **Usage:** `ibmcloud cos config [COMMAND]`
* **Commands:**
	* Switch between HMAC and IAM authentication.
		* Command: `auth`
	* Store CRN in the config.
		* Command: `crn`
	* Store Default Download Location in the config.
		* Command: `ddl`
	* Store HMAC credentials in the config.
		* Command: `hmac`
	* List configuration.
		* Command: `list`
	* Store Default Region in the config.
		* Command: `region`


### Copy object from bucket
{: #ic-copy-object}
* **Action:** Copy an object from source bucket to destination bucket.
* **Usage:** `ibmcloud cos copy-object --bucket BUCKET_NAME --key KEY --copy-source SOURCE [--cache-control CACHING_DIRECTIVES] [--content-disposition DIRECTIVES] [--content-encoding CONTENT_ENCODING] [--content-language LANGUAGE] [--content-type MIME] [--copy-source-if-match ETAG] [--copy-source-if-modified-since TIMESTAMP] [--copy-source-if-none-match ETAG] [--copy-source-if-unmodified-since TIMESTAMP] [--metadata MAP] [--metadata-directive DIRECTIVE] [--region REGION]`
* **Parameters to provide:**
    * The name of the bucket.
		* Flag: `--bucket BUCKET_NAME`
	* The KEY of the object.
		* Flag: `--key KEY`
	* (SOURCE) The name of the source bucket and key name of the source object, separated by a slash (/). Must be URL-encoded.
		* Flag: `--copy-source SOURCE`
	* _Optional_: Specifies CACHING_DIRECTIVES for the request/reply chain.
		* Flag: `--cache-control CACHING_DIRECTIVES`
	* _Optional_: Specifies presentational information (DIRECTIVES).
		* Flag: `--content-disposition DIRECTIVES`
	* _Optional_: Specifies what content encodings (CONTENT_ENCODING) have been applied to the object and thus what decoding mechanisms must be applied to obtain the media-type referenced by the Content-Type header field.
		* Flag: `--content-encoding CONTENT_ENCODING`
	* _Optional_: The LANGUAGE the content is in.
		* Flag: `--content-language LANGUAGE`
	* _Optional_: A standard MIME type describing the format of the object data.
		* Flag: `--content-type MIME`
	* _Optional_: Copies the object if its entity tag (Etag) matches the specified tag (ETAG).
		* Flag: `--copy-source-if-match ETAG`
	* _Optional_: Copies the object if it has been modified since the specified time (TIMESTAMP).
		* Flag: `--copy-source-if-modified-since TIMESTAMP`
	* _Optional_: Copies the object if its entity tag (ETag) is different than the specified tag (ETAG).
		* Flag: `--copy-source-if-none-match ETAG`
	* _Optional_: Copies the object if it hasn't been modified since the specified time (TIMESTAMP).
		* Flag: `--copy-source-if-unmodified-since TIMESTAMP`
	* _Optional_: A MAP of metadata to store. Syntax: KeyName1=string,KeyName2=string
		* Flag: `--metadata MAP`
	* _Optional_: Specifies whether the metadata is copied from the source object or replaced with metadata provided in the request. DIRECTIVE values: COPY,REPLACE.
		* Flag: ` --metadata-directive DIRECTIVE`
	* _Optional_: The REGION where the bucket is present. If this flag is not provided, the program will use the default option specified in config.
		* Flag: `--region REGION`


### Create a new bucket
{: #ic-create-bucket}

* **Action:** Create a new bucket in an IBM Cloud Object Storage instance.
* **Usage:** `ibmcloud cos create-bucket --bucket BUCKET_NAME [--class CLASS_NAME] [--ibm-service-instance-id ID] [--region REGION]`
* **Parameters to provide:**
    * The name of the bucket.
		* Flag: `--bucket BUCKET_NAME`
	* _Optional_: The name of the Class.
		* Flag: `--class CLASS_NAME`
	* _Optional_: Sets the IBM Service Instance ID in the request.
		* Flag: `--ibm-service-instance-id ID`
	* _Optional_: The REGION where the bucket is present. If this flag is not provided, the program will use the default option specified in config.
		* Flag: `--region REGION`



### Create a new multipart upload
{: #ic-create-multipart-upload}
* **Action:** Begin the multipart file upload process by creating a new multipart upload instance.
* **Usage:** `ibmcloud cos create-multipart-upload --bucket BUCKET_NAME --key KEY [--cache-control CACHING_DIRECTIVES] [--content-disposition DIRECTIVES] [--content-encoding CONTENT_ENCODING] [--content-language LANGUAGE] [--content-type MIME] [--metadata MAP] [--region REGION]`
* **Parameters to provide:**
    * The name of the bucket.
		* Flag: `--bucket BUCKET_NAME`
	* The KEY of the object.
		* Flag: `--key KEY`
	* _Optional_: Specifies CACHING_DIRECTIVES for the request/reply chain.
		* Flag: `--cache-control CACHING_DIRECTIVES`
	* _Optional_: Specifies presentational information (DIRECTIVES).
		* Flag: `--content-disposition DIRECTIVES`
	* _Optional_: Specifies what content encodings (CONTENT_ENCODING) have been applied to the object and thus what decoding mechanisms must be applied to obtain the media-type referenced by the Content-Type header field.
		* Flag: `--content-encoding CONTENT_ENCODING`
	* _Optional_: The LANGUAGE the content is in.
		* Flag: `--content-language LANGUAGE`
	* _Optional_: A standard MIME type describing the format of the object data.
		* Flag: `--content-type MIME`
	* _Optional_:  A MAP of metadata to store. Syntax: KeyName1=string,KeyName2=string
		* Flag: `--metadata MAP`
	* _Optional_: The REGION where the bucket is present. If this flag is not provided, the program will use the default option specified in config.
		* Flag: `--region REGION`


### Delete an existing bucket
{: #ic-delete-bucket}

* **Action:** Delete an existing bucket in an IBM Cloud Object Storage instance.
* **Usage:** `ibmcloud cos delete-bucket --bucket BUCKET_NAME [--region REGION] [--force]`
* **Parameters to provide:**
    * The name of the bucket.
		* Flag: `--bucket BUCKET_NAME`
    * _Optional_: The REGION where the bucket is present. If this flag is not provided, the program will use the default option specified in config.
       * Flag: `--region REGION`
    * _Optional_: The operation will do not ask for confirmation.
       * Flag: `--force`


### Delete bucket CORS
{: #ic-delete-bucket-cors}
* **Action:** Delete CORS configuration on a bucket in a user's IBM Cloud Object Storage account.
* **Usage:** `ibmcloud cos delete-bucket-cors --bucket BUCKET_NAME [--region REGION]`
* **Parameters to provide:**
    * The name of the bucket.
		* Flag: `--bucket BUCKET_NAME`
	* _Optional_: The REGION where the bucket is present. If this flag is not provided, the program will use the default option specified in config.
		* Flag: `--region REGION`


### Delete an object
{: #ic-delete-object}
* **Action:** Delete an object from a bucket in a user's IBM Cloud Object Storage account.
* **Usage:** `ibmcloud cos delete-object --bucket BUCKET_NAME --key KEY [--region REGION] [--force]`
* **Parameters to provide:**
    * The name of the bucket.
		* Flag: `--bucket BUCKET_NAME`
	* The KEY of the object.
		* Flag: `--key KEY`
	* _Optional_: The REGION where the bucket is present. If this flag is not provided, the program will use the default option specified in config.
		* Flag: `--region REGION`
    * _Optional_: The operation will do not ask for confirmation.
       * Flag: `--force`


### Delete multiple objects
{: #ic-delete-objects}
* **Action:** Delete multiple objects from a bucket in a user's IBM Cloud Object Storage account.
* **Usage:** `ibmcloud cos delete-objects --bucket BUCKET_NAME --delete VALUE [--region REGION]`
* **Parameters to provide:**
    * The name of the bucket.
		* Flag: `--bucket BUCKET_NAME`
    *The VALUE of Delete to set.
		* Flag: `--delete`  Syntax: Objects=[{Key=string},{Key=string}],Quiet=boolean
	* _Optional_: The REGION where the bucket is present. If this flag is not provided, the program will use the default option specified in config.
		* Flag: `--region REGION`


### Get a bucket's class
{: #ic-bucket-class}
* **Action:** Determine the class of a bucket in an IBM Cloud Object Storage instance.
* **Usage:** `ibmcloud cos get-bucket-class --bucket BUCKET_NAME`
* **Parameters to provide:**
	* The name of the bucket.
		* Flag: `--bucket BUCKET_NAME`


### Get bucket CORS
{: #ic-get-bucket-cors}
* **Action:** Returns the CORS configuration for the bucket in a user's IBM Cloud Object Storage account.
* **Usage:** `ibmcloud cos get-bucket-cors --bucket BUCKET_NAME [--region REGION]`
* **Parameters to provide:**
    * The name of the bucket.
		* Flag: `--bucket BUCKET_NAME`
	* _Optional_: The REGION where the bucket is present. If this flag is not provided, the program will use the default option specified in config.
		* Flag: `--region REGION`


### Find a bucket
{: #ic-find-bucket}
* **Action:** Determine the location and class of a bucket in an IBM Cloud Object Storage instance. 
* **Usage:** `ibmcloud cos get-bucket-location --bucket BUCKET_NAME`
* **Parameters to provide:**
	* The name of the bucket.
		* Flag: `--bucket BUCKET_NAME`
	


### Download an object
{: #ic-download-object}
* **Action:** Download an object from a bucket in a user's IBM Cloud Object Storage account.
* **Usage:** `ibmcloud cos get-object --bucket BUCKET_NAME --key KEY [--if-match ETAG] [--if-modified-since TIMESTAMP] [--if-none-match ETAG] [--if-unmodified-since TIMESTAMP] [--range RANGE] [--response-cache-control HEADER] [--response-content-disposition HEADER] [--response-content-encoding HEADER] [--response-content-language HEADER] [--response-content-type HEADER] [--response-expires HEADER] [--region REGION] [OUTFILE]`
* **Parameters to provide:**
    * The name of the bucket.
		* Flag: `--bucket BUCKET_NAME`
	* The KEY of the object.
		* Flag: `--key KEY`
	* _Optional_: Return the object only if its entity tag (ETag) is the same as the ETAG specified, otherwise return a 412 (precondition failed).
		* Flag: `--if-match ETAG`
	* _Optional_: Return the object only if it has been modified since the specified TIMESTAMP, otherwise return a 304 (not modified).
		* Flag: `--if-modified-since TIMESTAMP`
	* _Optional_: Return the object only if its entity tag (ETag) is different from the ETAG specified, otherwise return a 304 (not modified).
		* Flag: `--if-none-match ETAG`
	* _Optional_: Return the object only if it has not been modified since the specified TIMESTAMP, otherwise return a 412 (precondition failed).
		* Flag: `--if-unmodified-since TIMESTAMP`
	* _Optional_: Downloads the specified RANGE bytes of an object.
		* Flag: `--range RANGE`
	* _Optional_: Sets the Cache-Control HEADER of the response.
		* Flag: `--response-cache-control HEADER`
	* _Optional_: Sets the Content-Disposition HEADER of the response.
		* Flag: `--response-content-disposition HEADER`
	* _Optional_: Sets the Content-Encoding HEADER of the response.
		* Flag: `--response-content-encoding HEADER`
	* _Optional_: Sets the Content-Language HEADER of the response.
		* Flag: `--response-content-language HEADER`
	* _Optional_: Sets the Content-Type HEADER of the response.
		* Flag: `--response-content-type HEADER`
	* _Optional_: Sets the Expires HEADER of the response.
		* Flag: `--response-expires HEADER`
	* _Optional_: The REGION where the bucket is present. If this flag is not provided, the program will use the default option specified in config.
		* Flag: `--region REGION`
	* _Optional_: The location where to save the content of the object. If this parameter is not provided, the program will use the default location specified in the `credentials.json` file located in the user's `.bluemix` folder.
		* Parameter : `OUTFILE`


### Get a bucket's headers
{: #ic-bucket-header}
* **Action:** Determine if a bucket exists in an IBM Cloud Object Storage instance.
* **Usage:** `ibmcloud cos head-bucket --bucket BUCKET_NAME [--region REGION]`
* **Parameters to provide:**
	* The name of the bucket.
		* Flag: `--bucket BUCKET_NAME`
	* _Optional_: The REGION where the bucket is present. If this flag is not provided, the program will use the default option specified in config.
		* Flag: `--region REGION`


### Get an object's headers
{: #ic-object-header}
* **Action:** Determine if a file exists in a bucket in a user's IBM Cloud Object Storage account.
* **Usage:** `ibmcloud cos head-object --bucket BUCKET_NAME --key KEY [--if-match ETAG] [--if-modified-since TIMESTAMP] [--if-none-match ETAG] [--if-unmodified-since TIMESTAMP] [--range RANGE] [--region REGION]`
* **Parameters to provide:**
    * The name of the bucket.
		* Flag: `--bucket BUCKET_NAME`
	* The KEY of the object.
		* Flag: `--key KEY`
	* _Optional_: Return the object only if its entity tag (ETag) is the same as the ETAG specified, otherwise return a 412 (precondition failed).
		* Flag: `--if-match ETAG`
	* _Optional_: Return the object only if it has been modified since the specified TIMESTAMP, otherwise return a 304 (not modified).
		* Flag: `--if-modified-since TIMESTAMP`
	* _Optional_: Return the object only if its entity tag (ETag) is different from the ETAG specified, otherwise return a 304 (not modified).
		* Flag: `--if-none-match ETAG`
	* _Optional_: Return the object only if it has not been modified since the specified TIMESTAMP, otherwise return a 412 (precondition failed).
		* Flag: `--if-unmodified-since TIMESTAMP`
	* Downloads the specified RANGE bytes of an object.
		* Flag: `--range RANGE`
	* _Optional_: The REGION where the bucket is present. If this flag is not provided, the program will use the default option specified in config.
		* Flag: `--region REGION`


### List all buckets
{: #ic-list-buckets}
* **Action:** Print a list of all the buckets in a user's IBM Cloud Object Storage account. Note that buckets may be located in different regions.
* **Usage:** `ibmcloud cos list-buckets`
* **Parameters to provide:**
    * No parameters to provide.


### List in-progress multipart uploads
{: #ic-list-multipart-uploads}
* **Action:** This operation lists in-progress multipart uploads.
* **Usage:** `ibmcloud cos list-multipart-uploads --bucket BUCKET_NAME [--delimiter DELIMITER] [--encoding-type METHOD] [--prefix PREFIX] [--key-marker value] [--upload-id-marker value] [--page-size SIZE] [--max-items NUMBER] [--region REGION]`
* **Parameters to provide:**
    * The name of the bucket.
		* Flag: `--bucket BUCKET_NAME`
	* _Optional_: A DELIMITER is a character you use to group keys.
		* Flag: `--delimiter DELIMITER`
	* _Optional_: Requests to encode the object keys in the response and specifies the encoding METHOD to use.
		* Flag: `--encoding-type METHOD`
	* _Optional_: Limits the response to keys that begin with the specified PREFIX.
		* Flag: `--prefix PREFIX`
	* _Optional_:  Together with upload-id-marker, this parameter specifies the multipart upload after which listing should begin.
		* Flag: `--key-marker value`
	* _Optional_: Together with key-marker, specifies the multipart upload after which listing should begin. If key-marker is not specified, the upload-id-marker parameter is ignored.
		* Flag: `--upload-id-marker value`
	* _Optional_: The SIZE of each page to get in the service call. This does not affect the number of items returned in the command's output. Setting a smaller page size results in more calls to the AWS service, retrieving fewer items in each call. This can help prevent the service calls from timing out. (default: 1000).
		* Flag: `--page-size SIZE`
	* _Optional_: The total NUMBER of items to return in the command's output. If the total number of items available is more than the value specified, a NextToken is provided in the command's output. To resume pagination, provide the NextToken value in the starting-token argument of a subsequent command. (default: 0).
		* Flag: `--max-items NUMBER`
	* _Optional_: The REGION where the bucket is present. If this flag is not provided, the program will use the default option specified in config.
		* Flag: `--region REGION`


### List objects
{: #ic-list-objects}
* **Action:** List files present in a bucket in a user's IBM Cloud Object Storage Account.  This operation is currently limited to the 1000 most recently created objects and can't be filtered.
* **Usage:** `ibmcloud cos list-objects --bucket BUCKET_NAME [--delimiter DELIMITER] [--encoding-type METHOD] [--prefix PREFIX] [--starting-token TOKEN] [--page-size SIZE] [--max-items NUMBER] [--region REGION]`
* **Parameters to provide:**
	* The name of the bucket.
		* Flag: `--bucket BUCKET_NAME`
	* _Optional_: A DELIMITER is a character you use to group keys.
		* Flag: `--delimiter DELIMITER`
	* _Optional_: Requests to encode the object keys in the response and specifies the encoding METHOD to use.
		* Flag: `--encoding-type METHOD`
	* _Optional_: Limits the response to keys that begin with the specified PREFIX.
		* Flag: `--prefix PREFIX`
	* _Optional_: A TOKEN to specify where to start paginating. This is the NextToken from a previously truncated response.
		* Flag: `--starting-token TOKEN`
	* _Optional_: The SIZE of each page to get in the service call. This does not affect the number of items returned in the command's output. Setting a smaller page size results in more calls to the AWS service, retrieving fewer items in each call. This can help prevent the service calls from timing out. (default: 1000)
		* Flag: `--page-size SIZE`
	* _Optional_: The total NUMBER of items to return in the command's output. If the total number of items available is more than the value specified, a NextToken is provided in the command's output. To resume pagination, provide the NextToken value in the starting-token argument of a subsequent command. (default: 0)
		* Flag: `--max-items NUMBER`
	* _Optional_: The REGION where the bucket is present. If this flag is not provided, the program will use the default option specified in config.
		* Flag: `--region REGION`


### List parts
{: #ic-list-parts}
* **Action:** Print out information about an in progress multipart upload instance.
* **Usage:** `ibmcloud cos list-parts --bucket BUCKET_NAME --key KEY --upload-id ID --part-number-marker VALUE [--page-size SIZE] [--max-items NUMBER] [--region REGION]`
* **Parameters to provide:**
	* The name of the bucket.
		* Flag: `--bucket BUCKET_NAME`
	* The KEY of the object.
		* Flag: `--key KEY`
	* Upload ID identifying the multipart upload.
		* Flag: `--upload-id ID`
	* Part number VALUE after which listing begins (default: 1)
		* Flag: `--part-number-marker VALUE`
	* _Optional_: The SIZE of each page to get in the service call. This does not affect the number of items returned in the command's output. Setting a smaller page size results in more calls to the AWS service, retrieving fewer items in each call. This can help prevent the service calls from timing out. (default: 1000)
		* Flag: `--page-size SIZE`
	* _Optional_: The total NUMBER of items to return in the command's output. If the total number of items available is more than the value specified, a NextToken is provided in the command's output. To resume pagination, provide the NextToken value in the starting-token argument of a subsequent command. (default: 0)
		* Flag: `--max-items NUMBER`
	* _Optional_: The REGION where the bucket is present. If this flag is not provided, the program will use the default option specified in config.
		* Flag: `--region REGION`


### Set bucket CORS
{: #ic-set-bucket-cors}
* **Action:** Sets the CORS configuration for a bucket in the user's IBM Cloud Object Storage account.
* **Usage:** `ibmcloud cos put-bucket-cors --bucket BUCKET_NAME [--cors-configuration VALUE] [--content-md5 MD5] [--region REGION]`
* **Parameters to provide:**
	* The name of the bucket.
		* Flag: `--bucket BUCKET_NAME`
	* _Optional_: The VALUE of Cors Configuration to set.
		* Flag: `--cors-configuration VALUE`
	* _Optional_: The base64-encoded 128-bit MD5 digest of the data.
		* Flag: `--content-md5 MD5`
	* _Optional_: The REGION where the bucket is present. If this flag is not provided, the program will use the default option specified in config.
		* Flag: `--region REGION`



### Put object
{: #ic-upload-object}
* **Action:** Upload an object to a bucket in a user's IBM Cloud Object Storage account.
* **Usage:** `ibmcloud cos put-object --bucket BUCKET_NAME --key KEY [--body FILE_PATH] [--cache-control CACHING_DIRECTIVES] [--content-disposition DIRECTIVES] [--content-encoding CONTENT_ENCODING] [--content-language LANGUAGE] [--content-length SIZE] [--content-md5 MD5] [--content-type MIME] [--metadata MAP] [--region REGION]`
* **Parameters to provide:**
    * The name of the bucket.
		* Flag: `--bucket BUCKET_NAME`
	* The KEY of the object.
		* Flag: `--key KEY`
	* _Optional_: Object data location (FILE_PATH).
		* Flag: `--body FILE_PATH`
	* _Optional_: Specifies CACHING_DIRECTIVES for the request/reply chain.
		* Flag: `--cache-control CACHING_DIRECTIVES`
	* _Optional_: Specifies presentational information (DIRECTIVES).
		* Flag: `--content-disposition DIRECTIVES`
	* _Optional_: Specifies what content encodings (CONTENT_ENCODING) have been applied to the object and thus what decoding mechanisms must be applied to obtain the media-type referenced by the Content-Type header field.
		* Flag: `--content-encoding CONTENT_ENCODING`
	* _Optional_: The LANGUAGE the content is in.
		* Flag: `--content-language LANGUAGE`
	* _Optional_:  SIZE of the body in bytes. This parameter is useful when the size of the body cannot be determined automatically. (default: 0)
		* Flag: `--content-length SIZE`
	* _Optional_: The base64-encoded 128-bit MD5 digest of the data.
		* Flag: `--content-md5 MD5`
	* _Optional_: A standard MIME type describing the format of the object data.
		* Flag: `--content-type MIME`
	* _Optional_: A MAP of metadata to store. Syntax: KeyName1=string,KeyName2=string
		* Flag: `--metadata MAP`
	* _Optional_: The REGION where the bucket is present. If this flag is not provided, the program will use the default option specified in config.
		* Flag: `--region REGION`


## Manually controlling multipart uploads
{: #ic-manual-multipart-uploads}

The IBM Cloud Object Storage CLI provides the ability for users to upload large files in multiple parts using the AWS multipart upload functionality. To initiate a new multipart upload, run the `multipart-upload-create` command, which returns the new upload instance's upload ID. In order to continue with the upload process, you must save the upload ID for each subsequent command. This command requires you to generate an MD5 hash. Refer to the [Amazon documentation](https://aws.amazon.com/premiumsupport/knowledge-center/s3-multipart-upload-cli/) for more information on how to generate an MD5 hash for a multipart upload instance.

Once you have run the `multipart-upload-complete` command, run `part-upload` for each file part you wish to upload. **Note that for multipart uploads, every file part (except for the last part) must be at least 5MB in size.** To split a file into separate parts, you can run `split` in a terminal window. For example, if you have a 13MB file named `TESTFILE` on your Desktop, and you would like to split it into file parts of 5MB each, you can run `split -b 3m ~/Desktop/TESTFILE part-file-`. The Terminal will generate 3 file parts � two file parts of 5MB each, and one file part of 3MB, with the names `part-file-aa`, `part-file-ab`, and `part-file-ac`. For more information on this process, refer to the attached video in the [Amazon documentation.](https://aws.amazon.com/premiumsupport/knowledge-center/s3-multipart-upload-cli/)

As each file part is uploaded, the CLI will print out its ETag. You must save this ETag into an appropriately formatted JSON file, along with the part number. Below is an example of how the JSON file should be formatted. Use this template to create your own ETag JSON data file.

```
{
  "Parts": [
    {
      "PartNumber": 1,
      "ETag": "The ETag of the first file part goes here."
    },
    {
      "PartNumber": 2,
      "ETag": "The ETag of the second file part goes here."
    }
  ]
}
```

Add more entries to this JSON template as necessary.

To see the status of your multipart upload instance, you can always run the `part-list` command, providing the bucket name, key, and the upload ID. This will print out raw information about your multipart upload instance. Once you have completed uploading each part of the file, run the `multipart-upload-complete` command with the necessary parameters. If all goes well, you will receive a confirmation that the file uploaded successfully to the desired bucket.

### Upload a part
{: #ic-upload-part}
* **Action:** Upload a part of a file in an existing multipart upload instance.
* **Usage:** `ibmcloud cos upload-part --bucket BUCKET_NAME --key KEY --upload-id ID --part-number NUMBER [--body FILE_PATH] [--region REGION]`
	* Note that you must save each uploaded file part's number and ETag (which the CLI will print out for you) for each part into a JSON file. Refer to the "Multipart Upload Guide" below for more information.
* **Parameters to provide:**
	* The bucket name where the multipart upload is taking place.
		* Flag: `--bucket BUCKET_NAME`
	* The KEY of the object.
		* Flag: `--key KEY`
	* Upload ID identifying the multipart upload.
		* Flag: `--upload-id ID`
	* Part NUMBER of part being uploaded. This is a positive integer between 1 and 10,000. (default: 1)
		* Flag: `--part-number NUMBER`
	* _Optional_: Object data location (FILE_PATH).
		* Flag: `--body FILE_PATH`
	* _Optional_: The REGION where the bucket is present. If this flag is not provided, the program will use the default option specified in config.
		* Flag: `--region REGION`


### Upload a part copy
{: #ic-upload-a-part-copy}
* **Action:** Upload a part by copying data from an existing object.
* **Usage:** `ibmcloud cos upload-part-copy --bucket BUCKET_NAME --key KEY --upload-id ID --part-number NUMBER --copy-source SOURCE [--copy-source-if-match ETAG] [--copy-source-if-modified-since TIMESTAMP] [--copy-source-if-none-match ETAG] [--copy-source-if-unmodified-since TIMESTAMP] [--copy-source-range value] [--region REGION]`
	* Note that you must save each uploaded file part's number and ETag (which the CLI will print out for you) for each part into a JSON file. Refer to the "Multipart Upload Guide" below for more information.
* **Parameters to provide:**
	* The name of the bucket.
		* Flag: `--bucket BUCKET_NAME`
	* The KEY of the object.
		* Flag: `--key KEY`
	* Upload ID identifying the multipart upload.
		* Flag: `--upload-id ID`
	* Part NUMBER of part being uploaded. This is a positive integer between 1 and 10,000.
		* Flag: `--part-number PART_NUMBER`
	* (SOURCE) The name of the source bucket and key name of the source object, separated by a slash (/). Must be URL-encoded.
		* Flag: `--copy-source SOURCE`
	* _Optional_: Copies the object if its entity tag (Etag) matches the specified tag (ETAG).
		* Flag: `--copy-source-if-match ETAG`
	* _Optional_: Copies the object if it has been modified since the specified time (TIMESTAMP).
		* Flag: `--copy-source-if-modified-since TIMESTAMP`
	* _Optional_: Copies the object if its entity tag (ETag) is different than the specified tag (ETAG).
		* Flag: `--copy-source-if-none-match ETAG`
	* _Optional_: Copies the object if it hasn't been modified since the specified time (TIMESTAMP).
		* Flag: `--copy-source-if-unmodified-since TIMESTAMP`
	* _Optional_: The range of bytes to copy from the source object. The range value must use the form bytes=first-last, where the first and last are the zero-based byte offsets to copy. For example, bytes=0-9 indicates that you want to copy the first ten bytes of the source. You can copy a range only if the source object is greater than 5 MB.
		* Flag: `--copy-source-range value`
	* _Optional_: The REGION where the bucket is present. If this flag is not provided, the program will use the default option specified in config.
		* Flag: `--region REGION`


### Wait
{: #ic-wait}
* **Action:** Wait until a particular condition is satisfied. Each subcommand polls an API until the listed requirement is met.
* **Usage:** `ibmcloud cos wait command [arguments...] [command options]`
* **Commands:**
    * bucket-exists
		* Wait until 200 response is received when polling with head-bucket. It will poll every 5 seconds until a successful state has been reached. This will exit with a return code of 255 after 20 failed checks.
	* bucket-not-exists
		* Wait until 404 response is received when polling with head-bucket. It will poll every 5 seconds until a successful state has been reached. This will exit with a return code of 255 after 20 failed checks.
	* object-exists
		* Wait until 200 response is received when polling with head-object. It will poll every 5 seconds until a successful state has been reached. This will exit with a return code of 255 after 20 failed checks.
	* object-not-exists
		* Wait until 404 response is received when polling with head-object. It will poll every 5 seconds until a successful state has been reached. This will exit with a return code of 255 after 20 failed checks.

