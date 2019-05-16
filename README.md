# Piggy Stickers App for WhatsApp

![](/png/pig.png)

## Sticker art and app requirements

![](/png/ss.jpg)

We recommend you refer to the FAQ at https://faq.whatsapp.com/general/26000226 for complete details on how to properly create your sticker art. 

This FAQ also contains a sample PSD that demonstrates best practices for composing legible, rich sticker art.

* A sticker is an image that has a transparent background and can be sent in a
  WhatsApp chat
* Stickers are organized into "packs". Your app can contain anywhere from 1 to
  10 packs. Users must explicitly add each pack to WhatsApp one-by-one, so your
  app should list each pack separately and each pack must have its own
  affordance to add it to WhatsApp (do not try to create "add all packs"
  operations).
* Each sticker pack must have a minimum of 3 stickers and a maximum of 30
  stickers
* Stickers must be exactly 512 x 512 pixels
* Stickers will render on a variety of backgrounds, white, black, colored, patterned, etc. Test your sticker art on a variety of backgrounds. For this reason, we recommend you add a 8px #FFFFFF stroke to the outside of each sticker. See the sample PSD referenced at https://faq.whatsapp.com/general/26000226 for more details.
* Stickers must be in the [WebP format](https://developers.google.com/speed/webp). Currently, animated WebP or animated stickers are not supported. If you are using a linux machine install the package webp and use the command cwebp -q 100 input.png -o output.webp
* Each sticker must be less than 100KB. 
* Sticker Picker/Tray Icon
    * Provide an image that will be used to represent your sticker pack in the WhatsApp sticker picker/tray 
    * This image should be 96 x 96 pixels
    * Max file size of 50KB

## How to create the sticker app

### Overview
If you would like to create a sticker app using this app, you only have to minimally modify the given code of the app to get up and running quickly. 

* After downloading this repo, open the entire folder for the sample app in [Android Studio](https://developer.android.com/studio/). If you are new to Android development, visit https://developer.android.com/training/basics/firstapp/index.html for more information on setting up your Android development environment.
* Navigate to SampleStickerApp/app/src/main/assets in Android Studio. 
* Inside the assets folder, folder 1 contains a number of sample sticker art files. Replace these with your own sticker files.
* Also replace the sample tray icon PNG with your own tray icon. 
* If you'd like to have more than 1 sticker pack in your app, simply create a folder named "2" or "3", etc. within the assets folder and place your art and tray icon in there. 

### Modifying the contents.json file
You must also modify the contents.json file in SampleStickerApp/app/src/main/assets. Replace the values of the metadata with your own. A few notes:

* `name`: the sticker pack's name (128 characters max)
* `identifier`: The identifier should be unique and can be alphanumeric: a-z, A-Z, 0-9, and the following characters are also allowed "_", "-", "." and " ". The identifier should be less than 128 characters.
* `publisher`: name of the publisher of the pack (128 characters max)
* Replace the "image_file" value with the file name of your sticker image. It must have both the file name and extension. The ordering of the files in the JSON will dictate the ordering of your stickers in your pack. 
* `android_play_store_link` and `ios_app_store_link` (optional fields): here you can put the URL to your sticker app in the Google Play Store and Apple App Store (if you have an iOS version of your sticker app). If you provide these URLs, users who receive a sticker from your app in WhatsApp can tap on it to view your sticker app in the respective App Stores. On Android, the URL follows the format https://play.google.com/store/apps/details?id=com.example where "com.example" is your app's package name.
* `emojis` (optional): add up to a maximum of three emoji for each sticker file. Select emoji that best describe or represent that sticker file. For example, if the sticker is portraying love, you may choose to add a heart emoji like 💕. If your sticker portrays pizza, you may want to add the pizza slice emoji 🍕. In the future, WhatsApp will support a search function for stickers and tagging your sticker files with emoji will enable that. The sticker picker/tray in WhatsApp today already categorizes stickers into emotion categories (love, happy, sad, and angry) and it does this based on the emoji you tag your stickers with.

The following fields are optional: `ios_app_store_link`, `android_app_store_link`, `publisher_website`, `privacy_policy_website`, `license_agreement_website`, `emoji`
All the links need to start with either "http" or "https"

If your app has more than 1 sticker pack, you will need to reference it in contents.json. Simply create a second array within the "sticker_packs" section of the JSON and include all the metadata (name, identifier, etc) along with all the references to the sticker files. 

### Build the sample app
Before building your app, you will need to do the following: 

* Make sure to change the app's icon (i.e. launcher icon) that will be displayed on the home screens of users who install your app. The icons are contained in SampleStickerApp/app/src/main/res in each of the folders beginning with mipmap (e.g. mipmap-xhdpi or mipmap-xxxhdpi). For a simple way to create these icons, you can use Android Image Asset Studio which is built into Android Studio. See https://developer.android.com/studio/write/image-asset-studio#access for more information on how to run this tool and read the section [here](https://developer.android.com/studio/write/image-asset-studio#create-adaptive) for information on how to use the tool to create your app's launcher icons.
* Change your apps name in strings.xml (SampleStickerApp/app/src/main/res/values/strings.xml). This is the name users will see for your app on their phone. You can consider providing translations of your app name by following this instruction: https://developer.android.com/guide/topics/resources/localization

Make sure to run and test your sticker app. For help on building your app, visit https://developer.android.com/studio/run/. The app will run some checks. If there are problems, you will see the error in [logcat](https://developer.android.com/studio/debug/am-logcat.html). If there are no errors, the app will launch successfully displaying the sticker packs you have included.

## Submit your app
You need to build a release version of your app for submission to the Google Play Store. Click Build > Generate Signed Bundle/APK. For more information, visit https://developer.android.com/studio/publish/app-signing#sign-apk. Note that Android Studio saves the APKs you build in project-name/module-name/build/outputs/apk. For more information on building your app, visit https://developer.android.com/studio/run/.

To submit your app to the Google Play Store, follow the instructions here: https://developer.android.com/distribute/best-practices/launch/. 

It is advised that you create Multiple APKs per ABI (CPU Architecture), it will make the published app size smaller. see https://developer.android.com/studio/build/configure-apk-splits for more information. In order to do that, uncomment the lines 47-52 in app/build.gradle line.
