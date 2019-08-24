# BARCODE & QRCODE SCAN IN FLUTTER 
 How to implement Barcode and QRCode Scan in Flutter

# Introduction:
 In this article we will learn how to implement barcode and QRcode scanner feature in flutter. We will use barcode_scan plugin for that. Barcode_scan plugin written in kotlin so we need some extra efforts for android.

## Output:

## Plugin Required: barcode_scan: ^1.0.0

## Programming Steps:
1. First and basic step to create new application in flutter. If you are a beginner in flutter then you can check my blog Create a first app in Flutter. I have created an app named as “flutter_barcode_scan”

2. For Android, you must do the following before you can use the plugin:
 - Add the camera permission to your AndroidManifest.xml
```
<uses-permission android:name="android.permission.CAMERA" />
```
 - Add the BarcodeScanner activity to your AndroidManifest.xml. Do NOT modify the name.
```
<activity android:name="com.apptreesoftware.barcodescan.BarcodeScannerActivity"/>
```
 - This plugin is written in Kotlin. Therefore, you need to add Kotlin support to your project.

3. Edit your project-level build.gradle file to look like this:
```
buildscript {
    ext.kotlin_version = '1.3.30'
    ...
    dependencies {
        ...
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
    }
}
...
```

4. Edit your app-level build.gradle file to look like this:
```
apply plugin: 'kotlin-android'
...
dependencies {
    implementation "org.jetbrains.kotlin:kotlin-stdlib:$kotlin_version"
    ...
}
```

5. Open the pubspec.yaml file in your project and add the following dependencies into it.
```
dependencies:
 flutter:
   sdk: flutter
 cupertino_icons: ^0.1.2
 barcode_scan: ^1.0.0
```

6. In main.dart we will implement floating button to open camera to scan barcode then scanned code will be displayed in the textbox. Following is the implementation of that. 
```
import 'package:flutter/material.dart';
import 'package:barcode_scan/barcode_scan.dart';
 
void main() => runApp(MyApp());
 
class MyApp extends StatelessWidget {
 @override
 Widget build(BuildContext context) {
   return MaterialApp(
     theme: ThemeData(
       primarySwatch: Colors.blue,
     ),
     home: MyHomePage(),
   );
 }
}
 
class MyHomePage extends StatefulWidget {
 @override
 _MyHomePageState createState() => _MyHomePageState();
}
 
class _MyHomePageState extends State<MyHomePage> {
 String barcode = "";
 Future scanCode() async {
   try {
     String barcode = await BarcodeScanner.scan();
     setState(() => this.barcode = barcode);
   } catch (e) {
     if (e.code == BarcodeScanner.CameraAccessDenied) {
       setState(() {
         this.barcode = 'The user did not grant the camera permission!';
       });
     } else {
       setState(() => this.barcode = 'Unknown error: $e');
     }
   }
 }
 
 @override
 Widget build(BuildContext context) {
   return Scaffold(
     appBar: AppBar(
       title: Text('Flutter Barcode Scan'),
     ),
     body: Center(
       child: Column(
         mainAxisAlignment: MainAxisAlignment.center,
         children: <Widget>[
           Text(barcode),
         ],
       ),
     ),
     floatingActionButton: FloatingActionButton(
       onPressed: scanCode,
       tooltip: 'Scan',
       child: Icon(Icons.scanner),
     ),
   );
 }
}
```

7. Great, you are done with Barcode and QRCode Scan implementation in flutter. Run this project in device or emulator and check the output.

## Possible Errors:
1. flutter barcode scan Failed to notify project evaluation listener. > java.lang.AbstractMethodError (no error message)

2. Android dependency 'androidx.core:core' has different version for the compile (1.0.0) and runtime (1.0.1) classpath. You should manually set the same version via DependencyResolution

## Solution:
- In android/build.grader change the version 
```
classpath 'com.android.tools.build:gradle:3.3.1'
```

## Conclusion:
 In this article we have learned how to implement Barcode and QRCode scanner in Flutter application. This feature is useful for payments, offer scanning, billing etc.

 Git: https://github.com/myvsparth/flutter_barcode_scan

## Related Tags: Flutter, Barcode Scan, QRCode Scan, Android, iOS
