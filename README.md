What is Response for SureForms?
===============================

  
A web-hook sender and rest API receiver to display responses to queries via an
Automaton of choice with options to display below the form (No SureTriggers
needed)

Response for Sure Forms Documentation
-------------------------------------

This documentation is for response for SureForms it is tested up to 1.0.4 and is
designed to work with the repository version of
[SureForms](https://wordpress.org/plugins/sureforms/), it has been designed and
tested using Flowmattic although there is no reason it shouldn’t work with any
system that has the ability to receive web-hook responses and issue a JSON
response to an api via post.

 

Setup
-----

 

**Installation:**

-   Download Latest release

    -   Upload Latest Version

    -   Activate

**Using Response for sure forms :**

Navigate to Tools----\> Hooksure

![](https://github.com/stingray82/repo-images/raw/main/Hooksure/Menu.png)

 

**Settings Page:**

 

![](https://github.com/stingray82/repo-images/raw/main/Hooksure/Hooksure-Settings.png)

To add a form you will add a form ID in (1) and a Webhook Url (2) and click
(save (3)

You can delete a hook by finding it in the settings and hitting delete (4)

 

**Form Edits if you want a response**

 

You also need to modify your sure form to work with Response navigate to your
choose form and click edit, you need to select general and navigate to form
confirmation.

![](https://github.com/stingray82/repo-images/raw/main/response-for-sureforms/part1-editform-general-form-confirmation.png)

On the next screen you need to select hooksure response

 

 

 

![](https://github.com/stingray82/repo-images/raw/main/response-for-sureforms/part-2-hooksure-response.png)

and once done you should auto-select the below form option

 

![](https://github.com/stingray82/repo-images/raw/main/response-for-sureforms/part-3-hooksure-response-below-form.png)

You then need to exit out and save your form.

 

Your form is now setup for sending to and receiving a response back to the
chosen form, you also have the option to send only by not doing the form edits!

 

Web hook Response Information
=============================

 

Overview
--------

This documentation outlines the options available for the Response for Sure
Forms. It covers all the required parameters, their default behavior, optional
configurations, and how they can be used together to customize the response.

 

Form Submission
---------------

A return URL is submitted with the web-hook response which also includes the
session_id and the form_id you will need all three of these plus your message to
return a working message

 

Required Parameters
-------------------

These parameters must be included in the POST request for the webhook to work.

| Parameter    | Description                                                                  | Required |
|--------------|------------------------------------------------------------------------------|----------|
| `session_id` | A unique identifier for the session.                                         | Yes      |
| `form_id`    | The unique identifier for the form.                                          | Yes      |
| `body`       | Only Required if no other parameters are set this can be normal text or html | Yes      |

Optional Parameters
-------------------

The following parameters are optional but can be used to customize the response:

| Parameter          | Default Value | Description                                                                                                            |
|--------------------|---------------|------------------------------------------------------------------------------------------------------------------------|
| `body_display`     | `"yes"`       | Determines whether the body content is shown. `"yes"` will show it, `"no"` hides the body and shows a default message. |
| `link_url`         | N/A           | A clickable link passed as an anchor tag (`<a>`).                                                                      |
| `custom_link_text` | N/A           | Custom text for the link. If provided, replaces the default "Visit Link" text with the custom version                  |
| `copy_button`      | `"no"`        | If `"yes"`, a copy button will be displayed allowing users to copy the body content of **body** to the clipboard.      |
| `image_url`        | N/A           | HTML code for an image to be displayed. Passed as an object with the `html` property. (This should be the url)         |
| `pdf_url`          | N/A           | Should contain the URL of the PDF document to be displayed                                                             |
| `has_link`         | `"no"`        | If `"yes"`, a link will be displayed. Default is `"no"`, meaning no link will be shown unless specified.               |
| `has_image`        | `"no"`        | If `"yes"`, an image will be displayed. Default is `"no"`, meaning no image will be shown unless specified.            |
| `has_pdf`          | `"no"`        | If `"yes"`, a PDF link or embedded PDF will be displayed. Default is `"no"`.                                           |

Example Use Cases
-----------------

Default Example
---------------

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ json
{
  "session_id": "example_session_id",
  "form_id": "7",
  "body_display": "yes",
  "copy_button": "yes",
  "body": "Your Body Text Here",
}
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Example 1: Display Link (default Visit Link)
--------------------------------------------

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ json
{
  "session_id": "example_session_id",
  "form_id": "7",
  "body_display": "no",
  "link_url": "https://example.com",
  "has_link": "yes"
}
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Example 2: Display PDF
----------------------

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ json
{
  "session_id": "example_session_id",
  "form_id": "7",
  "body_display": "no",
  "pdf_url": "https://example.com/sample.pdf",
  "has_pdf": "yes"
}
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Example 3: Display link with Custom Link Text
---------------------------------------------

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ json
{
  "session_id": "example_session_id",
  "form_id": "7",
  "body_display": "no",
  "link_url": "https://example.com/sample.jpg",
  "custom_link_text": "Click here to view image",
  "has_link": "yes"
}
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Example 4: Display Image
------------------------

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ json
{
  "session_id": "example_session_id",
  "form_id": "7",
  "body_display": "no",
  "image_url": "https://example.com/sample.jpeg",
  "has_image": "yes"
}
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
