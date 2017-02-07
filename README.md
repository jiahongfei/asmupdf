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


#ABOUT

MuPDF is a lightweight PDF, XPS, EPUB and CBZ viewer and parser/rendering
library.

The renderer in MuPDF is tailored for high quality anti-aliased graphics. It
renders text with metrics and spacing accurate to within fractions of a pixel
for the highest fidelity in reproducing the look of a printed page on screen.

MuPDF is also small, fast, and yet complete. We support PDF 1.7 with
transparency, encryption, hyperlinks, annotations, search and many other bells
and whistles. MuPDF can also read XPS documents (OpenXPS / ECMA-388),
EPUB and CBZ (Comic Book archive) files.

MuPDF is written to be both modular and portable; the example applications
are merely thin layers on top of the functionality offered by the library,
so custom viewers can be easily built for a wide range of platforms. Example
viewer applications are supplied for Windows, Linux, MacOS, iOS and Android.

MuPDF is deliberately designed to be threading library agnostic, while still
supporting multi-threaded operation. In the absence of a thread library
it will run single-threaded, but by adding one significant benefits in
rendering speed on multi-core platforms can be obtained.

Interactive features such as form filling, javascript and transitions
are in development and partially supported by the Android application.

LICENSE

MuPDF is Copyright 2006-2015 Artifex Software, Inc.

This program is free software: you can redistribute it and/or modify it under
the terms of the GNU Affero General Public License as published by the Free
Software Foundation, either version 3 of the License, or (at your option) any
later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY
WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A
PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU Affero General Public License along
with this program. If not, see <http://www.gnu.org/licenses/>.

For commercial licensing, including our "Indie Dev" friendly options,
please contact sales@artifex.com.

COMPILING

If you are compiling from source you will need several third party libraries:
freetype2, jbig2dec, libjpeg, openjpeg, and zlib. These libraries are contained
in the source archive. If you are using git, they are included as git
submodules.

You will also need the X11 headers and libraries if you're building on Linux.
These can typically be found in the xorg-dev package. Alternatively, if you
only want the command line tools, you can build with HAVE_X11=no.

The new OpenGL-based viewer also needs OpenGL headers and libraries. If you're
building on Linux, install the mesa-common-dev and libgl1-mesa-dev packages.
You'll also need several X11 development packages: xorg-dev, libxcursor-dev,
libxrandr-dev, and libxinerama-dev. To skip building the OpenGL viewer, build
with HAVE_GLFW=no.

DOWNLOAD

The latest development source is available directly from the git repository:

	git clone http://mupdf.com/repos/mupdf.git

In the mupdf directory, update the third party libraries:

	git submodule update --init

INSTALLING (UNIX)

Typing "make prefix=/usr/local install" will install the binaries, man-pages,
static libraries and header files on your system.

REPORTING BUGS AND PROBLEMS

The MuPDF developers hang out on IRC in the #ghostscript channel on
irc.freenode.net.

Report bugs on the ghostscript bugzilla, with MuPDF as the selected component.

	http://bugs.ghostscript.com/

If you are reporting a problem with PDF parsing, please include the problematic
file as an attachment.
