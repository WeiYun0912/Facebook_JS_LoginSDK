# Facebook_JS_LoginSDK

## 設定 Facebook JavaScript SDK
Facebook JavaScript SDK 沒有任何需要下載或安裝的獨立檔案，<br>只需要將一小段一般的 JavaScript 置入 HTML 中，<br>就會以非同步的方式將 SDK 載入頁面中。
**非同步載入是指不會阻擋頁面中其他元素的載入。**

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
