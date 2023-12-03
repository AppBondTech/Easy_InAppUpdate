<br/>
<p align="center">
  <a href="https://github.com/AppBondTech/Easy_InAppUpdate">
    <img src="https://mdhasanmahmud.000webhostapp.com/inappupdate/appbondtech.jpg" alt="Logo" width="150" height="150">
  </a>

  <h3 align="center">In-App Update(java)</h3>

  <p align="center">
    Best Easy Way for In-App Update Implementation
    <br/>
    <br/>
    <a href=""><strong> For Details Video Tutorial »</strong></a>
    <br/>
    <br/>
	  
## About The Project

![Screen Shot](https://mdhasanmahmud.000webhostapp.com/inappupdate/eF05z.png)

## Getting Started

> Step 1. Make Sure Add Internet Permissiton in Manifests - 
```
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
```

> Step 2. Add the dependency - 
```
implementation 'com.google.android.play:app-update:2.1.0'	
```

> Step 3. Above On Create Bundle is where we declare various variables - 
```
private int REQUEST_CODE = 11;
```

> Setp 4. Anywhere in the On Create Bundle - 
```
  //In-App Udpates Implementation (1st part)------------------------------------------------------ 
        AppUpdateManager appUpdateManager = AppUpdateManagerFactory.create(MainActivity.this);
        Task<AppUpdateInfo> appUpdateInfoTask = appUpdateManager.getAppUpdateInfo();
        appUpdateInfoTask.addOnSuccessListener(new OnSuccessListener<AppUpdateInfo>() {
            @Override
            public void onSuccess(AppUpdateInfo result) {
                if (result.updateAvailability() == UpdateAvailability.UPDATE_AVAILABLE
                        & result.isUpdateTypeAllowed(AppUpdateType.IMMEDIATE)){
                    try {
                        appUpdateManager.startUpdateFlowForResult(result,AppUpdateType.IMMEDIATE,MainActivity.this,REQUEST_CODE);
                    } catch (IntentSender.SendIntentException e) {
                        throw new RuntimeException(e);
                    }
                }

            }
        });
```
> Step 5. Just below the last second bracket - 
```
//In-App Udpates Implementation (2nd part)------------------------------------------------------ 
 @Override
    protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if (requestCode == REQUEST_CODE){
            Toast.makeText(MainActivity.this,"Start Download",Toast.LENGTH_SHORT).show();
            if (requestCode!=RESULT_OK){
                Log.d("mmm","Update Fail"+resultCode);
            }
        }
    }
```

## In Cooperation

* **Md. Hasan Mahmud** - *Mobile Application Developer* - *Free Library*
