# asmupdf
用于android中打开pdf文件。基于mupdf-1.6 版本进行编译打包成动态库（libmupdf.so),可以自己封装成 .jar,提供到各自的app中使用

#简介
基于mupdf-1.6 版本进行编译打包成动态库（libmupdf.so)<br>
动态库SO总大小9.4M对于能打开pdf的第三方库算是比较小的了<br>
Android Studio直接引入libaray库文件即可

#测试代码
引入libaray库之后测试代码如下
```Java
String pdfAbsPath = "pdf绝对路径";
Uri uri = Uri.parse(Uri.encode(pdfAbsPath));
Intent intent = new Intent(mContext, MuPDFActivity.class);
intent.setAction(Intent.ACTION_VIEW);
intent.setData(uri);
startActivityForResult(intent, 0);
```

#混淆代码
```Java
#mupdf MuPDFCore不混淆,native不混淆，
-keep public class com.mupdf.libaray.MuPDFCore{*;}
jni中调用java文件不混淆
-keep public class com.mupdf.libaray.OutlineItem{*;}
-keep public class com.mupdf.libaray.TextChar{*;}
-keep public class com.mupdf.libaray.LinkInfo{*;}
-keep public class com.mupdf.libaray.LinkInfoInternal{*;}
-keep public class com.mupdf.libaray.LinkInfoExternal{*;}
-keep public class com.mupdf.libaray.LinkInfoRemote{*;}
-keep public class com.mupdf.libaray.Annotation{*;}
-keep public class com.mupdf.libaray.MuPDFAlertInternal{*;}
```
