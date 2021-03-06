# Android-Widget 理解 
![](https://developer.android.com/images/appwidgets/appwidget.png)
<br>一個應用程式的小窗口，可以依附在其他應用程式 (桌面)，圖中為音樂撥放器的小元件

## Google play store 上相關推薦 Widget
https://www.newmobilelife.com/2016/03/18/8-android-widget/

## 基本必要配置
- AppWidgetProviderInfo - 為 App Widget 所需要的 metadata ， 以及相關畫面 layout 的設置 xml
- AppWidgetProvider - 拿來寫 App Widget 用的 class ，他的基底是 broadcast events，所以透過廣播收到 App Widget 的各種事件
- View layout - 除了 metadata ，詳細 View 內容的配置 xml

- **[AppWidgetHost](https://developer.android.com/guide/topics/appwidgets/host.html) - 實際控制 App Widgets 的地方， Widget 必須要依附一個應用程式，無法單獨存在，如果程式要被依附需要使用這個(手機桌面就有)**
> Thanks: http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2017/0417/7838.html

## 手把手 widget 影片
> 以下為 Android studio 手把手使用模板產生 widget
> <br>https://www.youtube.com/watch?v=5BzYH6Vq6ZU

## 使用 AppWidgetProvider 來操作 App Widget 的各種事件
<br>(很像 Activity 生命週期)
 - onEnabled(Context) - 只有第一次添加上了 Widget 才會被 call ，之後加了兩次三次，不會再呼叫。(很像 Activity 的 onCreate)
 - onUpdate() - 依據 metadata 設定的 updatePeriodMillis 定時 call 此 method，就像平常使用 event handler 操作 view
 - onDeleted() - Widget 每次移除一次就會 call 一次
 - onDisabled(Context) - 最後一次 Widget 被移除的時候 call ，適合結束掉一些 work 或是清除 database
 - onReceive(Context, Intent) - 樓上每個 call back 都會 call 一次 (非必要 implement)
 - onAppWidgetOptionsChanged() - 每當 widget 在重新定義大小時會被 call
 
## 支援的 view
因為 App Widget 是透過 RemoteView 來做跨進程(ex. 桌面程式 <-> 自己的 App )的傳遞，並非所有view都適用，以下是支援的 view
> FrameLayout<br>
> LinearLayout<br>
> RelativeLayout<br>
> GridLayout<br>

> AnalogClock - https://www.mkyong.com/android/android-analogclock-and-digitalclock-example/<br>
> Button <br>
> Chronometer - http://androidbiancheng.blogspot.tw/2011/04/android-chronometer.html<br>
> ImageButton <br>
> ImageView <br>
> ProgressBar<br>
> TextView<br>
> ViewFlipper - https://www.youtube.com/watch?v=k_Y4OGL8DTA<br>
> ListView<br>
> GridView<br>
> StackView - http://www.thaicreate.com/mobile/android-stackview.html<br>
> AdapterViewFlipper - https://www.jianshu.com/p/6d616dce99d9<br>

- RemoteViews 特別也支持 ViewStub ， 可以一開始讓 view 為隱藏，晚一點在 inflate
## 參考
<br>https://developer.android.com/guide/topics/appwidgets/index.html#AppWidgetProvider
<br>http://blog.csdn.net/u012792686/article/details/73810655
<br>http://glgjing.github.io/blog/2015/11/05/android-kai-fa-zhi-app-widget-xiang-jie/
<br>http://blog.csdn.net/u012792686/article/details/73604254

# Floating View
另一個較多彈性的 view，只要在 WindowManager.addView 即可，像是 FB chat 那樣漂浮在畫面最頂層，不像 App Widget 限定特定 view
<br>教學連結：https://www.androidhive.info/2016/11/android-floating-widget-like-facebook-chat-head/
> 問題1.Android 6 權限問題 https://www.jianshu.com/p/2746a627c6d2
> <br>問題2.Android 8 Service限制 可能用 JobScheduler 取代（尚未試過） https://developer.android.com/reference/android/app/job/JobScheduler.html?hl=zh-cn

