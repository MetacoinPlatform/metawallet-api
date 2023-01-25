# 일반 함수

## Login

앱 & 사이트 에서 사용자 식별을 위하여 사용자가 선택한 주소를 반환함.

### Query Parameters

* `필수` appAction : login
* `필수` appName : 링크 참조
* `필수` appCallbackType : 링크 참조
* `필수` appCallback : 링크 참조
* appReqKey : 요청 식별값
* appIcon : 링크 참조
* network : 링크 참조

### Response

#### 성공

* `필수` appReqKey : 링크 참조
* `필수` code : 0000(성공), 9999(취소), 0001\~9998(오류)
* `필수` message : 성공시 빈 문자열, 실패시 오류 메시지
* `필수` network : 1(Mainnet) or 5(TestNet)
* `필수` data : 성공시 선택된 주소, 실패시 빈 문자열
* `필수` name : 성공시 선택된 주소의 명칭, 실패시 빈 문자열
* `필수` timestamp : 서버 시간
* `필수` sign: address + "|" + timestamp 를 RSA 로 서명한값. 사전에 제공된 공개키로 서명이 올바른지 확인하여야함.

#### 실패(아래 문서 참조)

{% content-ref url="undefined-1.md" %}
[undefined-1.md](undefined-1.md)
{% endcontent-ref %}

### Example

{% tabs %}
{% tab title="Android(Java)" %}
{% code overflow="wrap" lineNumbers="true" %}
```java
public class LoginTest {
    protected ActivityResultLauncher<Intent>
        mStartForResult = registerForActivityResult(new ActivityResultContracts.StartActivityForResult(), result -> {
        int i = result.getResultCode();
        if (i == Activity.RESULT_OK) {
            Intent intent = result.getData();
            if (intent == null) {
                return;
            }
            Bundle bundle = intent.getExtras();
            String code = bundle.getString("code", "");
            switch (code) {
                case "0000":
                    bindingResult.viResult.setText(R.string.success);
                    break;
                case "9999":
                    bindingResult.viResult.setText(R.string.cancel_by_user);
                    break;
                default:
                    bindingResult.viResult.setText(R.string.error);
                    break;
            }
            bindingResult.viResultCode.setText(code);
            bindingResult.viResultMessage.setText(bundle.getString("message", ""));
            bindingResult.viResultTXID.setText(bundle.getString("txid", ""));
        } else if (i == Activity.RESULT_CANCELED) {
            bindingResult.viResult.setText(R.string.cancel_by_user);
            bindingResult.viResultCode.setText("");
            bindingResult.viResultMessage.setText("");
            bindingResult.viResultTXID.setText("");
        }
    });
    
    public void doLogin(){
        Uri params = Uri.parse("metawallet://co.inblock");
        Intent intent = new Intent(Intent.ACTION_VIEW, params);
        intent.setFlags(Intent.FLAG_ACTIVITY_SINGLE_TOP);
        intent.putExtra("appCction", "login");
        intent.putExtra("appReqKey", "REQUEST_KEY");
        intent.putExtra("network", "1");
        intent.putExtra("appUrl", "https://www.example.com");
        intent.putExtra("appIcon", "https://www.example.com/images/icon.png");
        intent.putExtra("appName", "Example");
        intent.putExtra("appCallbankType", "intent");
        mStartForResult.launch(intent);
    }
}

```
{% endcode %}
{% endtab %}

{% tab title="iOS(Swift)" %}
{% code overflow="wrap" lineNumbers="true" %}
```swift
// Call MetaWallet
var requestComponents: URLComponents = URLComponents()
requestComponents.scheme = "metawallet://"
requestComponents.host = "co.inblock"
requestComponents.queryItems = [
    URLQueryItem(name: "appReqKey", value: topic),
    URLQueryItem(name: "appName", value: appName ?? name),
    URLQueryItem(name: "appAction", value: "connect")
    URLQueryItem(name: "appIcons", value: iconUrl!)
    URLQueryItem(name: "appCallbackType", value: "universallink")
    URLQueryItem(name: "appCallback", value: "smapleapp://metawallet")
]

if UIApplication.shared.canOpenURL(requestComponents.url) {
    UIApplication.shared.open(url, options: [.universalLinksOnly:true]){ isSuccess in
        if isSuccess {
            // Success 
        } else {
            // failed open app
        }
    }
}

//
// ==================================
//

// Result Process 

// SceneDelegate.swift
func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
    guard let _ = (scene as? UIWindowScene) else { return }

    if let userActivity = connectionOptions.userActivities.first {
        self.scene(scene, continue: userActivity)
    }
}

func scene(_ scene: UIScene, continue userActivity: NSUserActivity) {
    if let url = userActivity.webpageURL {
        if url.host == nil || url.scheme == nil {
            return
        }

        if url.host != "smapleapp" {
            return
        }
        
        guard let param = url.parameters else {
            return
        }
        
        if let reqKey = param["reqKey"] as? String {
            if !RequestQueue.shared.pop(key: reqKey) {
                return
            }
        
            let notificationName = NSNotification.Name(rawValue: reqKey)
            NotificationCenter.default.post(name: notificationName, object: param)
            
            return true
        }
    }    
}

```
{% endcode %}
{% endtab %}

{% tab title="HTML(Mobule Web)" %}
{% code overflow="wrap" lineNumbers="true" %}
```html
<a href="metawallet://co.inblock?
    ?appCction=connect
    &appReqKey=REQUEST_KEY
    &appUrl=https://wallet.metacoin.network
    &name=샘플사이트
    &icons=https://wallet.metacoin.network/favicon.png
    &callbackType=url
    &callback=https://wallet.metacoin.network/app/callback">
    Click to Metawallet Link</a>
```
{% endcode %}
{% endtab %}
{% endtabs %}
