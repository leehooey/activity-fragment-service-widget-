activity生命周期
 程序启动
 OnCreate     创建时调用
 OnStart       可见但没有焦点
 OnResume    可见并获取焦点
 程序进入运行状态
 Onpause     可见但失去焦点
 OnStop      不可见但存在于内存中
 OnDistroy    销毁
 程序销毁
用户点击返回键调用流程
onResume->onPause->onStop->onDistroy
用户点击home键
onCreate->onStart->onResume->onPause->onStop 该activity在内存中
点击hone键之后再启动应用
onStop--------->onRestart->onStart->onResume
MainActivity跳转到secondeActivity
Opause->onCreate->onStart()->onResume->onStop //opause尽量少做将耗时操作，将耗时操作放在onStop中，尽量早将secondActivity显示出来
当主activity跳转到secondActivity且secondActivity背景为透明
onCreate->onStart->onResume->onPause  主activity可见但没有焦点
从secondActivity返回主activity时
OnPause---->onResume

异常状态（如：旋转手机屏幕）onResume->onPause->onStop->onDistroy->onCreate->onStart->onResume  //activity销毁重建 销毁之前数据之前系统会调用方法onSaveInstanceStata()方法用来保存之前的数据，新建的activity可以通过onCreate()方法或重写onRestoreInstanceState()获取之前的数据，如果销毁前保存数据onRestoreInstanceStata()方法肯定调用不需要判断
activity节点设置android:configChanges=”orientation |screensize |keyboardHiddien”属性
当手机方向，屏幕尺寸，键盘隐藏显示都不会影响activity的生命周期 但是系统会调用onConfigurationChanged方法。








Service生命周期
服务启动
onCreate  //服务第一次开启时调用（只调用一次 ）
onStartCommand（代替onStart()，只被startService调用）
服务进入运行状态
onBind (bindService调用该方法)
onUnbind(unBindService调用，只能调用一次，不能多次解绑)
onDestroy
服务关闭
当服务第一次启动时调用onCreate方法和onStartCommand
如果用户调用bindService()则系统调用onBind
如果用户调用unBindService()则系统调用onUnbind
当服务没有关闭却在次点击启动按钮只执行onStartCommand方法
	
Widget(窗体小部件)
1.onReceive()//按接收到不同的广播类型执行下面不同的方法
2.onEnable()//创建第一个小部件的时候调用
3.onUpdate()//创建小部件的时候调用
4.onAppWidgetOptionsChanged()//小部件宽高发生改变时调用
5.onDelete()//删除小部件调用
6.onDisaable()//删除最后一个小部件的时候调用

Fragment生命周期

onAttach  依附在Activity上
onCreate
onCreateView  		加载布局显示Fragment内容
onActivityCreated   在onCreateView中初始化的view 完全初始化了 
onStart   		可见没焦点
onResume  	可见有焦点
onPause 		可见没焦点
onStop 		不可见没有焦点
onDestoryView 在onCreateView中创建的view销毁了
onDestory 
onDetach 取消依附	

点击home键 再次点击该应用
OnResume-->onPause-->onStop  -->onStart-->onResume //与activity的区别就是fragment没有onRestart方法
跳转至另一个fragment
该fragment彻底销毁且取消依附后启动另一个Fragment
点击返回键onResume->onPause->onStop->onDestoryView->onDestory->onDetach         
