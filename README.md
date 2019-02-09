# Facebook_JS_LoginSDK

## 創建屬於自己的FacebookAPI應用程式
首先進到Facebook的開發人員[網站](https://developers.facebook.com/)，點選右上角**我的應用程式**後點選**新增應用程式**
<br><br>
![image](https://github.com/WeiYun0912/Facebook_JS_LoginSDK/blob/master/images/FB_1.PNG)
<br><br>
於該視窗輸入自己要的名稱
<br><br>
![image](https://github.com/WeiYun0912/Facebook_JS_LoginSDK/blob/master/images/FB_3.PNG)
<br><br>
因 **同源政策 (Same-origin policy)** 的關係我們需要修改應用程式網域為localhost(本機測試)
<br><br>
![image](https://github.com/WeiYun0912/Facebook_JS_LoginSDK/blob/master/images/FB_5.PNG)

接著跟著圖片的順序操作點選
<br><br>
![image](https://github.com/WeiYun0912/Facebook_JS_LoginSDK/blob/master/images/FB_4.PNG)
## 設定 Facebook JavaScript SDK
Facebook JavaScript SDK 沒有任何需要下載或安裝的獨立檔案，<br>只需要將一小段一般的 JavaScript 置入 HTML 中，<br>就會以非同步的方式將 SDK 載入頁面中。<br>
**非同步載入是指不會阻擋頁面中其他元素的載入。**
<br><br>
以下程式碼片段會提供 Facebook JavaScript SDK 基本版，選項會設定為最常見的預設值。<br>在每一個要使用 Facebook 分析工具的頁面上，<br>
**將以下程式碼片段直接插入開頭的 <body> 標籤後方。以應用程式編號取代 {your-app-id}，<br>並以鎖定的 API 版本取代 {api-version}。目前的版本為v3.2。**
```js
<script>
  window.fbAsyncInit = function() {
  //初始化FB JS SDK
    FB.init({
      appId      : '{你的應用程式id}',
      cookie     : true,
      xfbml      : true,
      version    : '{api的版本(目前最新是3.2)}'
    });
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

## 確認登入狀態
載入網頁時，首先要確認此用戶是否已經使用「Facebook 登入」來登入，<br>
所以我們可以在初始化SDK時加上這段程式碼：
```js
FB.getLoginStatus(function(response) {
  console.log(response); //
});
```
getLoginStatus顧名思義就是取得目前用戶的登入狀態而這裡回傳的response物件含有數個欄位<br>
```js
{
    status: 'connected',
    authResponse: {
        accessToken: '...',
        expiresIn:'...',
        signedRequest:'...',
        userID:'...'
    }
}
```
status 代表此用戶目前的登入狀態。狀態可能為以下其中一項：
1. connected - 這位用戶已登入 Facebook，也已經登入您的應用程式。<br>
2. not_authorized - 這位用戶已登入 Facebook，但尚未登入您的應用程式。<br>
3. unknown - 這位用戶沒有登入 Facebook，因此您無法得知用戶是否已登入您的應用程式，或者之前已呼叫 <br>
FB.logout()，因此無法連結至 Facebook。
<br>
如果狀態是 connected，就會包含 authResponse，且由以下資料所構成：<br>
1. accessToken - 含有這位應用程式用戶的存取權杖。<br>
2. expiresIn - 以 UNIX 時間顯示權杖何時到期並需要再次更新。<br>
3. signedRequest - 已簽署的參數，其中包含這位應用程式用戶的資訊。<br>
4. userID - 這位應用程式用戶的編號。<br>
