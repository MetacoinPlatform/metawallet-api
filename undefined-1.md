# 공통 파라미터

## 호출시 공통 파라미터

### appParamURL(string, 1\~256bytes)

* 이 파라미터가 사용되면 다른 모든 파라미터는 무시되며 이 파라미터에 명시된 URL의 반환값을 대신 파라미터로 이용하게 됩니다.
* 파라미터가 너무 길어서 QRCode로 만들었을때 인식하기 힘든경우 유용하게 사용됩니다.
* 이 파라미터의 반환값은 다음과 유사합니다.
  * &#x20;appAction=Login\&appName=TestApp

### `필수` appAction(string, 1\~32bytes)

* MetaWallet 에서 처리할 작업을 명시합니다.
* 각 작업별로 명시된 값을 사용합니다.

### appCallbackType(string, 아래 명시된 값 중 하나 혹은 빈 문자열)

* MetaWallet 에서 결과를 통보할때 사용할 방식을 지정합니다.
* 아래 명시된 값 이외의 값 중 하나가 사용되어야 합니다.
  * universallink
    * iOS가 아닌경우 무시되며, 오류가 발생됩니다.
    * 'callback' 파라미터의 값을 Apple Universal Link 값으로 이용하여 통보합니다.
  * url
    * Web, iOS, Android 가 아닌경우 무시되며, 오류가 발생됩니다.
    * 'callback' 파라미터의 값을 URL로 판단하여 결과를 POST 방식으로 통보합니다.
  * deeplink
    * Android 가 아닌경우 무시되며, 오류가 발생됩니다.
    * 파라미터의 값을 DeepLink 로 판단하여 결과를 전달합니다.
  * intent
    * Android 가 아닌경우 무시되며, 오류가 발생됩니다.
    * [setResult](https://developer.android.com/reference/android/app/Activity?hl=ko#setResult\(int,%20android.content.Intent\)) 를 이용하여 결과를 반환합니다.
  * 빈 문자열
    * iOS의 경우 universallink 로 설정한것과 동일합니다.
    * Android의 경우 intent 로 설정한것과 동일합니다.

### appCallback(string, 0\~255bytes)

* 결과값을 반환할때 사용할 식별자를 지정합니다.
* `callbackType` 값에 따라 각각 다음과 같은 형식이어야 합니다.
  * universallink
    * Apple Universal Link 에서 사용할 URL Scheme 값
  * url
    * 결과값을 GET으로 전달하며, http/https 프로토콜을 사용해야 합니다.
  * deeplink
    * Android 에서 사용할 URL Scheme 값
  * intent
    * 이 값은 무시됩니다.

### appReqKey(string, 0\~64 bytes)

* 결과를 수신했을때 자신이 호출한값인지 여부를 알기 위해 사용됩니다.
* 이 값은 생략될 수 있습니다.

### `필수` appName(string)

* Metawallet 에서 표기할 호출자의 명칭입니다

### appIcon(string, url 형식)

* Metawallet 에서 표기할 호출자의 이미지입니다.
* 명시되지 않는경우 기본 이미지가 표시됩니다.

### appTopic(string, 선택)

* Metawallet 에서 표기할 작업의 설명입니다.
* 작업에 따라 사용되지 않는경우도 있습니다.

### network(string, 아래에 명시된 값 중 하나)

* 메타코인 네트워크를 명시합니다
* 작업에 따라 사용되지 않는경우도 있습니다.
* 아래 명시된 값 이외의 값 중 하나가 사용되어야 합니다.
  * "0"
    * 사용자가 선택할 수 있도록 합니다.
    * 작업에 따라 사용할 수 없는 경우가 있습니다.
  * "1"
    * MainNet
  * "5"
    * TestNet

## 응답시 공통 파라미터

### code(string, 4bytes)

* 결과 값에 대한 성공/실패/취소 여부를 의미합니다.
* 아래 명시된 값 이외의 값은 해당 API의 설명에 따릅니다.
  * 0000: 성공
  * 9999: 취소

### acion&#x20;

* appAction 에 명시된 값을 반환합니다.&#x20;
* 이것은 여러번 지갑을 호출한경우 어떤 호출에 대한 응답인지 식별하는데 사용됩니다.

### message(string, 0\~255 bytes)

* 성공시 빈 문자열이 반환됩니다.
* 실패시 오류 메시지를 반환합니다.

### appReqKey(string)

* 결과를 수신했을때 자신이 호출한값인지 여부를 알기 위해 사용됩니다.
* 호출시 넘겨준 appReqKey 의 값이 그대로 반환 됩니다.

### network(string, 1byte)

* 메타코인 네트워크를 명시합니다
* 아래 명시된 값 이외의 값 중 하나 입니다.
  * "1"
    * MainNet
  * "5"
    * TestNet

### networkName(string)

* 메타코인 네트워크 이름을 반환합니다.
* 아래 명시된 값 이외의 값 중 하나 입니다.
  * MainNet
  * TestNet

### txid(string)

* Metacoin Network 에서 밯생된 Transaction ID 입니다.
* 작업에따라 빈 값이 반환될 수 있습니다.

### data(string)

* 작업에 따라 요청한 값이 설정됩니다.
