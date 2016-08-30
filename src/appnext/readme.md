[&#8249; Appnext Doc Home](./)

<h1>Appnext Integration Guide</h1>
<<[../../shared/-VERSION-/version.md]

##Integration

### Account Registration

you must sign up for [Appnext](https://www.appnext.com/) and setup your app. make sure you have following items before proceeding to SDK integration

**Appnext Account & ID**

You must register for an Appnext Account in order to integrate the Appnext plugin.
Log in to your Appnext account. If you do not have an Appnext account, copy the following URL to the browser: https://www.appnext.com and sign up.

**Placement ID**

A unique ID called a “Placement ID” is required for all inbound requests. A Placement ID is a 32-character
string generated by Appnext for every registered app.

**Get a Unique ID**

To get started - add a new App via the Appnext Self-Service Platform, then copy the Placement ID, which
can be found in your account at: Apps -> Settings Icon-> Settings & Placements -> Placement ID
If you plan to show ads for both iOS and Android users, you will need to add a separate App for Android
and a separate App for iOS and copy the Placement ID of each app.

### Plugin Integration

Open a terminal and use the following command to install the SDKBOX Appnext plugin.
```bash
$ sdkbox import appnext
```


##Extra steps
1. For portrait iOS games with landscape video ad:

1.1 Edit `RootViewController.mm` file

    ```
    // For ios6, use supportedInterfaceOrientations & shouldAutorotate instead
    - (NSUInteger) supportedInterfaceOrientations{
    #ifdef __IPHONE_6_0
        return UIInterfaceOrientationMaskPortrait; // only portrait here
    #endif
    }
    - (BOOL) shouldAutorotate {
        return YES;
    }
    ```

1.2 Add Landscape orientations support

For Full-Screen/Rewarded Ad: Landscape orientations (Landscape left/Landscape Right).
Click on your project in the 'Project navigator'->'General'->'Device Orientation' and add the
required orientations for both iPhone/iPad devices.

1.3 set `"orientation":"landscape"` in `sdkbox_config.json`

<<[../../shared/notice.md]

<!--## Configuration
<<[../../shared/sdkbox_cloud.md]
<<[../../shared/remote_application_config.md]-->

### JSON Configuration
SDKBOX Installer will automatically inject a sample configuration to your `sdkbox_config.json`, that you have to modify it before you can use it for your own app

- id

- type: [string]

    - "interstitial"
    - "fullscreen"
    - "reward"

#### options

- creative_type:

    - "managed"
    - "video"
    - "static"

- progress_type:

    - "clock"
    - "bar"
    - "none"

- video_lenght:

    - "short"
    - "long"

- button_text
- button_color
- categories
- postback
- can_close

- skip_text
- mute
- autoplay

- progress_color: [string]
- show_close_button: [bool]
- close_delay: [float]
- orientation: [string]

    - "automatic"
    - "landscape"
    - "portrait"
    - "not_set"

more information:

- [https://selfservice.appnext.com/Apps/Tools.aspx#android/interstitial-sdk/native-app/advanced_settings](https://selfservice.appnext.com/Apps/Tools.aspx#android/interstitial-sdk/native-app/advanced_settings)
- [https://selfservice.appnext.com/Apps/Tools.aspx#android/full-screen/rewarded-sdk-beta/advanced_settings](https://selfservice.appnext.com/Apps/Tools.aspx#android/full-screen/rewarded-sdk-beta/advanced_settings)
- [https://selfservice.appnext.com/Apps/Tools.aspx#android/full-screen/rewarded-sdk-beta/app_categories](https://selfservice.appnext.com/Apps/Tools.aspx#android/full-screen/rewarded-sdk-beta/app_categories)

Example:
```json

{
    "ios": {
        "Appnext":{
            "debug":true,
            "ads": {
                "default": {
                    // Please replace this placement id with your own placement id from appnext
                    "id":"please_replace_with_your_placement_id",
                    "type":"interstitial",

                    "button_text":"Button Text",
                    "button_color":"#6AB344",
                    "categories":"Action,Puzzle",
                    "postback":"postback",

                    "skip_text":"Skip Text",
                    "mute":false,
                    "autoplay":true,
                    "creative_type":"managed"
                },
                "fullscreen": {
                    // Please replace this placement id with your own placement id from appnext
                    "id":"please_replace_with_your_placement_id",
                    "type":"fullscreen",

                    "button_text":"Button Text",
                    "button_color":"#6AB344",
                    "categories":"Action,Puzzle",
                    "postback":"postback",

                    "progress_type":"clock",
                    "progress_color":"#ffffff",
                    "show_close_button":true,
                    "video_lenght":"short",
                    "close_delay":5.0,
                    "orientation":"automatic"
                },
                "reward": {
                    // Please replace this placement id with your own placement id from appnext
                    "id":"please_replace_with_your_placement_id",
                    "type":"reward",

                    "button_text":"Button Text",
                    "button_color":"#6AB344",
                    "categories":"Action,Puzzle",
                    "postback":"postback",

                    "progress_type":"bar",
                    "progress_color":"#ffff00",
                    "show_close_button":true,
                    "video_lenght":"long",
                    "close_delay":5.0,
                    "orientation":"automatic"
                }
            }
        }
    },
    "android": {
        "Appnext":{
            "debug":true,
            "ads": {
                "default": {
                    // Please replace this placement id with your own placement id from appnext
                    "id":"please_replace_with_your_placement_id",
                    "type":"interstitial",

                    "button_text":"Button Text",
                    "button_color":"#6AB344",
                    "categories":"Action,Puzzle",
                    "postback":"postback",
                    "can_close":false,

                    "skip_text":"Skip Text",
                    "mute":false,
                    "autoplay":true,
                    "creative_type":"managed"
                },
                "fullscreen": {
                    // Please replace this placement id with your own placement id from appnext
                    "id":"please_replace_with_your_placement_id",
                    "type": "fullscreen",

                    "button_text":"Button Text",
                    "button_color":"#6AB344",
                    "categories":"Action,Puzzle",
                    "postback":"postback",
                    "can_close":false,

                    "progress_type":"clock",
                    "progress_color":"#ffffff",
                    "show_close_button":true,
                    "video_lenght":"short",
                    "orientation":"automatic"
                },
                "reward": {
                    // Please replace this placement id with your own placement id from appnext
                    "id":"please_replace_with_your_placement_id",
                    "type": "reward",

                    "button_text":"Button Text",
                    "button_color":"#6AB344",
                    "categories":"Action,Puzzle",
                    "postback":"postback",
                    "can_close":false,

                    "progress_type":"bar",
                    "progress_color":"#ffff00",
                    "show_close_button":false,
                    "video_lenght":"long",
                    "orientation":"automatic"
                }
            }
        }
    }
}

```

##Usage
<<[usage.md]

<<[api-reference.md]

<<[manual_integration.md]

<<[manual_ios.md]

<<[../../shared/manual_integration_android_and_android_studio.md]

<<[manual_android.md]

<<[extra-step.md]

<<[proguard.md]