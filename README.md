# Facebook_JS_LoginSDK

## 創建屬於自己的FacebookAPI應用程式
首先進到Facebook的開發人員[網站](https://developers.facebook.com/)，點選右上角**我的應用程式**後點選**新增應用程式**
![image](https://github.com/WeiYun0912/Facebook_JS_LoginSDK/blob/master/images/FB_1.PNG)
<br>
於該視窗輸入自己要的名稱
## 設定 Facebook JavaScript SDK
Facebook JavaScript SDK 沒有任何需要下載或安裝的獨立檔案，<br>只需要將一小段一般的 JavaScript 置入 HTML 中，<br>就會以非同步的方式將 SDK 載入頁面中。<br>
**非同步載入是指不會阻擋頁面中其他元素的載入。**
<br><br>
以下程式碼片段會提供 Facebook JavaScript SDK 基本版，選項會設定為最常見的預設值。<br>在每一個要使用 Facebook 分析工具的頁面上，<br>
**將以下程式碼片段直接插入開頭的 <body> 標籤後方。以應用程式編號取代 {your-app-id}，<br>並以鎖定的 API 版本取代 {api-version}。目前的版本為v3.2。**
```js
<script>
  window.fbAsyncInit = function() {
    FB.init({
      appId      : '{你的應用程式id}',
      cookie     : true,
      xfbml      : true,
      version    : '{api的版本(目前最新是3.2)}'
    });
      
    FB.AppEvents.logPageView();   
      
  };

  (function(d, s, id){
     var js, fjs = d.getElementsByTagName(s)[0];
     if (d.getElementById(id)) {return;}
     js = d.createElement(s); js.id = id;
     js.src = "https://connect.facebook.net/en_US/sdk.js";
     fjs.parentNode.insertBefore(js, fjs);
   }(document, 'script', 'facebook-jssdk'));
</script>
```
