# 广播机制

## Android中的广播分为两种类型：标准广播，有序广播。

## 接收系统广播

广播接收器可以自由的对自己感兴趣的广播进行注册，这样当有相应的广播发出时，广播接收器就能够接收到该广播，并在内部处理相应的逻辑，注册广播的方式一般有两种，在代码中注册和AndroidManifest.xml中注册，前者是动态注册，后者是静态注册。

### 动态注册监听网络变化

动态创建一个类，继承自BroadcastReceiver，并重写父类的onReceive方法，这样当有广播到来时，onReceive方法就会被执行。

```java
public class MainActivity extends AppCompatActivity {

    private IntentFilter intentFilter;
    private NetworkChangeReceiver networkChangeReceiver;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        intentFilter = new IntentFilter();
        intentFilter.addAction("android.net.conn.CONNECTIVITY_CHANGE");
        networkChangeReceiver = new NetworkChangeReceiver();
        registerReceiver(networkChangeReceiver, intentFilter);
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        unregisterReceiver(networkChangeReceiver);
    }

    class NetworkChangeReceiver extends BroadcastReceiver {
        @Override
        public void onReceive(Context context, Intent intent) {
            Toast.makeText(context, "network changes", Toast.LENGTH_SHORT).show();
        }
    }
}
```

在onCreate中，首先创建一个IntentFilter的实例，并给它添加一个值为android.net.conn.CONNECTIVITY_CHANGE的action，当网络发生变化时，系统发出一条android.net.conn.CONNECTIVITY_CHANGE的广播，也就是说我们的广播器想要监听什么广播，就在这里添加相应的action

### 静态注册实现开机启动

动态注册缺点必须要在程序启动之后才能接收到广播。

准备让程序接收一条开机广播，当收到这条广播时就可以在onReceive方法里执行相应的逻辑，从而实现开机启动，右击com.example.broadcasttest包->New->Other->Broadcast Receiver,会弹一个框，Exported属性表示是否允许这个广播接收器接收本程序以外的广播，Enabled属性表示是否启用这个广播接收器

然后修改BootCompleteReceiver中的代码：

```java
public class BootCompleteReceiver extends BroadcastReceiver {

    @Override
    public void onReceive(Context context, Intent intent) {
        // TODO: This method is called when the BroadcastReceiver is receiving
        // an Intent broadcast.
        Toast.makeText(context, "Boot Complete", Toast.LENGTH_SHORT).show();
    }
}
```
在AndroidManifest.xml中修改：

```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.broadcasttest">
    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        <receiver
            android:name=".BootCompleteReceiver"
            android:enabled="true"
            android:exported="true">
            <intent-filter>
                <action android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
            </intent-filter>
        </receiver>

        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```

## 链接

- [目录](directory.md)
- 上一部分：[活动](activity.md)
- 下一部分：[持久化](store.md)
