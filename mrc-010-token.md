# MRC-010(Token)

## 이체

#### Query Parameters

* `필수` appAction : transfer
* `필수` appName : [링크 참조](undefined-1.md#appname-string)
* `필수` appCallbackType : [링크 참조](undefined-1.md#appcallbacktype-string)
* `필수` appCallback : [링크 참조](undefined-1.md#appcallback-string-0-255bytes)
* appReqKey : [요청 식별값](undefined-1.md#appreqkey-string-0-64-bytes)
* appIcon : [링크 참조](undefined-1.md#appicon-string-url)
* network : [링크 참조](undefined-1.md#network-string)
* `필수` amount : 문자열, 이체 금액
* `필수` tokenId : 이체할 토큰의 고유 ID
* `필수` address : 토큰을 이체 받을 주소
* tag : 수취인 측에서 사용자를 식별하기 위한 TAG 값
* memo : 이체 건에 대한 메모

#### Response

* `필수` appReqKey : 링크 참조
* `필수` code : 0000(성공), 9999(취소), 0001\~9998(오류)
* `필수` message : 성공시 빈 문자열, 실패시 오류 메시지
* `필수` network : 1(Mainnet) or 5(TestNet)
* `필수` txid : 작업이 수행된 Transaction ID

## 생성

#### Query Parameters

* `필수` appAction :  mrc010Create
* `필수` appName : [링크 참조](undefined-1.md#appname-string)
* `필수` appCallbackType : [링크 참조](undefined-1.md#appcallbacktype-string)
* `필수` appCallback : [링크 참조](undefined-1.md#appcallback-string-0-255bytes)
* appReqKey : [요청 식별값](undefined-1.md#appreqkey-string-0-64-bytes)
* appIcon : [링크 참조](undefined-1.md#appicon-string-url)
* network : [링크 참조](undefined-1.md#network-string)

***

* owner : 생성자의 주소, 사용자가 해당 주소에 접근할 권한이 없는경우 오류 발생, 생략시 사용자가 주소를 선택할 수 있음.
* `필수` name : 토큰 이름
* `필수` symbol : 토큰 심볼
* `필수` decimal : 최대 소수점 자리수
* `필수` totalSupply : 총 발행량
* `필수` imageUrl : 토큰 이미지 url
* `필수` url : 토큰 프로젝트 홈페이지 주소
* information : 토큰에 대한 설명

#### Response

* `필수` appReqKey : 링크 참조
* `필수` code : 0000(성공), 9999(취소), 0001\~9998(오류)
* `필수` message : 성공시 빈 문자열, 실패시 오류 메시지
* `필수` network : 1(Mainnet) or 5(TestNet)
* `필수` txid : 작업이 수행된 Transaction ID

## 정보 변경

#### Query Parameters

* `필수` appAction : mrc010Update
* `필수` appName : [링크 참조](undefined-1.md#appname-string)
* `필수` appCallbackType : [링크 참조](undefined-1.md#appcallbacktype-string)
* `필수` appCallback : [링크 참조](undefined-1.md#appcallback-string-0-255bytes)
* appReqKey : [요청 식별값](undefined-1.md#appreqkey-string-0-64-bytes)
* appIcon : [링크 참조](undefined-1.md#appicon-string-url)
* network : [링크 참조](undefined-1.md#network-string)

***

* `필수` owner : 생성자의 주소, 사용자가 해당 주소에 접근할 권한이 없는경우 오류 발생, 생략시 사용자가 주소를 선택할 수 있음.
* `필수` token : 토큰 ID
* `필수` imageUrl : 토큰 이미지 url
* `필수` url : 토큰 프로젝트 홈페이지 주소
* `필수` information : 토큰에 대한 설명

#### Response

* `필수` appReqKey : 링크 참조
* `필수` code : 0000(성공), 9999(취소), 0001\~9998(오류)
* `필수` message : 성공시 빈 문자열, 실패시 오류 메시지
* `필수` network : 1(Mainnet) or 5(TestNet)
* `필수` txid : 작업이 수행된 Transaction ID

## 추가 발행

{% hint style="info" %}
명시된 수량만큼 MRC010 생성자의 지갑에 입됩니다.

토큰정보의 총 발행 수량도 증가됩니다.
{% endhint %}

#### Query Parameters(공통)

* `필수` appAction : mrc010Mint
* `필수` appName : [링크 참조](undefined-1.md#appname-string)
* `필수` appCallbackType : [링크 참조](undefined-1.md#appcallbacktype-string)
* `필수` appCallback : [링크 참조](undefined-1.md#appcallback-string-0-255bytes)
* appReqKey : [요청 식별값](undefined-1.md#appreqkey-string-0-64-bytes)
* appIcon : [링크 참조](undefined-1.md#appicon-string-url)
* network : [링크 참조](undefined-1.md#network-string)

***

* `필수` owner : 생성자의 주소, 사용자가 해당 주소에 접근할 권한이 없는경우 오류 발생, 생략시 사용자가 주소를 선택할 수 있음.
* `필수` token : 토큰 ID
* `필수` amount : 추가 발행할 수량

#### Response

* `필수` appReqKey : 링크 참조
* `필수` code : 0000(성공), 9999(취소), 0001\~9998(오류)
* `필수` message : 성공시 빈 문자열, 실패시 오류 메시지
* `필수` network : 1(Mainnet) or 5(TestNet)
* `필수` txid : 작업이 수행된 Transaction ID

## 소각

{% hint style="danger" %}
명시된 수량만큼 MRC010 생성자의 지갑에서 차감합니다.

총 발행 수량역시 차감됩니다.
{% endhint %}

#### Query Parameters(공통)

* `필수` appAction : mrc010Burn
* `필수` appName : [링크 참조](undefined-1.md#appname-string)
* `필수` appCallbackType : [링크 참조](undefined-1.md#appcallbacktype-string)
* `필수` appCallback : [링크 참조](undefined-1.md#appcallback-string-0-255bytes)
* appReqKey : [요청 식별값](undefined-1.md#appreqkey-string-0-64-bytes)
* appIcon : [링크 참조](undefined-1.md#appicon-string-url)
* network : [링크 참조](undefined-1.md#network-string)

***

* `필수` owner : 생성자의 주소, 사용자가 해당 주소에 접근할 권한이 없는경우 오류 발생, 생략시 사용자가 주소를 선택할 수 있음.
* `필수` token : 토큰 ID
* `필수` amount : 추가 발행할 수량

#### Response

* `필수` appReqKey : 링크 참조
* `필수` code : 0000(성공), 9999(취소), 0001\~9998(오류)
* `필수` message : 성공시 빈 문자열, 실패시 오류 메시지
* `필수` network : 1(Mainnet) or 5(TestNet)
* `필수` txid : 작업이 수행된 Transaction ID



## 판매(MRC010 DEX) 등록

#### Query Parameters

* `필수` appAction : mrc010Sell
* `필수` appName : 링크 참조
* `필수` appCallbackType : 링크 참조
* `필수` appCallback : 링크 참조
* appReqKey : 요청 식별값
* appIcon : 링크 참조
* network : 링크 참조
* `필수` id : 판매 하려는 mrc010(토큰) ID
* `필수` amount : 경매 입찰 금액
* `필수` token : 구매시 지불 가능한 토큰 ID
* `필수` price : 1개당 판매 금액
* platform\_address : 거래 체결시 수수료를 받을 거래 플렛폼의 메타코인 주소
* platform\_commission : 거래 체결시 거래 플렛폼이 받을 수수료의 비율(% 단위)
* platform\_name : 거래 플렛폼 이름
* platform\_url : 거래 플렛폼 url
* min\_trade\_unit : 최소 거래 수량, 구매시 수량은 이 값의 배수 이어야 함

#### Response

* `필수` appReqKey : 링크 참조
* `필수` code : 0000(성공), 9999(취소), 0001\~9998(오류)
* `필수` message : 성공시 빈 문자열, 실패시 오류 메시지
* `필수` network : 1(Mainnet) or 5(TestNet)
* `필수` txid : 작업이 수행된 Transaction ID

## 판매 취소

#### Query Parameters

* `필수` appAction : mrc010Unsell
* `필수` appName : 링크 참조
* `필수` appCallbackType : 링크 참조
* `필수` appCallback : 링크 참조
* appReqKey : 요청 식별값
* appIcon : 링크 참조
* network : 링크 참조
* `필수` id : mrc010 DEX ID

#### Response

* `필수` appReqKey : 링크 참조
* `필수` code : 0000(성공), 9999(취소), 0001\~9998(오류)
* `필수` message : 성공시 빈 문자열, 실패시 오류 메시지
* `필수` network : 1(Mainnet) or 5(TestNet)
* `필수` txid : 작업이 수행된 Transaction ID

## 구매

#### Query Parameters

* `필수` appAction : mrc010Buy
* `필수` appName : 링크 참조
* `필수` appCallbackType : 링크 참조
* `필수` appCallback : 링크 참조
* appReqKey : 요청 식별값
* appIcon : 링크 참조
* network : 링크 참조
* `필수` amount : 문자열, 구매 수량
* `필수` id : MRC 010 DEX ID

#### Response

* `필수` appReqKey : 링크 참조
* `필수` code : 0000(성공), 9999(취소), 0001\~9998(오류)
* `필수` message : 성공시 빈 문자열, 실패시 오류 메시지
* `필수` network : 1(Mainnet) or 5(TestNet)
* `필수` txid : 작업이 수행된 Transaction ID
