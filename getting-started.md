---

copyright:
  years: 2015, 2018
lastupdated: "2018-04-27"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:curl: #curl .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}

# Getting started tutorial

This tutorial guides you through how to use some built-in classifiers in {{site.data.keyword.visualrecognitionfull}} to classify an image and then detect faces in an image.
{: shortdesc}

## Before you begin
{: #prerequisites}

- Create an instance of the service:
    1.  Go to the [{{site.data.keyword.visualrecognitionshort}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.{DomainName}/catalog/services/visual-recognition){: new_window} page in the {{site.data.keyword.Bluemix_notm}} Catalog.
    1.  Sign up for a free {{site.data.keyword.Bluemix_notm}} account or log in.
    1.  Click **Create**.
- Copy the credentials to authenticate to your service instance:
    1.  Click **Show** to view your credentials.
    1.  Copy the apikey value.


## Step 1: Classify an image
{: #classify}

1.  Download the sample <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/fruitbowl.jpg" download="fruitbowl.jpg">fruitbowl.jpg <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a> image.
1.  Issue the following command to upload the image and classify it against all built-in classifiers:
    - Replace `{your_api_key}` with the service credentials you copied earlier.
    - Modify the location of the images\_file to point to where you saved the image.

    ```bash
    curl -X POST -u "apikey:{your_api_key}" --form "images_file=@fruitbowl.jpg" \
    "https://gateway.watsonplatform.net/visual-recognition/api/v3/classify?version=2018-03-19"
    ```
    {: pre}

    If you have {{site.data.keyword.Bluemix_notm}} Dedicated, the `gateway.watsonplatform.net` endpoint here might not be your service endpoint. Check the `url` on the **Service credentials** page of your service dashboard.
    {: tip}

    The response includes the General model or classifier (which uses the `default` classifier_id), the classes identified in the image, and a score for each class.

    ```json
    {
      "images": [
        {
          "classifiers": [
            {
              "classifier_id": "default",
              "name": "default",
              "classes": [
                {
                  "class": "banana",
                  "score": 0.562,
                  "type_hierarchy": "/fruit/banana"
                },
                {
                  "class": "fruit",
                  "score": 0.788
                },
                {
                  "class": "diet (food)",
                  "score": 0.528,
                  "type_hierarchy": "/food/diet (food)"
                },
                {
                  "class": "food",
                  "score": 0.528
                },
                {
                  "class": "honeydew",
                  "score": 0.5,
                  "type_hierarchy": "/fruit/melon/honeydew"
                },
                {
                  "class": "melon",
                  "score": 0.501
                },
                {
                  "class": "olive color",
                  "score": 0.973
                },
                {
                  "class": "lemon yellow color",
                  "score": 0.789
                }
              ]
            }
          ],
          "image": "fruitbowl.jpg"
        }
      ],
      "images_processed": 1,
      "custom_classes": 0
    }
    ```
    {: codeblock}

    Confidence scores are in the range of 0 to 1, with a higher score indicating greater correlation. By default, the `/v3/classify` calls don't include classes with a score below `0.5`.

## Step 2: Detect faces in an image
{: #detect-faces}

{{site.data.keyword.visualrecognitionshort}} can detect faces in images. The response provides information such as the location of the face in the image and the estimated age range and gender for each face.

1.  Download the sample <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/visual-recognition/Ginni_Rometty_at_the_Fortune_MPW_Summit_in_2011.jpg" download="">Ginni_Rometty.jpg <img src="../../icons/launch-glyph.svg" alt="External link icon" title="External link icon" class="style-scope doc-content"></a> image.
1.  Issue the following command to the `POST /v3/detect_faces` method to upload and analyze the image. If you use your own image, the maximum size is 10 MB:
    - Replace `{your_api_key}` with the service credentials you copied earlier.
    - Modify the location of the images\_file to point to where you saved the image.

    ```bash
    curl -X POST -u "apikey:{your_api_key}" --form "images_file=@Ginni_Rometty.jpg" \
    "https://gateway.watsonplatform.net/visual-recognition/api/v3/detect_faces?version=2018-03-19"
    ```
    {: pre}

    The response includes a location and age and gender estimates with scores.

    Scores range from 0-1, with a higher score indicating greater correlation.

    ```json
    {
      "images": [
        {
          "faces": [
            {
              "age": {
                "min": 50,
                "max": 53,
                "score": 0.33788413
              },
              "face_location": {
                "height": 744,
                "width": 606,
                "left": 460,
                "top": 373
              },
              "gender": {
                "gender": "FEMALE",
                "score": 0.9999988
              }
            }
          ],
          "image": "Ginni_Rometty.jpg"
        }
      ],
      "images_processed": 1
    }
    ```
    {: codeblock}

## Next steps

You have a basic understanding of how to use the built-in default classifier with {{site.data.keyword.visualrecognitionshort}}. Now dive deeper:

- Learn more about how to [build a custom classifier](/docs/services/visual-recognition/tutorial-custom-classifier.html).
- Read about the API in the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/visual-recognition/api/v3/){: new_window}.

### Attributions
{: #attributions}

- [Fruit basket ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://flic.kr/p/JPHES){: new_window} by Flikr user [Ryan Edwards-Crewe ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.flickr.com/photos/ryanec/){: new_window} used under [Creative Commons Attribution 2.0 license ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://creativecommons.org/licenses/by/2.0/deed.en){: new_window}. No changes were made to this image.
- [Ginni Rometty at the Fortune MPW Summit in 2011 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://commons.wikimedia.org/wiki/File:Ginni_Rometty_at_the_Fortune_MPW_Summit_in_2011.jpg){: new_window} by Asa Mathat / Fortune Live Media used under [CC BY 2.0 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://creativecommons.org/licenses/by/2.0/legalcode){: new_window}.  No changes were made to this image.
