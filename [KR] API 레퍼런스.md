## 📂 Project Title 
**[KR] 객체 검출 API 레퍼런스**

## 💼 Context
이 문서는 객체 검출 API를 위해 마크다운(Markdown) 형식으로 작성된 API 레퍼런스입니다.

------------
# 객체 검출 API (Object Detection API)
사용자가 업로드한 이미지 파일을 분석해 이미지 내 특정 객체를 검출하고 위치를 반환하는 API입니다.

## 요청 파라미터 (Request Parameters)
헤더 또는 바디에 토큰을 포함하며, 전송 데이터는 아래의 구조를 따릅니다.

| 필드명 | 타입 | 필수 여부| 설명|
| :----: | :----: | :----:| :----|
| `access_token`|String|Y|API 인증을 위한 액세스 토큰|
|`request_data`|Object|Y|요청 데이터 본문 객체|
| ↳`image_format`| String | Y | 이미지 파일의 확장자(`jpg`, `jpeg`, `png`) |
| ↳`base64_source`| String | Y | 이미지를 Base64 문자열로 인코딩한 텍스트 데이터|
|↳`options`|Object|Y|API 검출 필터링 옵션 객체
|↳↳ `confidence_threshold`|Double|Y| 검출 신뢰도 하한선 예) `0.75`지정 시 75% 이상만 반환|
|↳↳ `target_objects`|List|Y|탐지할 사물 목록 제한 예) `["person", "car", "bicycle"]`|

## 응답 데이터 (Response)

### 1. 성공 시 (Success Response)
| JSON Key 명 | 타입 | 설명 | 예시 |
| :-----: | :-----: | :----- | :----- |
|`status`| String | API 처리 상태 결과 | `"success"`|
|`timestamp`|String |API 요청 처리 시각(ISO 8601 형식)|`"2026-06-23T14:18:40Z"`|
|`data`|Object|검출 결과 데이터 객체| |
|↳`detected_count`|Integer|검출된 총 객체의 수|`2`|
|↳`objects`|List|검출된 객체 정보 리스트| |
|↳↳`label`|String|검출된 객체의 명칭|`"person"`|
|↳↳`confidence`|Double|검출 결과 신뢰도|`0.92`|
|↳↳`bounding_box`|Object|객체를 둘러싼 경계 상자의 위치 정보, 기준점(0.0): 좌측 상단 모서리| |
|↳↳↳`x`|Integer|박스의 좌측 상단 X 좌표값(단위:px)|`120`|
|↳↳↳`y`|Integer|박스의 좌측 상단 Y 좌표값(단위:px)|`85`|
|↳↳↳`width`|Integer|박스의 가로 길이(단위:px)|`50`|
|↳↳↳`height`|Integer|박스의 세로 길이(단위:px)|`120`|

### 2. 실패 시 (Error Response)
객체 검출이 제대로 이루어지지 않았을 경우에는 객체 인식 결과 대신 오류 메시지가 반환됩니다.
|JSON Key|오류 메시지|설명|
|-----|-----|:-----|
|`error_01`|`"File type not allowed"`|지원하지 않는 파일 확장자일 경우|
|`error_02`|`"Object detection failed"`| 지원하는 이미지 파일 확장자이지만, 목표 객체 리스트에 지정된 객체가 포함되지 않아 객체를 검출할 수 없을 경우 |

## 응답 JSON 구현 예제 (Response JSON Example)
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
```
