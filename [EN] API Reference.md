## 📂 Project Title 
**[EN] Object Detection API Reference**

## 💼 Context
This is an API reference sample created for an object detection API, written in Markdown.

---------

# Object Detection API

This API analyzes image files uploaded by the user to detect specific objects and provide object coordinates.

## Request Parameters
Request must include a token in its header or body, and the transmitted data must follow the structure below.

| Field | Type | Required (Y/N) | Description |
| :----: | :----: | :----:| :---- |
| `access_token`|String|Y| Access token for API verification|
|`request_data`|Object|Y| Request data body |
| ↳`image_format`| String | Y | Extension of image file (`jpg`, `jpeg`, `png`) |
| ↳`base64_source`| String | Y | Base 64-encoded image data |
|↳`options`|Object|Y| API detection filtering option |
|↳↳ `confidence_threshold`|Double|Y| Required minimum confidence score (ex. input `0.75` -> only return results with a minimum of 75% confidence) |
|↳↳ `target_objects`|List|Y|A list of targeted objects for detection (ex.`["person", "car", "bicycle"]`) |

## Response

### 1. Success Response
| JSON Key | Type | Description | Examples |
| :-----: | :-----: | :----- | :----- |
|`status`| String | API process status report | `"success"`|
|`timestamp`|String | Process timestamp for API request (ISO 8601 format)|`"2026-06-23T14:18:40Z"`|
|`data`|Object| Detection result data object | |
|↳`detected_count`|Integer| Total number of detected objects |`2`|
|↳`objects`|List| Information list of detected objects | |
|↳↳`label`|String| Name of detected object |`"person"`|
|↳↳`confidence`|Double| Confidence score of result |`0.92`|
|↳↳`bounding_box`|Object| Coordinate information of boundary box surrounding the object; `origin (0.0): top left corner` | |
|↳↳↳`x`|Integer| X coordinate of box's upper left vertex (unit:px) |`120`|
|↳↳↳`y`|Integer| Y coordinate of box's upper left vertex (unit:px) |`85`|
|↳↳↳`width`|Integer| box width (unit:px)|`50`|
|↳↳↳`height`|Integer| box height (unit:px)|`120`|

 

### 2. Error Response
If object detection fails, an error message will be returned in place of detection results.

|JSON Key|Error Message|Description|
|-----|-----|:-----|
|`error_01`|`"File type not allowed"`| API does not support the image extension |
|`error_02`|`"Object detection failed"`| API does support image extension, but the image does not include any detectable objects from the target object list |

## Response JSON Example
```
{
  "status": "success",
  "timestamp": "2026-06-23T14:18:40Z",
  "data": {
    "detected_count": 2,
    "objects": [
      {
        "label": "person",
        "confidence": 0.92,
        "bounding_box": {
          "x": 120,
          "y": 85,
          "width": 50,
          "height": 120
        }
      },
      {
        "label": "car",
        "confidence": 0.84,
        "bounding_box": {
          "x": 340,
          "y": 200,
          "width": 180,
          "height": 95
        }
      }
    ]
  }
}
``
