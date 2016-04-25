# Installation
1. Create a new project with Android Studio (or use a existing Android Studio Project)
2. In the root of the project, run command 
```
git clone https://github.com/magnetsystems/message-chatkit-android
```
Alternatively, you can add it as a git submodule (assume it's under source control with git)
```
git submodule add https://github.com/magnetsystems/message-chatkit-android
```
3. In Android Studio, add mmxchatsdk as a module.
4. Add following repositories in the root build.gradle 
```

    jcenter()
    maven {
      url "https://repo.magnet.com/artifactory/public"
    }

    maven {
      url "http://dev-repo.magnet.com:8081/artifactory/everything"
      credentials {
        username = "pritesh.shah"
        password = "aardvark"
      }
    }

    maven {
      url "https://repo.commonsware.com.s3.amazonaws.com"
    }
    maven {
      url "https://jitpack.io"
    }
 
```
5.Enable dataBinding in your app build.gradle
```
android {
...

  dataBinding {
    enabled = true
  }

...
}
```

# Integration with your App

## Initialization
In your Application subclass, init the Max and ChatSDK
```
public class ChatSampleApplication extends MultiDexApplication {

...
 @Override
  public void onCreate() {
    super.onCreate();

    //Initialization of the MagnetMax
    Max.init(this, new MaxAndroidPropertiesConfig(this, com.magnet.chatsdk.sample.R.raw.magnetmax));
    
   //Initialization of Chat SDK 
   ChatSDK.init(this);

```

## Enable incoming message after User Login
```
User.login(email, password, remember, new ApiCallback<Boolean>() {
            @Override
            public void success(Boolean aBoolean) {
                ...
                // Start MMX to enable incoming message
                MMX.start();
               ...
            }

            @Override
            public void failure(ApiError apiError) {
                Logger.error("login", apiError);
            }
        });
```
# SDK components
## ChatListActivity
This activity shows the list of chat current user.
Click on one item will go to ChatActivity
Click on the Floating Action Bar will go to ChooseUserActivity to start a new Chat

## ChatActivity
This activity is the actual chat window where user sends and receives message with other user/users.
Click on "Details" menu will go to 

## ChooseUserActivity
This activity shows the users in the app (be default) who you can choose to start a new chat or add to existing chat.

## ChatDetailsActivity
This activity shows all the members in the chat.
If current user is the creator of the chat, click on the "+" menu item will go to ChooseUserActivity to add more user(s) to the chat

# Customization
## Color
Following are the colors you can customize
```
    <color name="primary">#2196F3</color>
    <color name="primary_dark">#1976D2</color>
    <color name="primary_light">#BBDEFB</color>
    <color name="accent">#517daa</color>
    <color name="primary_text">#212121</color>
    <color name="secondary_text">#727272</color>

    <color name="buttonsTextColor">#517daa</color>
    <color name="itemSelected">#c3c3c3</color>
    <color name="itemNotSelected">#fff</color>


    <color name="colorHintText">#51517daa</color>
    <color name="colorLightGray">#cccccc</color>
    <color name="colorDarkTransparent">#88000000</color>

    <color name="messageBackgroundFromMe">#517daa</color>
    <color name="messageBackgroundToMe">#e6e6e6</color>

    <color name="FABBackground">#00c0ff</color>
```
## Theme
The SDK has a theme MagnetChatSDKTheme, to customize it, you need to add 
tools:replace="android:theme" in the application tag of application Manifest
