# Ex.No:6 Create a simple application to request storage and camera permission at RunTime using android studio.


## AIM:

To develop a simple application for RunTime Permission in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min.required Giraffe)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as runtimepermission and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Display process of runtimepermission in android mobile devices.

Step 7: Save and run the application.

## PROGRAM:
```
/*
Program to print the process of runtimepermission in android mobile devices”.
Developed by:MANISHA M
Registeration Number : 212224220061
*/
```
# MainActivity.java
```
package com.example.runtimepermissiondemo;

import android.Manifest;
import android.content.pm.PackageManager;
import android.os.Bundle;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;

public class MainActivity extends AppCompatActivity {

    private static final int PERMISSION_REQUEST_CODE = 100;

    private TextView tvStatus;
    private Button btnRequest;

    // Permissions required
    private final String[] permissions = {
            Manifest.permission.CAMERA,
            Manifest.permission.READ_MEDIA_IMAGES
    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        setContentView(R.layout.activity_main);

        tvStatus = findViewById(R.id.tvStatus);
        btnRequest = findViewById(R.id.btnRequest);

        btnRequest.setOnClickListener(v -> {
            checkAndRequestPermissions();
        });

        updateStatusText();
    }

    private void checkAndRequestPermissions() {

        boolean allGranted = true;

        for (String permission : permissions) {

            if (ContextCompat.checkSelfPermission(
                    this,
                    permission
            ) != PackageManager.PERMISSION_GRANTED) {

                allGranted = false;
                break;
            }
        }

        if (allGranted) {

            Toast.makeText(
                    this,
                    "All permissions already granted!",
                    Toast.LENGTH_SHORT
            ).show();

        } else {

            ActivityCompat.requestPermissions(
                    this,
                    permissions,
                    PERMISSION_REQUEST_CODE
            );
        }
    }

    @Override
    public void onRequestPermissionsResult(
            int requestCode,
            @NonNull String[] permissions,
            @NonNull int[] grantResults) {

        super.onRequestPermissionsResult(
                requestCode,
                permissions,
                grantResults
        );

        if (requestCode == PERMISSION_REQUEST_CODE) {

            boolean allGranted = true;

            for (int result : grantResults) {

                if (result != PackageManager.PERMISSION_GRANTED) {
                    allGranted = false;
                    break;
                }
            }

            if (allGranted) {

                Toast.makeText(
                        this,
                        "All permissions granted!",
                        Toast.LENGTH_LONG
                ).show();

            } else {

                Toast.makeText(
                        this,
                        "Some permissions were denied.",
                        Toast.LENGTH_LONG
                ).show();
            }

            updateStatusText();
        }
    }

    private void updateStatusText() {

        boolean cameraGranted =
                ContextCompat.checkSelfPermission(
                        this,
                        Manifest.permission.CAMERA
                ) == PackageManager.PERMISSION_GRANTED;

        boolean imagesGranted =
                ContextCompat.checkSelfPermission(
                        this,
                        Manifest.permission.READ_MEDIA_IMAGES
                ) == PackageManager.PERMISSION_GRANTED;

        String status =
                "Camera: "
                        + (cameraGranted
                        ? "✅ GRANTED"
                        : "❌ DENIED")
                        + "\n"
                        + "Photos: "
                        + (imagesGranted
                        ? "✅ GRANTED"
                        : "❌ DENIED");

        tvStatus.setText(status);
    }
}
```
# AndroidManifest.xml

```
<?xml version="1.0" encoding="utf-8"?>

<manifest xmlns:android="http://schemas.android.com/apk/res/android">

    <uses-permission android:name="android.permission.CAMERA" />

    <uses-permission android:name="android.permission.READ_MEDIA_IMAGES" />

    <application
        android:allowBackup="true"
        android:label="@string/app_name"
        android:supportsRtl="true"
        android:theme="@style/Theme.RuntimePermissionDemo">

        <activity
            android:name=".MainActivity"
            android:exported="true">

            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />

            </intent-filter>

        </activity>

    </application>

</manifest>
```
# activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>

<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center"
    android:padding="16dp">

    <TextView
        android:id="@+id/tvStatus"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Permissions Status"
        android:textSize="18sp"
        android:textStyle="bold"
        android:layout_marginBottom="30dp" />

    <Button
        android:id="@+id/btnRequest"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Request Permissions"
        android:textSize="16sp" />

</LinearLayout>
```


## OUTPUT
<img width="340" height="612" alt="image" src="https://github.com/user-attachments/assets/9dc2c80d-8715-4fc7-bff4-115c74930890" />
<img width="322" height="717" alt="image" src="https://github.com/user-attachments/assets/809bafc0-3df5-4890-a6b6-5337b1a1e44f" />





## RESULT
Thus a Simple Android Application to request storage and camera permission at RunTime in Android Studio is developed and executed successfully.
