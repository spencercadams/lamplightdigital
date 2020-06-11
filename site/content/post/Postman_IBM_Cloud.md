---
title: Postman in IBM Cloud
date: 2020-02-02
description: >-
  Leveraging Postman for API Testings
image: /img/code.jpg
---

## Using Postman with IBM Cloud

Before we get started, make sure you have your environment setup and have documentation ready-at-will:

* [SoftLayer API](https://sldn.softlayer.com/)
* [IBM Cloud API](https://cloud.ibm.com/apidocs)
* [IBM Cloud Docs](https://cloud.ibm.com/docs)

The Cloud Object Storage team put together a quick reference for their offering, available [here](https://cloud.ibm.com/docs/services/cloud-object-storage?topic=cloud-object-storage-postman).  At the same time, this is specific to Object Storage provisioned within Classic Infrastructure.  As Cloud Object Storage development has shifted to non-classic infrastructure provisioned COS, then I would advise setting up your own Postman library, but keep the other library for reference.

For example, to leverage non-classic infrastructure Cloud Object Storage, you can provision a bucket for a Service Instance already created via:
```
PUT https://[endpoint_example=s3.us-south.objectstorage.softlayer.net]/[name_of_bucket]
-H 'authorization: bearer <IAM_token>'
-H 'ibm-service-instance-id: 40easdlv-EXAMPLE-efggrf-dsdf5234-b4af44'
```
The Service Instance ID is only available after provisioning Cloud Object Storage instance.  Which you can obtain when you LIST buckets:
```
GET https://s3.us-south.objectstorage.softlayer.net/[name_of_bucket]/
-H 'authorization: bearer <IAM_token>'
```
To obtain the authorization, you can leverage the IBM Cloud CLI, after to login: `ibmcloud iam oauth-tokens`

Object Storage team recently established [Resource Configuration](https://cloud.ibm.com/apidocs/cos/cos-configuration) to grab metadata and various ancillary data, which is helpful when S3 API is lacking and more development resources will be available in the coming months.

I am hopeful that this feature request for a Postman library will obtain some traction within the Dev team at IBM Cloud = https://ibmcloud.ideas.aha.io/ideas/IDEA-I-2929

*Side note - IBM Cloud also has a [Terraform provider available](https://ibm-cloud.github.io/tf-ibm-docs/).  It is a self-created provider, outside of Hashicorp, but works.  You can follow the [tutorial](https://cloud.ibm.com/docs/terraform?topic=terraform-setup_cli) to setup*
