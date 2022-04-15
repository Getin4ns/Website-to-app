# Website-to-app
Convert a responsive website into an android app/

Website to App Solution

Step 1: The first step is to take a responsive website that you want to convert in android app important point to note is that it should be a responsive(mobile friendly) website.


Step 2: Create a new project in Android Studio and name it WebViewApp.

Step 3: Open res -> layout -> activity_main.xml (or) main.xml, create the application interface and add webview element to it.

CODE:

_______________________________________________________________________________________________________________________________________________________________________

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
   android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    tools:context="com.example.webviewapp.MainActivity">
 
 <WebView
        android:id="@+id/webview"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
</RelativeLayout>

_______________________________________________________________________________________________________________________________________________________________________

Step 4: Open src -> package -> MainActivity.java. Here firstly declare a webview variable, make JavaScript enable and load the URL of the website. See the whole code below.

Important Note: You can replace our url in below code with any other url you want to convert it into Android App.

CODE:

_______________________________________________________________________________________________________________________________________________________________________
package com.example.webviewapp;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
        import android.webkit.WebSettings;
        import android.webkit.WebView;
        import android.webkit.WebViewClient;

public class MainActivity extends AppCompatActivity {
    private WebView mywebView;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        mywebView = (WebView) findViewById(R.id.webview);
        WebSettings webSettings= mywebView.getSettings();
        webSettings.setJavaScriptEnabled(true);
        mywebView.loadUrl("https://domain_name/");
    }
}
_______________________________________________________________________________________________________________________________________________________________________

Step 5: Open AndroidManifest.xml file and add internet permission to it just after the package name. It is required because the App will load data directly from the website.

CODE:

_______________________________________________________________________________________________________________________________________________________________________

<uses-permission android:name="android.permission.INTERNET"></uses-permission>

_______________________________________________________________________________________________________________________________________________________________________

Step 6: After adding the permissions the application is complete but when you run you will find that it will open the links in browser not in application itself. Solution for this is add this line of code in your MainActivity.java class.

CODE:

_______________________________________________________________________________________________________________________________________________________________________

 mywebView.setWebViewClient(new WebViewClient());

_______________________________________________________________________________________________________________________________________________________________________

Step 7: Now to add back buttons to the application to need to add following code to your MainActivity.java class.

CODE:

_______________________________________________________________________________________________________________________________________________________________________

  public void onBackPressed() {
        if(mywebView.canGoBack())
        {
            mywebView.goBack();
        }

        else{
            super.onBackPressed();
        }
    }
_______________________________________________________________________________________________________________________________________________________________________

Step 8: Further if you want to remove the additional padding in the app, open activity_main.xml and in the layouts remove the padding(bottom, top, right, left). Here’s the final code.
activity_main.xml

CODE:

_______________________________________________________________________________________________________________________________________________________________________

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.example.webviewapp.MainActivity">

// WebView Element
    <WebView
        android:id="@+id/webview"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
</RelativeLayout>

_______________________________________________________________________________________________________________________________________________________________________

MainActivity.java complete code:

_______________________________________________________________________________________________________________________________________________________________________

package com.example.webviewapp;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.webkit.WebSettings;
import android.webkit.WebView;
import android.webkit.WebViewClient;

public class MainActivity extends AppCompatActivity {
    private WebView mywebView;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        mywebView = (WebView) findViewById(R.id.webview);
        WebSettings webSettings= mywebView.getSettings();
        webSettings.setJavaScriptEnabled(true);
        mywebView.loadUrl("https://domain_name");
        // Line of Code for opening links in app
        mywebView.setWebViewClient(new WebViewClient());
    }
    
//Code For Back Button
@Override
    public void onBackPressed() {
        if(mywebView.canGoBack())
        {
            mywebView.goBack();
        }

        else
        {
            super.onBackPressed();
        }
    }
}

_______________________________________________________________________________________________________________________________________________________________________

Bonus Tip For WebView App: In addition if you want to remove the default action bar, see in image the blue top header. You just need to make a little change in styles.xml file.

app -> res -> values -> styles.xml
Just change theme as NoActionBar. Below code will do

CODE:

_______________________________________________________________________________________________________________________________________________________________________

<style name=”AppTheme” parent=”Theme.AppCompat.Light.NoActionBar”>

_______________________________________________________________________________________________________________________________________________________________________

Output:
Now run the App and you will see WebView App of your website. You can simply replace the url with any website url you want to convert into Android App.

Hope this is useful.
