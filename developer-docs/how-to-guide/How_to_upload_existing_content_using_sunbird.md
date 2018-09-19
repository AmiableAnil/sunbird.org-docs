---
title: Uploading Content on Sunbird Portal
page_title: Uploading and Publishing Content 
description: Uploading and Publishing Existing Content
keywords: uploading content, existing content, training material
published: true
allowSearch: true
---

## Scenario

XYZ Corp, is a global conglomerate with over ten thousand employees, spread across 7 locations. Employee training and enablement is one of the core values of the organization. Before the organization opted to use the Sunbird platform, they had a legacy system that employees accessed to train and upskill themselves. 
The legacy system has a large repository of content artifacts. These artifacts have to be uploaded into Sunbird so that employees can access them.
The organization also creates content artifacts and courses using multiple resources on an ongoing basis. Content and course creators also need to upload all such new content into Sunbird.  
 
## Prerequisites

* Content creation access

* Content artifacts with a unique object ID

## Intended Audience

* **Content Creator**: Users who have permissions to create, manage, and upload content artifacts

* **Content Reviewer**: Users who have permissions to review and publish content artifacts

> Note: Reviewers cannot change any content. They can only send review comments to content creators for modifications or publish the content artifact directly, if no modifications are required.

## Overview

Sunbird enables users who have the appropriate permissions to create, store, upload and consume various types of content. Users with content creation right can create and upload content on Sunbird.

Currently, the Sunbird platform supports the following content formats:

* Text (.pdf)

* Video (.mp4, .webm, YouTube URLs)

* HTML

* ECML (created using the inbuilt content editor)

* EPUB

* H5P

It also supports the following formats for in its resource library:

* Audio (.mp3)

* Images (.jpeg, .png)

* URLs for YouTube videos and other files

* Videos (.mp4) 

> Note: More file formats will be supported in future versions of Sunbird. 

Maximum file size supported on the platform:

<table>
  <tr>
    <td>Content/ File Type</td>
    <td>Maximum File Size</td>
  </tr>
  <tr>
    <td>Book,Course,Collection,Lesson Plan</td>
    <td>250 MB</td>
  </tr>
  <tr>
    <td>HTML (as zip files)</td>
    <td>50 MB</td>
  </tr>
  <tr>
    <td>EPUB</td>
    <td>50 MB</td>
  </tr>
  <tr>
    <td>H5P</td>
    <td>50 MB</td>
  </tr>
  <tr>
    <td>Video (.mp4, webm)</td>
    <td>50 MB</td>
  </tr>
  <tr>
    <td>.pdf</td>
    <td>50 MB</td>
  </tr>
</table>


Every content artifact must be tagged with the following metadata before it is uploaded on Sunbird:

- ContentType

- Mime Type

The uploaded content is validated through these metadata.

You can upload video content created by others, if:

* you have the required permissions from the original creator

* it adheres to prescribed content guidelines

* it is the accepted file format

* it is within the prescribed size 

### Taskflow

To complete this scenario, you need to create the content with appropriate metadata & ownership information, upload the existing content artifact, and publish the meterial for public usage.

You can upload existing content on the Sunbird platform using Upload Content API.

#### Uploading Content Using API

This API is associated with uploading content on the Sunbird Platform .

* The <b>_/upload/{content_ID}</b> endpoint executes "Upload Content" request based on the content metadata validation with the uploaded file.

* You need to provide a valid content ID value in {Content Id} field of API URL. 

* It is a must to provide values for the required parameters

**Path  Parameter:**

<table>
  <tr>
    <td>Path  Parameter</td>
    <td>Parameter Type</td>
    <td>Description</td>
    <td>Sample Value</td>
    <td>Is Mandatory</td>
  </tr>
  <tr>
    <td>Content ID
</td>
    <td>String</td>
    <td>Content ID of the Request URL</td>
    <td>do_11258058227713638416</td>
    <td>Yes</td>
  </tr>
</table>


**Form data Parameter:**

<table>
  <tr>
    <td>Form data Parameter</td>
    <td>Parameter Type</td>
    <td>Description</td>
    <td>Sample Value</td>
    <td>Is Mandatory</td>
  </tr>
  <tr>
    <td>file</td>
    <td>String</td>
    <td>Content file path that you want to upload</td>
    <td>sample.pdf</td>
    <td>Yes</td>
  </tr>
</table>


**Header Parameter**

<table>
  <tr>
    <td>Header Parameter</td>
    <td>Parameter Type</td>
    <td>Description</td>
    <td>Sample Value</td>
    <td>Is Mandatory</td>
  </tr>
  <tr>
    <td>Content-Type</td>
    <td>String</td>
    <td>The Content Type entity is the media type of the resource.Possible media types can be: Multipart/form-data</td>
    <td>multipart/form-data</td>
    <td>Yes</td>
  </tr>
  <tr>
    <td>X-Authenticated-Userid</td>
    <td>String</td>
    <td>Represents the registered User ID to execute the API.</td>
    <td>userName</td>
    <td>Yes</td>
  </tr>
  <tr>
    <td> Authorization</td>
    <td>String</td>
    <td>To make use of the API, you require authorization. Raise a request to the administrator for the use of the API. You will receive the authorization key. Specify the key received. </td>
    <td>api_key</td>
    <td>Yes</td>
  </tr>
  <tr>
    <td>ts</td>
    <td>String</td>
    <td>Time Stamp at which upload request was sent.</td>
    <td>2018-09-05T10:55:22Z</td>
    <td>Yes</td>
  </tr>
</table>


Following is an example of  <b>response body</b> for <b>uploading content API</b>:

{

    "id": "ekstep.learning.content.upload",

    "ver": "3.0",

    "ts": "2018-09-05T10:55:22ZZ",

    "params": {

        "resmsgid": "d6dui5d1-60u8-4a79-23f9-78796195c2h7",

        "msgid": null,

        "err": null,

        "status": "successful",

        "errmsg": null

    },

    "responseCode": "OK",

    "result": {

        "content_url": "https://ekstep-public-prod.s3-ap-south-1.amazonaws.com/content/do_112534095400542340156583/artifact/highq_153614492126723.pdf",

        "node_id": "do_112534095400542340156583",

        "versionKey": "153614492126723"

    }

}

For the youtube content or file url, pass it as fileUrl in <b>Upload API</b> or set the artifact Url of the content using  [Update Content API**](http://www.sunbird.org/apis/content/#operation/Update%20Content)

After you uploading the content, publish the content using **[Publish Content API**](http://www.sunbird.org/apis/content/#operation/Publish%20Content). 

Request Body for Publish Content API

{

  "request": {

    "content": {

      "lastPublishedBy": "sunbird",

      "publishChecklist": [
          "No Hate speech, Abuse, Violence,Profanity"
          "No Vulgarity",
          "No Discrimination or Defamation",
          "Is suitable for children",
          "Appropriate Title, Description",
          "Correct Board, Grade, Subject, Medium",
          "Appropriate tags such as Resource Type, Concepts",
          "Relevant Keywords",
          "Content plays correctly",
          "Can see the content clearly on Desktop and App",
          "Audio (if any) is clear and easy to understand",
          "No Spelling mistakes in the text",
          "Language is simple to understand"

      ]

    }

  }

}

Response Body for Publish Content API

{

  "result": {

    "node_id": "string",

    "versionKey": "string"

  },

  "id": ""ekstep.learning.content.publish",

  "ver": "3.0",

  "ts": "2018-09-14T10:44:43ZZ",

  "params": {

    "resmsgid": "d3415c1a-94c6-4dc7-9c28-3e0dac767ee3",

    "msgid": "null",

    "err": "null",

    "status": "string",

    "errmsg": "null"

  },

  "responseCode": "OK",<br> "result":{
    "publishStatus": "Publish Operation for Content Id 'do_2125903396473978881177' Started Successfully!",<br>
    "node_id": "do_2125903396473978881177"<br>
  }<br>

}


>Note: Reviewer has the right to publish content. Use id of one of the selected reviewers as publisher user id.



