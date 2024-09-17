# Wesign SDK

[![PyPI - Version](https://img.shields.io/pypi/v/wesign-sdk.svg)](https://pypi.org/project/wesign-sdk)
[![PyPI - Python Version](https://img.shields.io/pypi/pyversions/wesign-sdk.svg)](https://pypi.org/project/wesign-sdk)

-----

## Table of Contents

- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [License](#license)

## Installation

```console
pip install wesign-sdk
```

## Configuration
The Wesign API uses API keys for authentication.

Wesign uses API keys for authentication. You can generate a Wesign API key in the [API keys](https://wesign.com) section of your Wesign account settings.

The wesign-sdk requires the configuration of a domain, which should be set to https://api.wesign.com.


```console
from wesign_sdk.sdk import WesignSDK

wesign_app = WesignSDK('https://api.wesign.com','<API KEY>')

```

### <span style="color:red;">&#x2022;</span> Exceptions :
- InvalidHostError : Exception raised on invalid host.
- InvalidAPIKeyError : Exception raised on invalid API key.


## Usage
Use listed api in order to get document signed. 

1. [Upload Documents](#upload-documents)
2. [Add Recipients](#add-recipients)
3. [Send Envelope for signing](#send-envelope-for-signing)
4. [Get Sign URL](#get-sign-url)
5. [Download Documents](#download-documents)
##
### <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAwCAYAAABXAvmHAAAACXBIWXMAAAsTAAALEwEAmpwYAAAA+0lEQVR4nO3VLQ7CQBAF4L3Eih6HOQScAIfmDMhq0NVgcegaCAq7GoMpBJKyBEc2/GyZaafTzkue36/7sjVGo9FoICs8toOsmLF9Sezhh8szLwIL2B5LP1oxIrAAV9x5ERQAR41I86vHdrK+VAI4SgT28PPdLRrhXgBkCCzgcCr9IhLhAgAJAgt4HiIW4d4AQgQLoAoCfpQNQIUwnAAKhOEGYBGmDYAQAW0GxNSONx+rgLSBGwDpEwLpAPtl87UAkun+73YSANInBNIBtun/AHYynQOA9AmBdICV/oxa6QCQPiFQQN+e0UQ6ICWuqTMKyPUGej4hjUZjROQBwgDUDcPYwFwAAAAASUVORK5CYII=" height=30 width=30>   Upload Documents 
Upload document to the wesign server. \
Allowed file types : .docx, .pdf, .png, .jpg, .ppt, .csv, .xlsx, .html, .txt

```console
from wesign_sdk.sdk import WesignSDK

wesign_app = WesignSDK('https://api.wesign.com','<API KEY>')

document_information = wesign_app.upload_documents('<absolute document path>')

```

#### <span style="color:red;">&#x2022;</span> Exceptions :
- Exception : raised by server.
- FileUploadingError : Exception raised during uploading file
- InvalidPathError : Invalid document path.


#### Returned response :

```console
{
    "document_id" : unique generated id for the document,
    "document_name" : document name,
    "created_on" : document uploaded timestamp,
    "converted" : true/false (usefull for other than pdf files, as all files will be converted to pdf.) 
    "uploaded_by" : Account holder user ID.
}

```


##

### <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAB4AAAAeCAYAAAA7MK6iAAAACXBIWXMAAAsTAAALEwEAmpwYAAADyUlEQVR4nLXVfUwbZRwH8GaJRhO3+PaX/+wf/3DzrwlcmhZSxljX0tIXesUCc7yUlW1YBhGSVtp77lrqgAHdlEJpCy1zTLKNwQyUjYrifAm+zZghi9NA1CC5KdZkL8Sx8jNPI8gWb4XS/pJv8uS53/P73OUuOR5vg2UwpDxmUe3aUa9MFZgVxE6EeFt4ySxT7q4XKQ0xwpD8ucaCdLb1NdGfjYXpLEXyf7WoiLKkoBZ1qo7R8tnuI1I4U6N4IH1HFdBclBGmNPyahKJITfDt+YLfMfAwuorXKMChE/5Ba4hZa15aG9LufHzzcB4x1WuUcaIP38DbZVl3qTzi4qZQszzlJfw+Y4EBowxOVf13cw6dkMVn44bfVKUaOsqzI49Ce41yaCkRQWtZJnRX5kT38Bmring9btiSl+bwHBL/L3jqqBxchmxw6nfDbLAObl6hoKU0E96tkkPXoX1AqYljccNWdWp158G90XfnOSyBE/oscOKUZ4G7SgKTPRVw6+sGuHPVEc23/UZoLRZFXOXZy2ZV2sG4YZMyJcdZknm7rWT38sVjOlj4jF5FuGIvENxvOSBaMCtfyYgbRgWi5x06QdhRKIzEAlfSUCiI2PL5YSTa/kTcsA9JjjTuT484ioTrQnEc+4XQVJwR8VKSw3HDHmpvZR+ljOBhG4H77er7XkocP/yOac9zPbRs3v2GeN0w7u2mpfNeJH6Wt5nqsO7L6G2QL60XPv1W7r0uJBbwElEBW8718CQTE8U9Abv8Gi9R5aVzKib8pbdjwRP+kls+JEncLxIhtMVvk331/fvVy1zotaGqZb9NOol7eYmsk0iyzc9I734cKAX2U+sqiNcTPaXgt0nv+OoEW3nJqG5Gev2L9www4CRhpKMwmgtOEr48UwH4WkIxmWn4GRV1uVjLjA+2M7rFmUu1MHO5FqaGjNHgNd7D13AP7lWiwafjBrU1Z58k6bGTrzZ8OF/tm15kBn6DdncnjHr0USgK/osGPXpo97gB91R7pxd19vF5DRM6gWdsCFXUDb1A0qGpWv+Nv5uDf8Hx0ZWEweXtAn9jEQy49NHgtcvngePB8GofPlMb+OEeSX8wjWetF91KotAN+vzcGvDBtIzchLZz30Dr2avRNVcfOjcHGib0oxZ99FRMmKTHBk19s0tcwzYa0+mZJZIeO/9INNcy+nJx0+dsotCVHGj6hFVZhndwP61tvNPS/0tCUZz6/p8hnwl1cMJaOvRT85qPJFHBM/FsTlhDjbGV7u8WkhENdYnlhOXm4B5F/XB2MoJnr8X+AZKz63kCXXN7AAAAAElFTkSuQmCC"> Add Recipients
Include recipient details to send the envelope to the signer for document signing.

Wesign offers various types of fields that can be included in a document, as listed below.


- signature
- stamp
- initial
- checkbox
- radio
- text
- drawing
- date_signed
- full_name
- email
- company
- title
- plain_text
- comment_text
- dropdown
- attachment

**Note :** Each fields has different structure and attribute requirements.

The Recipient object must follow the proper structure and include the required attributes listed below:

- **recipient_name** (required) - Signer/Recipient Name.
- **recipient_email** (required) - Signer/Recipient Email ID.
- **action** (required) - Action to be taken by the recipient; it must be either `needs_to_sign` or `receive_copy`.
- **meta_data** (required) - Contains the field information that needs to be completed by the recipient or signer.
    -**page_no** (required) - Specify the page number of the document where this field should appear.
    - **left** (required) - Specify the X-axis position where the field should appear.
    - **top** (required) - Specify the Y-axis position where the field should appear.
    - **width** (required) - Specify the width of the field box.
    - **height** (required) - Specify the height of the field box.
    - **document_order** (required) - Specify the document order number corresponding to the sequence in which the documents were uploaded in the previous API call.
    - **field_name** (required) - Specify the field name, which must be selected from the predefined list of available field names.
    - **font_color** - Specify the font color in RGB format (e.g. `rgb(0,0,0)`).
    - **font_size** - Font size of the text.
    - **signature_with_border** - Indicate whether the signature should have a border and provide the generated unique signature ID.
    - **initial_with_border** - Indicate whether the initial should have a border and provide the generated unique initial ID.
    - **group** (required for field radio) - Specify the group name for **radio** buttons (e.g., `gender`).
    - **is_checked** - Mark `true` if the **checkbox** should be pre-checked.
    - **field_data** - Must not be null in case of **plain_text**, **dropdown**, **radio** fields.

```console
from wesign_sdk.sdk import WesignSDK

wesign_app = WesignSDK('https://api.wesign.com','<API KEY>')

document_information = wesign_app.upload_documents('<absolute document path>')

data = {
        "recipient_name": "Mayur P.",
        "recipient_email": "mayur@wesign.com",
        "action": "needs_to_sign",
        "meta_data": [
            {
                "page_no": 1,
                "left": 1,
                "top": 1,
                "width": 100,
                "height": 100,
                "document_order":1,
                "field_name": "signature",
                "include_date_name": True,
                "signature_with_border": True
            },{
                "page_no": 1,
                "left": 120,
                "top": 1,
                "width": 100,
                "height": 100,
                "document_order":1,
                "field_name": "initial",
                "include_date_name": None,
                "initial_with_border": False
            },{
                "page_no": 1,
                "left": 240,
                "top": 1,
                "width": 100,
                "height": 20,
                "document_order":1,
                "field_name": "email",
                "font_color" : "rgb(0,0,0)"
            },{
                "page_no": 1,
                "left": 1,
                "top": 150,
                "width": 100,
                "height": 20,
                "document_order":1,
                "field_name": "comment_text",
                "font_color" : "rgb(0,0,0)"
            },{
                "page_no": 1,
                "left": 120,
                "top": 150,
                "width": 100,
                "height": 20,
                "document_order":1,
                "field_name": "plain_text",
                "font_color" : "rgb(0,0,0)",
                "field_data" : "Field Data"
            },{
                "page_no": 1,
                "left": 240,
                "top": 150,
                "width": 100,
                "height": 100,
                "document_order":1,
                "field_name": "drawing",
            },{
                "page_no": 1,
                "left": 1,
                "top": 270,
                "width": 20,
                "height": 20,
                "document_order":1,
                "field_name": "attachment",
                "required_field_checkbox": True
            },{
                "page_no": 2,
                "left": 1,
                "top": 1,
                "width": 100,
                "height": 100,
                "document_order":1,
                "field_name": "signature",
                "include_date_name": True,
                "signature_with_border": True
            },{
                "page_no": 2,
                "left": 120,
                "top": 1,
                "width": 100,
                "height": 100,
                "document_order":1,
                "field_name": "initial",
                "include_date_name": None,
                "initial_with_border": False
            },{
                "page_no": 2,
                "left": 240,
                "top": 1,
                "width": 100,
                "height": 20,
                "document_order":1,
                "field_name": "email",
                "font_color" : "rgb(0,0,0)"
            },{
                "page_no": 2,
                "left": 1,
                "top": 150,
                "width": 100,
                "height": 20,
                "document_order":1,
                "field_name": "comment_text",
                "font_color" : "rgb(0,0,0)"
            },{
                "page_no": 2,
                "left": 120,
                "top": 150,
                "width": 100,
                "height": 20,
                "document_order":1,
                "field_name": "plain_text",
                "font_color" : "rgb(0,0,0)",
                "field_data" : "Field Data"
            },{
                "page_no": 2,
                "left": 240,
                "top": 150,
                "width": 100,
                "height": 100,
                "document_order":1,
                "field_name": "drawing",
            },{
                "page_no": 3,
                "left": 1,
                "top": 150,
                "width": 20,
                "height": 20,
                "field_name": "checkbox",
                "document_order":2,
                "is_checked": False
            }, {
                "page_no": 3,
                "left": 120,
                "top": 150,
                "width": 100,
                "height": 20,
                "field_name": "dropdown",
                "field_data": "Gender,Female,Male,dont want to answer",
                "document_order":2,
                "font_size": 10
            }, {
                "page_no": 3,
                "left": 240,
                "top": 150,
                "width": 10,
                "height": 10,
                "field_name": "radio",
                "field_data": "Male",
                "document_order":2,
                "group": "gender"
                
            }, {
                "page_no": 3,
                "left": 240,
                "top": 170,
                "width": 10,
                "height": 10,
                "field_name": "radio",
                "field_data": "Female",
                "document_order":2,
                "group": "gender"
            }, {
                "page_no": 1,
                "left": 1,
                "top": 270,
                "width": 20,
                "height": 20,
                "document_order":2,
                "field_name": "attachment",
                "required_field_checkbox": True
            },
        ],
        
    }

recipient_1 = wesign_app.add_recipient(data)

```



#### <span style="color:red;">&#x2022;</span> Exceptions :
- InvalidRecipientStructureError : Exception raised during validating recipient meta_data structure
- InvalidFontFamilyError : Exception raised during validating font-family
- Exception : General exception.
- InvalidDropDownOptions : Exception raised during validating dropdown structure.

##

### <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAwCAYAAABXAvmHAAAACXBIWXMAAAsTAAALEwEAmpwYAAAC6ElEQVR4nO2YTWgTQRiGRxFEUBRFaAh66alI9dCLBz1YitCDJxFvXgz1KChJRSyhYKFgsvNFRUTw4kGhPYmIB62Ch5gZAi1LpdUi2l6UoOBPdWeidmR/YrbWJJP9mU1hH/ggkMs3m2ffzbsIxcTExIRJvih2Fmh1CAi7jdYLhddis0bZMaB8AhNWBcoFJuwc6nQKpWofUF7AlH00l64P+3mdLHehTiRHf+zBhA0D4QvupXMvDJF59Nn6jAl/iDqJ8bLYjkv8FBD+GBO2svpqczEy9U30X3snrhQN+wCUn4x6Z5QVYqNGjQFM2B0gbPnfpcGZ1GRFdI+8FJeefHWWZ1/yRbElssU1wvcB5eOY8veNlgZHmcGbSyKR0cXpiYrb/1uRRR+mrNxsaXAps3/slbX80RuLq78vVw9FFn0yk5qsiL0XZ63ley/P//XembdCiA0RRV/zcSuTyOjWIWreu/TJKo0+2XErk3BmtffWg2ulUDa6lUWfF2USzqzx3r76z5VFnxdlatO71ntrNMJToUefH2Uae8/N7DfwtNjh+QBA2N0gFm+kTCPvoe7/PeTbd8IXw1Cmufe89gsMIr9opephTNmvIJVp5T3Y/3s+ZJ+JTSgIMOW5IJVp5j3UD5BDQT5dMWUzQSjTyntw5mqJH0BBYiaSmQp+lJHxHmz3Z1AYAGHnvSoj4z3U0yec2mg+0IDyKS/KyHgPKmpjvvg9CZR9akcZWe9BVW0Eyo7LKiPrPdTTR01t7BtbONIzOn8/OawbQXgPUdXGXem5bYm0PpRI62Xv3vPoaqOb/x1CxntQXRsb0ZXRz3jxHlTVxlbszs5uTV6w7wlZ70Ovje3SMzr3oD3vQ6iNfjiovRloy/ugamOQAOEnag87mdH81MawsN5YUP5UIvv91cYwMVMFKDuLCWNN/PdXG1Vgvxxg06HVRhWYpch8wwGE/Q6lNqpCKxn9QPhS4LVRJeZNa76yCbw2xsTEoHXLH1K6lxNbQo4wAAAAAElFTkSuQmCC" height=30 width=30> Send Envelope for signing

After uploading the document(s) and adding recipient(s), the user can send the envelope for signing.

When sending the envelope, Wesign requires certain keyword arguments, which are listed below.

- **subject** *(str)* : The subject line to address the envelope.

- **expiry_date** *(str - YYYY-MM-DD)* : The date when the envelope expires (format: YYYY-MM-DD).

- **follow_signing_order** *(bool)* : Expiry date for signing the envelope; after this date, recipients cannot sign the envelope.

- **enable_writing_id** *(bool)* : Disabling this will prevent writing the envelope ID on the top-left of each page of documents (default: true).

- **auto_reminder** *(int)* : Allows reminders to be sent to the recipient to sign the envelope. To enable this feature, specify the number of days between reminder intervals (default: 0).

- **number_of_reminders** *(int)* : Specifies the number of reminders to be sent to the recipient.

- **send_email_recipient** *(bool)* : Send email to recipient.


```console
from wesign_sdk.sdk import WesignSDK

wesign_app = WesignSDK('https://api.wesign.com','<API KEY>')

document_information = wesign_app.upload_documents('<absolute document path>')

data = {
        "recipient_name": "Mayur P.",
        "recipient_email": "mayur@wesign.com",
        "action": "needs_to_sign",
        "meta_data": [
            {
                "page_no": 1,
                "left": 1,
                "top": 1,
                "width": 100,
                "height": 100,
                "document_order":1,
                "field_name": "signature",
                "include_date_name": True,
                "signature_with_border": True
            },
            ...
        ],
        
    }

recipient_1 = wesign_app.add_recipient(data)

envelope = wesign_sdk.send_envelope(
    subject='subject', 
    expiry_date="2030-12-31", # DATE FORMAT - YYYY-MM-DD
    follow_signing_order=True, # default False
    enable_writing_id=True, # Default true
    auto_reminder=0, # default 0
    number_of_reminders=2 # default 0
    )

print(envelope)

```


#### <span style="color:red;">&#x2022;</span> Exceptions :
- ValueError : Excpection raised if any value is invalid.
- TypeError : Exception raised if any type is invalid.
- EnvelopeSendingError : Exception raised if server return with error.

#### <span style="color:green;">&#x2022;</span> Returned response :
In response, Wesign provides a detailed envelope with signing URLs. Developers should use these URLs to sign the documents.

```console
{
  "message": "Envelope Created.",
  "status": true,
  "status_code": 200,
  "envelope": {
    "id": 1,
    "envelope_documents": [
      {
        "id": 1,
        "document_key": "document_key",
        "priority": "document_order",
        "document_name": "document_name",
        "created_on": "created timestamp",
        "updated_on": "updated timestamp",
        "deleted": true/false,
        "document_id": "unique generated id",
        "is_attachment": true/false, // true in case of document is attachment during signing process
        "converted": true/false, // indicates document is converted to pdf or no
        "envelope": "envelope id"
      }
    ],
    "envelope_recepients": [
      {
        "id": "recipient id",
        "token": "unique token generated for recipient",
        "recepient_name": "recipient name",
        "recepient_email": "recipient email id",
        "signed_status": "signed status", // signed, unsinged, declined
        "signed_date": "signed timestamp",
        "action": "recipient actions", // needs_to_sign or recieve_copy
        "last_changed": "last changed timestamp",
        "last_viewed": "last viewed document timestamp",
        "meta_data": [
          {
            "page_no": "page number passed to sign on",
            "left": "X-axis coordinate",
            "top": "Y-axis coorfinate",
            "width": "element box width",
            "height": "element box height",
            "document_order": "document order",
            "field_name": "field_name",
            "element_id": "auto-generated element id",
            "color_code": "color-code assigned",
            "border_color": "border color-code assigned",
            "document_key": "auto assigned document key",
            "type": "element accept type", // image, text
          },
         ....
    ],
    "envelope_content": {
      "subject": "subject of the envelope",
      "content": "content to be send during emailing to the recipient",
      "envelope": "envelope id"
    },
    "subject": "subject of the envelope",
    "envelope_id": "auto-generated unique id of envelope",
    "location": "wesign",
    "sent": "envelope email status",
    "sent_on": "envelope email sent timestamp",
    "signed_status": "envelope signed status", // pending, completed, declined
    "last_changed": "last changed timestamp",
    "last_viewed": "last viewed document timestamp",
    "created_on": "created timestamp",
    "updated_on": "updated timestamp",
    "document_status": "envelope email status",,
    "im_signer": true/false, // true in case of acccount holder is signer
    "expiry_date": "envelope expiry date - YYYY-MM-DD",
    "enable_comments": true/false,
    "void": false/false,
    "voided_on": "voided timestamp",
    "deleted": true/false,
    "deleted_on": "deleted timestamp",
    "completed": true/false,
    "auto_reminder": "auto reminder days",
    "number_of_reminders": "number of auto reminder",
    "follow_signing_order": true/false, // indicates that envelope follows signing order
    "enable_writing_id": true/false, // indicates writing id on top-left of the pages.
    "api_v1": true,
    "holder": "account holder user id"
  },
  "signings_url": [
    {
      "recipient": "recipient email id",
      "signing_url": "signing url to be redirected"
    }
  ]
}

```



##

### <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAwCAYAAABXAvmHAAAACXBIWXMAAAsTAAALEwEAmpwYAAAEEUlEQVR4nO2Yz28TRxTHX9omjSqSS5XEO2NDVXKsqlYJSPkDeuHUc1X12FtSVBLv2G5iRClqA5EgCoJkdwvqvf9CBSGJWxrieGdoKkPizihATyC1Un6UiKlmTfjhHRsveGMj+SuNVs7m7X7eezPvzSxAU0011VRQGdN39iOHp7DDF7Aj/sY230G2uIdtMY9tnkQ/rsegEXXgUqEdO2ICOWILO0KWG8gWm9jhp3vP5d+GRlG3tdqDHJ6pBI59gy/0/HS7u0HgBQsGL4rZcHimrpk4cKkQwbZYeRl4/DQT4w0Hj2y+gRwxGrvMD/ZNL7aqK3LEmPq7bk1ELwvcOPCOuB+1xGGdHbLXB3ROYIeThoE3LN5XyR45YkyzFq6+FvBKajppbO/AXlSbV4VXUlVHY78FYTepcnU+CLxS1BK9e54B1WFrAa+EbJHWVK0rEJY6Tv0xgCy+U/pSw/rrYXvy+gyYi/urfVbUEoe1VcjmZu3J04V2GLo22XEy+9AXMYvLtvi8hKMZCfHcJpjsNAxW7qiGxftUxnQ9o/Z9IOH2QHzpVxiak12Ted/U6fg2K+GrOQUvgbDiMNkCmNn3gsDjYvR/qD08oQziyxKGZmXkYsH30re+npUwfOMp/JPh/guD+c7q4cV8bfdCwywCJlvxYJQDg1e96VL64pbBKxJGshoHvExcrxJ+RZXmcOA9B3JlM9D53dIncCx7HAjb8DtBJSTd/sjF2/2V4FVTDA/ei6QrH68B/yJ2xJhnl3A/1WXhzRTLGFPsAbZ5neB3I3l04UHX1K0L2t2mvT7g2Zvsl1Lb1m9yj4xzyxJbhXrBe+M+jNzoV2fY4jHQ74QxvXq8PU2/KLV9I0mlcTYrsbUWIryqNpXgifukw2Kbn9F24ulVGZn43WffQpg0zi5JNLMWErxqUoRmqoFXUocSbItZnwMX8rJr3O/AbgaQ5wD/M2ZzBDWVSSeqhd+VOoA//lRSdMBak8ZkTu474S+nbaM57x6yVjO1LZVKKRoDQreCwD+/FebjaGZtE00x+e73i7Il4Q/EvhPZHTxJJ8I5sBOa0sBvAKGHqn0EOn8r1nly6eeWBNVkkcp3TrlHIDSZbE7jwGiwZ7ifg0kf6Tsx/Q1CFaH3NHuY96u2N9lnZeEJ+6d0L1R7mXTb9+I0a6tB5LchsfwBhC6iycAwPfhKkVfww+wj2BMRek2zgxx7PeCVTJrUVyG3uLcp1cjNI5Xh3Q9hT5WiMTDpptYJlQnCer3joboSltZvmesR+WdF6JkyVaS6UVd4pS8XW8Gksy/nwM1tMPMfQ911bLnbO4gHirz6/wA9I3Spua4+iejXxLNTRt0ff9Gnk/opnouCyYg3rUx6Fwj7z7t6vxnx7jfVVFNNQUD9D+AcOX6Kbv2UAAAAAElFTkSuQmCC" height=30 width=30> Get Sign URL

After successfully creation of envelope. Developer can access signing URL by recipient Email-ID.

```console
from wesign_sdk.sdk import WesignSDK

wesign_app = WesignSDK('https://api.wesign.com','<API KEY>')

document_information = wesign_app.upload_documents('<absolute document path>')

data = {
        "recipient_name": "Mayur P.",
        "recipient_email": "mayur@wesign.com",
        "action": "needs_to_sign",
        "meta_data": [
            {
                "page_no": 1,
                "left": 1,
                "top": 1,
                "width": 100,
                "height": 100,
                "document_order":1,
                "field_name": "signature",
                "include_date_name": True,
                "signature_with_border": True
            },
            ...
        ],
        
    }

recipient_1 = wesign_app.add_recipient(data)

envelope = wesign_sdk.send_envelope(
    subject='subject', 
    expiry_date="2030-12-31", # DATE FORMAT - YYYY-MM-DD
    follow_signing_order=True, # default False
    enable_writing_id=True, # Default true
    auto_reminder=0, # default 0
    number_of_reminders=2 # default 0
    )

sign_url = wesign_sdk.get_sign_url('mayur@wesign.com')

```

#### <span style="color:green;">&#x2022;</span> Returned response :
Wesign returns a secure HTTP URL for signing the documents.
##

## <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAwCAYAAABXAvmHAAAACXBIWXMAAAsTAAALEwEAmpwYAAACrElEQVR4nO2YzW7aQBSFR/hBAoZg82NM36VddxGpqtoq7Y6l8x7ZeBMMBEggCRCiqqoQbRbpqn0F/9AC+3Yz1Z0fMrjBStuFPZKPdCRkMfZ3DIt7D0KpUqVKFZY5Xc/rN2tcn1Kb4MlyhmRRnYNfg1fUkxVGssjk0NcrXJvcG8kiU4CujamN8VKeALUQuDGiRrLICIFXr6iRLDJC4MSXP+QJUA2BV5iRLKpeLjfQlQvq8oVEASoh8PIQ/F2eAOUQeGlAjWRROQROfC5RgFIIXGdGsqgkQOtnC2LtbCFPAD0ErvWpkSzSBGhwsUeNZJG2BR5Qd4NkBtD6i28Pv/F78H3wKXUB3PGZva9JCHAs/k22oHeC+zjf9rHa9o7j5kfIwpliL7B3g/t/gBM7noM6WEGJkIUzhW5gc2gC/hA0uOXjXKLgxRCdwI4CV1teQuG3Qvi2CJ1veQRcdTycayYZnsvCmbzj26oALg88l4UzOce1Cbh08FwWzmSb3nMwfN5cTxWh2mg5h0qElFKsXavfrGOrBJ9ARcmrSVaSGeOIihKWcNIojJe012FhUEwyebMn1DSR9QysgbDPwlIuhkExyRCgeVEQWQ7og8Uv2KJgJazwMDEWUtUr1m6w/RrY9MHi584DxX7whSwi53QdhL0WDqIE7NY6W5KKveBu5wHt1H8GQxkZi9lGBQeVgyFWXoyw8nKKlVfvsfL6A1befMTK4Qwrb+fMn6jffRZ8yyxc49/j5w5n9F5wT7g3PAOedTDcQPNxnbD1vKeRqQudwIJpEiZLGI/hYFwBND6mswkX2B7106ltvwHDGJksu0FsAfbZWA4sast7HPwmhOM2YCCDw3EFKPDF52/hubKO24B5Jq4AquPhbPMf4bn2TtyjuALsnbhH/wWfKlUqlHj9BkQRtIh4vvG7AAAAAElFTkSuQmCC" height=30 width=30> Download Documents

After the envelope is created, the developer can retrieve a detailed response of the envelope and use the document_key to download the signed documents.

```console
from wesign_sdk.sdk import WesignSDK, DocumentExtractor

document_extractor = DocumentExtractor('https://api.wesign.com','<API KEY>', 'ID OF ENVELOPE')

print(document_extractor.envelope)
document_list = document_extractor.list_documents() 

<!-- returns the list of documents
[{
   'document_name' : "Name of the document",
   'is_attachment' : True/False, # Indicates whether its attached document or uploaded by creator.
    'document_key' : "unique key generated for document stored in secured File storage"
}] -->


document_extractor.download_documents('ABSOLUTE PATH TO FOLDER TO STORE FILES')
```


## License

`wesign-sdk` is distributed under the terms of the [MIT](https://spdx.org/licenses/MIT.html) license.
