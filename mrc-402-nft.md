# MRC-402(NFT)

## 이체

### Query Parameters

* `필수` appAction : mrc402Transfer
* `필수` appName : [링크 참조](undefined-1.md#appname-string)
* `필수` appCallbackType : [링크 참조](undefined-1.md#appcallbacktype-string)
* `필수` appCallback : [링크 참조](undefined-1.md#appcallback-string-0-255bytes)
* appReqKey : [요청 식별값](undefined-1.md#appreqkey-string-0-64-bytes)
* appIcon : [링크 참조](undefined-1.md#appicon-string-url)
* network : [링크 참조](undefined-1.md#network-string)
* `필수` amount : 문자열, 이체 금액
* `필수` mrc402id : MRC402 ID
* `필수` address : 토큰을 이체 받을 주소
* tag : 수취인 측에서 사용자를 식별하기 위한 TAG 값
* memo : 이체 건에 대한 메모

### Response

* `필수` appReqKey : 링크 참조
* `필수` code : 0000(성공), 9999(취소), 0001\~9998(오류)
* `필수` message : 성공시 빈 문자열, 실패시 오류 메시지
* `필수` network : 1(Mainnet) or 5(TestNet)
* `필수` txid : 작업이 수행된 Transaction ID

## 발행

{% hint style="info" %}
발행된 MRC402는 생성자의 지갑에 추가됩니다.
{% endhint %}

{% hint style="warning" %}
초기 생성 금액이 있는경우 지정된 금액만큼 생성자의 지갑에서 차감됩니다.
{% endhint %}

### Query Parameters

* `필수` appAction : mrc402Create
* `필수` appName : [링크 참조](undefined-1.md#appname-string)
* `필수` appCallbackType : [링크 참조](undefined-1.md#appcallbacktype-string)
* `필수` appCallback : [링크 참조](undefined-1.md#appcallback-string-0-255bytes)
* appReqKey : [요청 식별값](undefined-1.md#appreqkey-string-0-64-bytes)
* appIcon : [링크 참조](undefined-1.md#appicon-string-url)
* network : [링크 참조](undefined-1.md#network-string)
* `필수` creator : 생성자의 주소, 사용자가 해당 주소에 접근할 권한이 없는경우 오류 발생, 생략시 사용자가 주소를 선택할 수 있음.
* `필수` name : 토큰 이름
* `필수` creatorcommition : 경매, 판매시 생성자가 받을 수수료 비율(0.00\~10.00%) 숫자, 소수점 2자리
* `필수` totalSupply : 총 발행량(정수)
* `필수` decimal : 최대 소수점 자리수(현재 정책상 0 으로 입력할것)
* `필수` url : 토큰 프로젝트 홈페이지 주소
* `필수` imageUrl : 토큰 이미지 url
* `필수` copyrighterholder : 저작권자의 메타코인 주소 및 경매, 판매시 생성자가 받을 수수료 비율(0.00\~10.00%) 숫자, 소수점 2자리
  * 최대 5개의 주소를 지정할 수 있음.
  * 지정하지 않는경우 빈 문자열 입력&#x20;

```json
{"MT....":"5", "MT....":"7.5"} // { Address : Commition ratio, ... }
```

* `필수` initialreserve : 토큰 1개당 사용할 초기 설정 금액\
  지정하지 않는경우 빈 문자열 입력 \~\~\~json // token id : amount&#x20;

```json
{"0":"5", "5":"7.5"} // { Token ID : Amount, ... }
```

* `필수` expiredate : Melting 가능한일시, 설정하지 않을경우 0 으로 입력
* data : Application 에서 활용할 Data
* info : NFT에 대한 설명 Markdown 형태로 서술할것
* socialmedia : SNS 링크

```json
{"twitter":"htts://www.twitter.com/metacoin", 
"Home Page" : "http://...."} // { ID : URL, ... }
```

### Response

* `필수` appReqKey : 링크 참조
* `필수` code : 0000(성공), 9999(취소), 0001\~9998(오류)
* `필수` message : 성공시 빈 문자열, 실패시 오류 메시지
* `필수` network : 1(Mainnet) or 5(TestNet)
* `필수` txid : 작업이 수행된 Transaction ID
* `필수` data : 성공시 생성된 MRC402 ID, 실패시 빈 문자열

## 정보 변경

> 명시된 수량만큼 MRC010 생성자의 지갑에서 차감합니다.
>
> 총 발행 수량역시 차감됩니다.

### Query Parameters

* `필수` appAction : mrc402Update
* `필수` appName : [링크 참조](undefined-1.md#appname-string)
* `필수` appCallbackType : [링크 참조](undefined-1.md#appcallbacktype-string)
* `필수` appCallback : [링크 참조](undefined-1.md#appcallback-string-0-255bytes)
* appReqKey : [요청 식별값](undefined-1.md#appreqkey-string-0-64-bytes)
* appIcon : [링크 참조](undefined-1.md#appicon-string-url)
* network : [링크 참조](undefined-1.md#network-string)
* `필수` creator : 생성자의 주소, 사용자가 해당 주소에 접근할 권한이 없는경우 오류 발생, 생략시 사용자가 주소를 선택할 수 있음.
* `필수` mrc402id : MRC402 ID
* `필수` url : 토큰 프로젝트 홈페이지 주소
* data : Application 에서 활용할 Data
* info : NFT에 대한 설명 Markdown 형태로 서술할것
* socialmedia : SNS 링크 \~\~\~json // token id : amount {"twitter":"htts://www.twitter.com/metacoin", "Home Page" : "http://...."} \~\~\~

### Response

* `필수` appReqKey : 링크 참조
* `필수` code : 0000(성공), 9999(취소), 0001\~9998(오류)
* `필수` message : 성공시 빈 문자열, 실패시 오류 메시지
* `필수` network : 1(Mainnet) or 5(TestNet)
* `필수` txid : 작업이 수행된 Transaction ID

## 추가 발행

{% hint style="info" %}
추가 발행된 수량만큼 MRC402 생성자의 MRC402 잔액이 증가됩니다.

토큰 정보의 총 발행 수량도 증가됩니다.
{% endhint %}

{% hint style="warning" %}
초기 생성 금액이 있는경우 해당 금액만큼 생성자의 지갑에서 차감됩니다.
{% endhint %}

### Query Parameters

* `필수` appAction : mrc402Mint
* `필수` appName : [링크 참조](undefined-1.md#appname-string)
* `필수` appCallbackType : [링크 참조](undefined-1.md#appcallbacktype-string)
* `필수` appCallback : [링크 참조](undefined-1.md#appcallback-string-0-255bytes)
* appReqKey : [요청 식별값](undefined-1.md#appreqkey-string-0-64-bytes)
* appIcon : [링크 참조](undefined-1.md#appicon-string-url)
* network : [링크 참조](undefined-1.md#network-string)
* `필수` owner : 생성자의 주소, 사용자가 해당 주소에 접근할 권한이 없는경우 오류 발생, 생략시 사용자가 주소를 선택할 수 있음.
* `필수` token : 토큰 ID
* `필수` amount : 추가 발행할 수량

### Response

* `필수` appReqKey : 링크 참조
* `필수` code : 0000(성공), 9999(취소), 0001\~9998(오류)
* `필수` message : 성공시 빈 문자열, 실패시 오류 메시지
* `필수` network : 1(Mainnet) or 5(TestNet)
* `필수` txid : 작업이 수행된 Transaction ID

## 소각

{% hint style="warning" %}
명시된 수량만큼 MRC402 생성자의 지갑에서 차감합니다.
{% endhint %}

{% hint style="info" %}
총 발행 수량이 감소됩니다.

초기 생성 금액이 있는경우 해당 금액만큼 생성자의 지갑에 추가됩니다.
{% endhint %}

### Query Parameters

* `필수` appAction : mrc402Burn
* `필수` appName : [링크 참조](undefined-1.md#appname-string)
* `필수` appCallbackType : [링크 참조](undefined-1.md#appcallbacktype-string)
* `필수` appCallback : [링크 참조](undefined-1.md#appcallback-string-0-255bytes)
* appReqKey : [요청 식별값](undefined-1.md#appreqkey-string-0-64-bytes)
* appIcon : [링크 참조](undefined-1.md#appicon-string-url)
* network : [링크 참조](undefined-1.md#network-string)
* `필수` owner : 생성자의 주소, 사용자가 해당 주소에 접근할 권한이 없는경우 오류 발생, 생략시 사용자가 주소를 선택할 수 있음.
* `필수` token : 토큰 ID
* `필수` amount : 추가 발행할 수량

### Response

* `필수` appReqKey : 링크 참조
* `필수` code : 0000(성공), 9999(취소), 0001\~9998(오류)
* `필수` message : 성공시 빈 문자열, 실패시 오류 메시지
* `필수` network : 1(Mainnet) or 5(TestNet)
* `필수` txid : 작업이 수행된 Transaction ID

## 경매 등록

### Query Parameters

* `필수` appAction : mrc402Auction
* `필수` appName : [링크 참조](undefined-1.md#appname-string)
* `필수` appCallbackType : [링크 참조](undefined-1.md#appcallbacktype-string)
* `필수` appCallback : [링크 참조](undefined-1.md#appcallback-string-0-255bytes)
* appReqKey : [요청 식별값](undefined-1.md#appreqkey-string-0-64-bytes)
* appIcon : [링크 참조](undefined-1.md#appicon-string-url)
* network : [링크 참조](undefined-1.md#network-string)
* `필수` id :  경매에 등록하려는 MRC402 ID
* `필수` amount : 문자열, 경매로 판매할 수량
* `필수` token : 경매시 입찰 가능한 토큰 ID
* `필수` auction\_start\_price : 경매 시작 금액
* `필수` auction\_bidding\_unit : 경매 입찰 단위
* `필수` auction\_buynow\_price : 즉시 구매가격
* `필수` auction\_start\_date : 경매 시작 일시(EPOCH Time), 서버에 등록되는 시점\~7일 이내
* `필수` auction\_end\_date : 경매 시작 일시(EPOCH Time), 경매 시작시점으로부터 1시간\~7일 이내
* platform\_address : 거래 체결시 수수료를 받을 거래 플렛폼의 메타코인 주소
* platform\_commission : 거래 체결시 거래 플렛폼이 받을 수수료의 비율(% 단위)
* platform\_name : 거래 플렛폼 이름
* platform\_url : 거래 플렛폼 url

### Response

* `필수` appReqKey : 링크 참조
* `필수` code : 0000(성공), 9999(취소), 0001\~9998(오류)
* `필수` message : 성공시 빈 문자열, 실패시 오류 메시지
* `필수` network : 1(Mainnet) or 5(TestNet)
* `필수` txid : 작업이 수행된 Transaction ID
* `필수` data : MRC402DEX ID

## 경매 등록 취소

### Query Parameters

* `필수` appAction : mrc402UnAuction
* `필수` appName : [링크 참조](undefined-1.md#appname-string)
* `필수` appCallbackType : [링크 참조](undefined-1.md#appcallbacktype-string)
* `필수` appCallback : [링크 참조](undefined-1.md#appcallback-string-0-255bytes)
* appReqKey : [요청 식별값](undefined-1.md#appreqkey-string-0-64-bytes)
* appIcon : [링크 참조](undefined-1.md#appicon-string-url)
* network : [링크 참조](undefined-1.md#network-string)
* `필수` id : MRC402 DEX ID

### Response

* `필수` appReqKey : 링크 참조
* `필수` code : 0000(성공), 9999(취소), 0001\~9998(오류)
* `필수` message : 성공시 빈 문자열, 실패시 오류 메시지
* `필수` network : 1(Mainnet) or 5(TestNet)
* `필수` txid : 작업이 수행된 Transaction ID

## 경매 입찰

### Query Parameters

* `필수` appAction : mrc402AuctionBid
* `필수` appName : [링크 참조](undefined-1.md#appname-string)
* `필수` appCallbackType : [링크 참조](undefined-1.md#appcallbacktype-string)
* `필수` appCallback : [링크 참조](undefined-1.md#appcallback-string-0-255bytes)
* appReqKey : [요청 식별값](undefined-1.md#appreqkey-string-0-64-bytes)
* appIcon : [링크 참조](undefined-1.md#appicon-string-url)
* network : [링크 참조](undefined-1.md#network-string)
* `필수` amount : 경매로 입찰 금
* `필수` token : MRC 402 ID

### Response

* `필수` appReqKey : 링크 참조
* `필수` code : 0000(성공), 9999(취소), 0001\~9998(오류)
* `필수` message : 성공시 빈 문자열, 실패시 오류 메시지
* `필수` network : 1(Mainnet) or 5(TestNet)
* `필수` txid : 작업이 수행된 Transaction ID



## 판매 등록

### Query Parameters

* `필수` appAction : mrc402Sell
* `필수` appName : [링크 참조](undefined-1.md#appname-string)
* `필수` appCallbackType : [링크 참조](undefined-1.md#appcallbacktype-string)
* `필수` appCallback : [링크 참조](undefined-1.md#appcallback-string-0-255bytes)
* appReqKey : [요청 식별값](undefined-1.md#appreqkey-string-0-64-bytes)
* appIcon : [링크 참조](undefined-1.md#appicon-string-url)
* network : [링크 참조](undefined-1.md#network-string)
* `필수` id : 판매 하려는 MRC402 ID
* `필수` amount : 경매 입찰 금액
* `필수` token : 구매시 지불 가능한 토큰 ID
* `필수` price : 1개당 판매 금액
* platform\_address : 거래 체결시 수수료를 받을 거래 플렛폼의 메타코인 주소
* platform\_commission : 거래 체결시 거래 플렛폼이 받을 수수료의 비율(% 단위)
* platform\_name : 거래 플렛폼 이름
* platform\_url : 거래 플렛폼 url

### Response

* `필수` appReqKey : 링크 참조
* `필수` code : 0000(성공), 9999(취소), 0001\~9998(오류)
* `필수` message : 성공시 빈 문자열, 실패시 오류 메시지
* `필수` network : 1(Mainnet) or 5(TestNet)
* `필수` txid : 작업이 수행된 Transaction ID



## 판매 취소

### Query Parameters

* `필수` appAction : mrc402Unsell
* `필수` appName : [링크 참조](undefined-1.md#appname-string)
* `필수` appCallbackType : [링크 참조](undefined-1.md#appcallbacktype-string)
* `필수` appCallback : [링크 참조](undefined-1.md#appcallback-string-0-255bytes)
* appReqKey : [요청 식별값](undefined-1.md#appreqkey-string-0-64-bytes)
* appIcon : [링크 참조](undefined-1.md#appicon-string-url)
* network : [링크 참조](undefined-1.md#network-string)
* `필수` id : MRC402 DEX ID

### Response

* `필수` appReqKey : 링크 참조
* `필수` code : 0000(성공), 9999(취소), 0001\~9998(오류)
* `필수` message : 성공시 빈 문자열, 실패시 오류 메시지
* `필수` network : 1(Mainnet) or 5(TestNet)
* `필수` txid : 작업이 수행된 Transaction ID



## 구매

### Query Parameters

* `필수` appAction : mrc402Buy
* `필수` appName : [링크 참조](undefined-1.md#appname-string)
* `필수` appCallbackType : [링크 참조](undefined-1.md#appcallbacktype-string)
* `필수` appCallback : [링크 참조](undefined-1.md#appcallback-string-0-255bytes)
* appReqKey : [요청 식별값](undefined-1.md#appreqkey-string-0-64-bytes)
* appIcon : [링크 참조](undefined-1.md#appicon-string-url)
* network : [링크 참조](undefined-1.md#network-string)
* `필수` amount : 문자열, 구매 수량
* `필수` id : MRC 402 ID

### Response

* `필수` appReqKey : 링크 참조
* `필수` code : 0000(성공), 9999(취소), 0001\~9998(오류)
* `필수` message : 성공시 빈 문자열, 실패시 오류 메시지
* `필수` network : 1(Mainnet) or 5(TestNet)
* `필수` txid : 작업이 수행된 Transaction ID
