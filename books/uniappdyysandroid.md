#### uni-app调用原生Android
``` java
 //获取宿主上下文
				  var main = plus.android.runtimeMainActivity();
				   //通过反射获取Android的Intent对象
				  var Intent = plus.android.importClass("android.content.Intent");
				  //通过宿主上下文创建 intent
				  var intent = new Intent(main.getIntent());
				  //设置要开启的Activity包类路径  com.HBuilder.integrate.MainActivity换掉你自己的界面
				  intent.setClassName(main, "chenziji.top.demo01.MainActivity");
				  //开启新的任务栈 （跨进程）
				  intent.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
				  //向原生界面传值操作
				  intent.putExtra("uni_key","来自uniapp的值");
				  //开启新的界面
				  main.startActivity(intent);
```

https://blog.csdn.net/qq_28461727/article/details/109049499