#Ptr Comparizon
目前仅比对github上star数>1500的下拉刷新开源库，在比较完成之后可能会加入其它有代表性的库.

##Repo
|Repo|Owner|Star (up to2015.12.5)|SanpShot|
|:--:|:--:|:------:|:---:|:--:|
|[Android-PullToRefresh][3]<br/>(已停止维护)|[chrisbanes][4]|6014|![chrisbanes](/demo_gif/chrisbanes.gif)|
|[android-Ultra-Pull-To-Refresh][1]|[liaohuqiu][2]|3413|![liaohuqiu](/demo_gif/liaohuqiu.gif)|
|[android-pulltorefresh][5]<br/>(已停止维护)|[johannilsson][6]|2414|![johannilsson](/demo_gif/johan.gif)|
|[Phoenix][7]|[Yalantis][8]|1897|![yalantis](/demo_gif/yalantis.gif)|
|[FlyRefresh][9]|[race604][10]|1843|![flyrefresh](/demo_gif/flyrefresh.gif)|

##拓展性

|Repo|自定义顶部视图|支持的内容布局|
|:--:|:--:|:--:|:---:|:--:|:--:|
|[Android-PullToRefresh][3]|不支持，只能改代码。<br/>由于仅支持其中实现的`LoadingLayout`作为顶视图，改代码实现自定义工作量较大。|任意视图，内置:`GridView`<br/>`ListView`,`HorizontalScrollView`<br/> `ScrollView` ,`WebView`|
|[android-Ultra-Pull-To-Refresh][1]|任意视图。<br/> 通过继承`PtrUIHandler`并调用<br/>`PtrFrameLayout.addPtrUIHandler()`得到最大支持。|任意视图||
|[android-pulltorefresh][5]|不支持，只能改代码。<br/> 代码仅一个`ListView`，耦合度太高，改动工作量较大。|无法扩展，自身为`ListView`|
|[Phoenix][7]|不支持，此控件特点就是顶部视图及动画。|任意视图|
|[FlyRefresh][9]|不支持，此控件特点就是顶部视图及动画。|任意视图|

##易用性

|Repo|gradle配置|上拉加载|自动加载|滑动阻尼配置|
|:--:|:--:|:------:|:---:|:--:|:--:|:--:|
|[Android-PullToRefresh][3]|×|√|×|
|[android-Ultra-Pull-To-Refresh][1]|√|×|√|√|
|[android-pulltorefresh][5]|×|×|×|
|[Phoenix][7]|√|×|×|
|[FlyRefresh][9]|√|×|×|

##性能分析

通过捕捉如下图中的操作持续1秒钟的systrace进行性能分析：

![trace_operation](trace_operation.gif)

> 注：由于开源库Header大多无法直接放自定义视图，头部视图复杂程度不同，数据对比结果会有所偏差。

###1. Chris Banes's Ptr

滑动实现方式：`View.post(Runnable)` + `View.scrollTo()` 

trace snapshot:

![trace_chrisbanes](/traces/chrisbanes.PNG)

###2. liaohuqiu's Ptr

滑动实现方式：`Scroller` + `View.post(Runnable)` + `View.offsetTopAndBottom()`

trace snapshot:

![trace_liaohuqiu](/traces/liaohuqiu.PNG)

###3. johannilsson's Ptr

滑动实现方式：`View.setPadding()`

trace snapshot:

![trace_johan](/traces/johan.PNG)

###4. Yalantis's Ptr

滑动实现方式：`Animation` + `View.topAndBottomOffset()`

trace snapshot:

![trace_yalantis](/traces/yalantis.PNG)

###5. race604's Ptr

滑动实现方式：`NestedScrollingChildHelper.dispatchNestedScroll()`

trace snapshot:

![trace_flyrefresh](/traces/flyrefresh.PNG)

[1]: https://github.com/liaohuqiu/android-Ultra-Pull-To-Refresh
[2]: https://github.com/liaohuqiu
[3]: https://github.com/chrisbanes/Android-PullToRefresh
[4]: https://github.com/chrisbanes
[5]: https://github.com/johannilsson/android-pulltorefresh
[6]: https://github.com/johannilsson
[7]: https://github.com/Yalantis/Phoenix
[8]: https://github.com/Yalantis
[9]: https://github.com/race604/FlyRefresh
[10]: https://github.com/race604