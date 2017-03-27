# AndroidMinV9EmojiIssue
Shows an issue with EMOJI consuming from a `string` resource when min-sdk is 9.

This project has two modules:
1) a single Activity
2) a single layout
3) Two `TextView` - one has the text "Hello World", the other has 😀 (more precisely, `&#128512;`) referenced via `@string/emoji_text`.
4) Do not use support library, or any other library.
5) Uses the latest build tools and latest stable plugin.

They differ in two details:
1) the application id is different: `com.example.menny.emojitest` and `com.example.menny.emojitestV9`
2) the `minSdkVersion` value is different: `com.example.menny.emojitest` = 7, `com.example.menny.emojitestV9` = 9

If you run the first (`com.example.menny.emojitest`), it works fine and render the text and emoji.
If you run the second (`com.example.menny.emojitestV9`), the app crashes with:
```
I/ActivityManager( 1246): Start proc com.example.menny.emojitestV9 for activity com.example.menny.emojitestV9/.MainActivity: pid=1896 uid=10035 gids={}
W/dalvikvm( 1896): JNI WARNING: illegal start byte 0xf0
W/dalvikvm( 1896):              string: '😀'
W/dalvikvm( 1896):              in Landroid/content/res/StringBlock;.nativeGetString (II)Ljava/lang/String; (NewStringUTF)
I/dalvikvm( 1896): "main" prio=5 tid=1 NATIVE
I/dalvikvm( 1896):   | group="main" sCount=0 dsCount=0 obj=0xb1803c38 self=0x83a6e48
I/dalvikvm( 1896):   | sysTid=1896 nice=0 sched=0/0 cgrp=[fopen-error:2] handle=-2145907712
I/dalvikvm( 1896):   at android.content.res.StringBlock.nativeGetString(Native Method)
I/dalvikvm( 1896):   at android.content.res.StringBlock.get(StringBlock.java:82)
I/dalvikvm( 1896):   at android.content.res.AssetManager.getPooledString(AssetManager.java:273)
I/dalvikvm( 1896):   at android.content.res.TypedArray.loadStringValueAt(TypedArray.java:726)
I/dalvikvm( 1896):   at android.content.res.TypedArray.getText(TypedArray.java:96)
I/dalvikvm( 1896):   at android.widget.TextView.<init>(TextView.java:581)
I/dalvikvm( 1896):   at android.widget.TextView.<init>(TextView.java:343)
I/dalvikvm( 1896):   at java.lang.reflect.Constructor.constructNative(Native Method)
I/dalvikvm( 1896):   at java.lang.reflect.Constructor.newInstance(Constructor.java:415)
I/dalvikvm( 1896):   at android.view.LayoutInflater.createView(LayoutInflater.java:505)
I/dalvikvm( 1896):   at com.android.internal.policy.impl.PhoneLayoutInflater.onCreateView(PhoneLayoutInflater.java:56)
I/dalvikvm( 1896):   at android.view.LayoutInflater.createViewFromTag(LayoutInflater.java:568)
I/dalvikvm( 1896):   at android.view.LayoutInflater.rInflate(LayoutInflater.java:623)
I/dalvikvm( 1896):   at android.view.LayoutInflater.inflate(LayoutInflater.java:408)
I/dalvikvm( 1896):   at android.view.LayoutInflater.inflate(LayoutInflater.java:320)
I/dalvikvm( 1896):   at android.view.LayoutInflater.inflate(LayoutInflater.java:276)
I/dalvikvm( 1896):   at com.android.internal.policy.impl.PhoneWindow.setContentView(PhoneWindow.java:207)
I/dalvikvm( 1896):   at android.app.Activity.setContentView(Activity.java:1657)
I/dalvikvm( 1896):   at com.example.menny.emojitestV9.MainActivity.onCreate(MainActivity.java:11)
I/dalvikvm( 1896):   at android.app.Instrumentation.callActivityOnCreate(Instrumentation.java:1047)
I/dalvikvm( 1896):   at android.app.ActivityThread.performLaunchActivity(ActivityThread.java:1611)
I/dalvikvm( 1896):   at android.app.ActivityThread.handleLaunchActivity(ActivityThread.java:1663)
I/dalvikvm( 1896):   at android.app.ActivityThread.access$1500(ActivityThread.java:117)
I/dalvikvm( 1896):   at android.app.ActivityThread$H.handleMessage(ActivityThread.java:931)
I/dalvikvm( 1896):   at android.os.Handler.dispatchMessage(Handler.java:99)
I/dalvikvm( 1896):   at android.os.Looper.loop(Looper.java:130)
I/dalvikvm( 1896):   at android.app.ActivityThread.main(ActivityThread.java:3683)
I/dalvikvm( 1896):   at java.lang.reflect.Method.invokeNative(Native Method)
I/dalvikvm( 1896):   at java.lang.reflect.Method.invoke(Method.java:507)
I/dalvikvm( 1896):   at com.android.internal.os.ZygoteInit$MethodAndArgsCaller.run(ZygoteInit.java:839)
I/dalvikvm( 1896):   at com.android.internal.os.ZygoteInit.main(ZygoteInit.java:597)
I/dalvikvm( 1896):   at dalvik.system.NativeStart.main(Native Method)
I/dalvikvm( 1896):
E/dalvikvm( 1896): VM aborting
I/DEBUG   ( 1187): *** *** *** *** *** *** *** *** *** *** *** *** *** *** *** ***
I/DEBUG   ( 1187): Build fingerprint: 'generic_x86/sdk_x86/generic_x86:2.3.7/GINGERBREAD/3093079:eng/test-keys'
I/DEBUG   ( 1187): pid: 1896, tid: 1896  >>> com.example.menny.emojitestV9 <<<
I/DEBUG   ( 1187): signal 11 (SIGSEGV), code 1 (SEGV_MAPERR), fault addr deadd00d
I/DEBUG   ( 1187):  eax 00000000  ebx 823ee4f8  ecx 00001000  edx 00000000
I/DEBUG   ( 1187):  esi b0f6a450  edi 823b7565
I/DEBUG   ( 1187):  xcs 00000073  xds 0000007b  xes 0000007b  xfs 00000000 xss 0000007b
I/DEBUG   ( 1187):  eip 82353cfe  ebp bfe98d88  esp bfe98d70  flags 00010246
I/DEBUG   ( 1187): #00
I/DEBUG   ( 1187):     eip: 82353cfe  /system/lib/libdvm.so (dvmAbort)
I/DEBUG   ( 1187): #01
I/DEBUG   ( 1187):     eip: 82339851  /system/lib/libdvm.so (checkUtfString)
I/DEBUG   ( 1187): #02
I/DEBUG   ( 1187):     eip: 8233994c  /system/lib/libdvm.so (Check_NewStringUTF)
I/DEBUG   ( 1187): #03
I/DEBUG   ( 1187):     eip: 8088c884  /system/lib/libandroid_runtime.so (_ZN7androidL43android_content_StringBlock_nativeGetStringEP7_JNIEnvP8_jobjectii)
I/DEBUG   ( 1187): #04
I/DEBUG   ( 1187):     eip: 82315611  /system/lib/libdvm.so
I/DEBUG   ( 1187): #05
I/DEBUG   ( 1187):     eip: 083a4be0
I/DEBUG   ( 1187): #06
I/DEBUG   ( 1187):     eip: 4489243c
I/DEBUG   ( 1187): #07
I/DEBUG   ( 1187):     eip: ffffffff
I/DEBUG   ( 1187): stack:
I/DEBUG   ( 1187): #00
I/DEBUG   ( 1187):     bfe98d70  00000000
I/DEBUG   ( 1187):     bfe98d74  823b7565  /system/lib/libdvm.so
I/DEBUG   ( 1187):     bfe98d78  823bc109  /system/lib/libdvm.so
I/DEBUG   ( 1187):     bfe98d7c  823ee4f8
I/DEBUG   ( 1187):     bfe98d80  82353cb9  /system/lib/libdvm.so (dvmAbort)
I/DEBUG   ( 1187):     bfe98d84  823ee4f8   (dvmAbort)
I/DEBUG   ( 1187):     bfe98d88  bfe98de8   (dvmAbort)
I/DEBUG   ( 1187): #01
I/DEBUG   ( 1187):     bfe98d8c  82339851  /system/lib/libdvm.so (checkUtfString)
I/DEBUG   ( 1187):     bfe98d90  083a6e48   (checkUtfString)
I/DEBUG   ( 1187):     bfe98d94  00000000   (checkUtfString)
I/DEBUG   ( 1187):     bfe98d98  823b8974  /system/lib/libdvm.so
I/DEBUG   ( 1187):     bfe98d9c  b05432c5
I/DEBUG   ( 1187):     bfe98da0  b061103d
I/DEBUG   ( 1187):     bfe98da4  08532450
I/DEBUG   ( 1187):     bfe98da8  823b99f3  /system/lib/libdvm.so (__FUNCTION__.18803)
I/DEBUG   ( 1187):     bfe98dac  00000000   (__FUNCTION__.18803)
I/DEBUG   ( 1187):     bfe98db0  0000002c   (__FUNCTION__.18803)
I/DEBUG   ( 1187):     bfe98db4  b1d00a10   (__FUNCTION__.18803)
I/DEBUG   ( 1187):     bfe98db8  00008000   (__FUNCTION__.18803)
I/DEBUG   ( 1187):     bfe98dbc  b1d00a7c   (__FUNCTION__.18803)
I/DEBUG   ( 1187):     bfe98dc0  bfe98e30   (__FUNCTION__.18803)
I/DEBUG   ( 1187):     bfe98dc4  083a6e48   (__FUNCTION__.18803)
I/DEBUG   ( 1187):     bfe98dc8  823b99ed  /system/lib/libdvm.so (__FUNCTION__.18803)
I/DEBUG   ( 1187):     ......  ......
I/DEBUG   ( 1187): #02
I/DEBUG   ( 1187):     bfe98dec  8233994c  /system/lib/libdvm.so (Check_NewStringUTF)
I/DEBUG   ( 1187):     bfe98df0  00000001   (Check_NewStringUTF)
I/DEBUG   ( 1187):     bfe98df4  823b99ed  /system/lib/libdvm.so (__FUNCTION__.18803)
I/DEBUG   ( 1187):     bfe98df8  001dd242   (__FUNCTION__.18803)
I/DEBUG   ( 1187):     bfe98dfc  af438ed0   (__FUNCTION__.18803)
I/DEBUG   ( 1187):     bfe98e00  00000020   (__FUNCTION__.18803)
I/DEBUG   ( 1187):     bfe98e04  00000000   (__FUNCTION__.18803)
I/DEBUG   ( 1187):     bfe98e08  af43909b   (__FUNCTION__.18803)
I/DEBUG   ( 1187):     bfe98e0c  00000000   (__FUNCTION__.18803)
I/DEBUG   ( 1187):     bfe98e10  00000000   (__FUNCTION__.18803)
I/DEBUG   ( 1187):     bfe98e14  00000000   (__FUNCTION__.18803)
I/DEBUG   ( 1187):     bfe98e18  00000000   (__FUNCTION__.18803)
I/DEBUG   ( 1187):     bfe98e1c  808dc8dc   (__FUNCTION__.18803)
I/DEBUG   ( 1187):     bfe98e20  083a4be0   (__FUNCTION__.18803)
I/DEBUG   ( 1187):     bfe98e24  084bb1a4   (__FUNCTION__.18803)
I/DEBUG   ( 1187):     bfe98e28  bfe98e78   (__FUNCTION__.18803)
I/DEBUG   ( 1187):     ......  ......
I/DEBUG   ( 1187): #03
I/DEBUG   ( 1187):     bfe98e2c  8088c884  /system/lib/libandroid_runtime.so (_ZN7androidL43android_content_StringBlock_nativeGetStringEP7_JNIEnvP8_jobjectii)
I/DEBUG   ( 1187):     bfe98e30  083a4be0   (_ZN7androidL43android_content_StringBlock_nativeGetStringEP7_JNIEnvP8_jobjectii)
I/DEBUG   ( 1187):     bfe98e34  af43909c   (_ZN7androidL43android_content_StringBlock_nativeGetStringEP7_JNIEnvP8_jobjectii)
I/DEBUG   ( 1187):     bfe98e38  bfe98e5c   (_ZN7androidL43android_content_StringBlock_nativeGetStringEP7_JNIEnvP8_jobjectii)
I/DEBUG   ( 1187):     bfe98e3c  00000000   (_ZN7androidL43android_content_StringBlock_nativeGetStringEP7_JNIEnvP8_jobjectii)
I/DEBUG   ( 1187):     bfe98e40  40000000   (_ZN7androidL43android_content_StringBlock_nativeGetStringEP7_JNIEnvP8_jobjectii)
I/DEBUG   ( 1187):     bfe98e44  0842f0c4   (_ZN7androidL43android_content_StringBlock_nativeGetStringEP7_JNIEnvP8_jobjectii)
I/DEBUG   ( 1187):     bfe98e48  00000000   (_ZN7androidL43android_content_StringBlock_nativeGetStringEP7_JNIEnvP8_jobjectii)
I/DEBUG   ( 1187):     bfe98e4c  bfe98e5c   (_ZN7androidL43android_content_StringBlock_nativeGetStringEP7_JNIEnvP8_jobjectii)
I/DEBUG   ( 1187):     bfe98e50  00000000   (_ZN7androidL43android_content_StringBlock_nativeGetStringEP7_JNIEnvP8_jobjectii)
I/DEBUG   ( 1187):     bfe98e54  bfe98e94   (_ZN7androidL43android_content_StringBlock_nativeGetStringEP7_JNIEnvP8_jobjectii)
I/DEBUG   ( 1187):     bfe98e58  808836ab  /system/lib/libandroid_runtime.so (_ZN7androidL39android_content_AssetManager_applyStyleEP7_JNIEnvP8_jobjectiiiiP10_jintArrayS5_S5_)
I/DEBUG   ( 1187):     bfe98e5c  00000002   (_ZN7androidL39android_content_AssetManager_applyStyleEP7_JNIEnvP8_jobjectiiiiP10_jintArrayS5_S5_)
I/DEBUG   ( 1187):     bfe98e60  b142c8c8   (_ZN7androidL39android_content_AssetManager_applyStyleEP7_JNIEnvP8_jobjectiiiiP10_jintArrayS5_S5_)
I/DEBUG   ( 1187):     bfe98e64  bfe98e94   (_ZN7androidL39android_content_AssetManager_applyStyleEP7_JNIEnvP8_jobjectiiiiP10_jintArrayS5_S5_)
I/DEBUG   ( 1187):     bfe98e68  bfe98eb4   (_ZN7androidL39android_content_AssetManager_applyStyleEP7_JNIEnvP8_jobjectiiiiP10_jintArrayS5_S5_)
I/DEBUG   ( 1187):     ......  ......
I/DEBUG   ( 1187): #04
I/DEBUG   ( 1187):     bfe98e7c  82315611  /system/lib/libdvm.so
I/DEBUG   ( 1187):     bfe98e80  083a4be0
I/DEBUG   ( 1187):     bfe98e84  b1809290
I/DEBUG   ( 1187):     bfe98e88  084bb1a4
I/DEBUG   ( 1187):     bfe98e8c  0000000c
I/DEBUG   ( 1187):     bfe98e90  b1d00b28
I/DEBUG   ( 1187):     bfe98e94  bfe98ee4
I/DEBUG   ( 1187):     bfe98e98  8231f3f7  /system/lib/libdvm.so (tryMalloc)
I/DEBUG   ( 1187):     bfe98e9c  00000024   (tryMalloc)
I/DEBUG   ( 1187):     bfe98ea0  b142c85c   (tryMalloc)
I/DEBUG   ( 1187):     bfe98ea4  083a6e48   (tryMalloc)
I/DEBUG   ( 1187):     bfe98ea8  b0f6a450   (tryMalloc)
I/DEBUG   ( 1187):     bfe98eac  823ee4f8   (tryMalloc)
I/DEBUG   ( 1187):     bfe98eb0  bfe98f00   (tryMalloc)
I/DEBUG   ( 1187):     bfe98eb4  8235a3f6  /system/lib/libdvm.so (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187): #05
I/DEBUG   ( 1187): #06
I/DEBUG   ( 1187):     8235a3fa  4489243c   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     8235a3fe  bbe80424   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     8235a402  8b00013e   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     8235a406  758bf45d   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     8235a40a  fc7d8bf8   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     8235a40e  c35dec89   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     8235a412  90909090   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     8235a416  90909090   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     8235a41a  90909090   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     8235a41e  89559090   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     8235a422  24648de5   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     8235a426  2444c7b8   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     8235a42a  00000704   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     8235a42e  f45d8900   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     8235a432  e8fc7d89   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     8235a436  fffbb177   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     ......  ......
I/DEBUG   ( 1187): #07
I/DEBUG   ( 1187):     89e4458f  ffffffff   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     89e44593  ffffffff   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     89e44597  ffffffff   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     89e4459b  ffffffff   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     89e4459f  ffffffff   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     89e445a3  ffffffff   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     89e445a7  ffffffff   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     89e445ab  ffffffff   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     89e445af  ffffffff   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     89e445b3  ffffffff   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     89e445b7  ffffffff   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     89e445bb  ffffffff   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     89e445bf  ffffffff   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     89e445c3  ffffffff   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     89e445c7  ffffffff   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     89e445cb  ffffffff   (dvmCallJNIMethod_staticNoRef)
I/DEBUG   ( 1187):     ......  ......
D/Zygote  ( 1189): Process 1896 terminated by signal (11)
I/ActivityManager( 1246): Process com.example.menny.emojitestV9 (pid 1896) has died.
```
