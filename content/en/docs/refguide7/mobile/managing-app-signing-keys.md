---
title: "Managing App Signing Keys"
url: /refguide7/managing-app-signing-keys/
category: "Mobile Development"
#If moving or renaming this doc file, implement a temporary redirect and let the respective team know they should update the URL in the product. See Mapping to Products for more details.
---

## 1 Introduction

To create a mobile app, you need platform-specific app signing keys. A mobile app is signed with a digital signature by its developers before publication. These signatures are used by both app stores and devices to verify that the app is authentic.

Depending on which platforms you want to target, you will need to create the required signing keys. The following sections describe (per platform) how to create those keys.

## 2 iOS{#ios}

Unfortunately, signing keys is always required for iOS app deployment, even if you just want to test the app on your personal device and do not want to publish to the Apple App Store. This section describes how to create the required files.

It is convenient to have an Apple Mac available, but it is not a requirement. You do always need an Apple Developer Account.

### 2.1 On Apple Macs

If you have an Apple Mac available, see the Apple developer documentation on [certificate management](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html) for information on how to obtain an iOS signing certificate and distribution profile. Next, see the Apple documentation on [how to create the required distribution profile](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html). Finally, check the end of this section for information on how to [upload the signing key files to Adobe PhoneGap Build](/refguide7/managing-app-signing-keys/).

### 2.2 On Other Platforms

If you do not have an Apple Mac available, you can create a certificate signing request manually. First, create a private key and certificate signing request with the OpenSSL utilty. The following steps assume you have a Windows machine, but these are equally applicable to Linux machines, which usually have the OpenSSL package pre-installed.

To create a certificate signing request manually, follow these steps:

1. Download [OpenSSL for Windows](https://www.openssl.org/community/binaries.html) and install it. You just need to download and install the **Win32 OpenSSL Light** package (get the latest version at the top of the list).
    * If the setup process complains about a missing VC++ redistributable libraries package, cancel the installation, and first download and install the **Visual C++ 2008 Redistributables** from the same list of packages (you will be redirected to a Microsoft download page). Install OpenSSL to, for example, *C:\OpenSSL* (make note of this directory, as you will need it in step 3).
2. Open a command prompt. On most systems, you need to do this as an administrator (right-click the Windows start menu link and select **Run as Administrator**).
3. Generate a private key with the OpenSSL program that you just installed. Replace `C:\OpenSSL` with where you installed OpenSSL in step 1. The private key file is stored at the location specified after the `-out` parameter. The following example will store the file in the root directory of your C: drive (you can change this to anything you want, just select a convenient place and keep track of where the file is stored): `"C:\OpenSSL\bin\openssl.exe" genrsa -out "C:\private.key" 2048`. The command will output "Generating RSA private key, 2048 bit long modulus" and lots of dots and plus signs.
4. Generate a certificate signing request (CSR). The file is again stored in the same folder, but can be placed anywhere. Make sure to point to the private key file that was created in the previous step: `"C:\OpenSSL\bin\openssl.exe" req -new -key "C:\private.key" -out "C:\ios.csr"`. The command will print some text and then ask you for several different pieces of information related to your identity. Only the **Common Name** is relevant. Fill in your own name, so that the certificate is easily recognized later on after uploading it to the Apple Developer Member Center.

The resulting *ios.csr* file must be uploaded to the Apple Developer Member Center to generate a signed certificate. Follow these steps to do that:

1. Open the [Apple Developer Member Center](https://developer.apple.com/account/overview.action).
2. Under **iOS, tvOS, watchOS**, click **Certificates, All**.
3. In the **iOS Certificates** overview, click the plus button on the top-right. This will open the **Add iOS Certificate** wizard in the **Select Type** step with the caption "What type of certificate do you need?".
    * If the plus button is disabled (greyed out), you do not have enough rights. Ask the company account administrator to give you extra rights.
4. Under **Development**, select **iOS Development Certificate**.
5. Click **Continue**. You are now at step **About Creating a Certificate Signing Request (CSR)**. This page describes how to create a certificate signing request on Macs. You can ignore it.
6. Click **Continue** again. You are now at step **Generate**, captioned **Generate your certificate**.
7. Under **Upload CSR file**, click **Choose File ...**.
8. Select the *ios.csr* certificate signing request file that you created.
9. Click **Continue**. Apple will sign your CSR and make the signed certificate available for download.
    * If you are presented with a message that says that your certificate signing request is pending approval, you do not have enough rights. Ask the company account administrator to approve your certificate signing request.
10. Click **Download** and store the *.cer* file on your disk at a convenient place (for example, next to the private key and CSR files).
11. Click **Done**. The **iOS Certificates** overview page becomes visible again. Your new certificate should be in the list. Here, you can download it again, or you can revoke it (in case you lose the corresponding private key).

### 2.3 Creating the Required Distribution Profile

Once you have the certificate file, you need to obtain a distribution profile. The Apple Developer Member Center allows you to define an app identifier, a test device, and finally a distribution profile. For more information, check the Apple documentation on how to [maintain identifiers, devices and profiles](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html).

### 2.4 Uploading the Key to Adobe PhoneGap Build

Once you have downloaded the signing certificate (a *.cer* file), you need to convert the signing certificate from a *.cer* to a *.p12*. Use OpenSSL with the following steps:

1. Create from the signing certificate a PEM format: `"C:\OpenSSL\bin\openssl.exe" x509 -in "C:\ios.cer" -inform DER -out "C:\ios_pem.pem" -outform PEM`.
2. Create from the PEM certificate a password secured. This action requires the PEM certificate, the private key that was created in step 3 earlier, and the password thas was given on the creation of the *ios.csr*: `"C:\OpenSSL\bin\openssl.exe" pkcs12 -export -out "C:\ios.p12" -inkey "C:\private.key" -in "C:\ios_pem.pem"`.
3. You can upload the signing certificate (now a `.p12` file) and the distribution profile (a `.mobileprovision` file) to Adobe PhoneGap Build on your [account page](https://build.phonegap.com/people/edit). Go to the **Signing Keys** tab and click **Add a key** under **iOS**. Select the two files and give the key a name. Unlock the key by clicking the yellow lock icon on the right of the key and filling in the certificate passphrase. The key is now ready to be used by your build job.

## 3 Android{#android}

Android apps can be developed and deployed to Android devices without signing the apps. However, to publish to app stores, signed apps are required. This requires you generate a keystore and then upload it to Adobe PhoneGap Build.

### 3.1 Generating a Keystore

To generate a keystore for Android, follow these steps:

1. Install Java JDK either for Mac or Windows. Remember where you installed your JDK, as the JDK bin folder will be used later.
2. Open your **Command Prompt** and run your new *keytool.exe* located in your JDK’s bin folder.
3. The *keytool.exe* program can be found in the bin directory of your Java installation (for example: *C:\Program Files\Java\jre1.8.0_20\bin*):

    {{< figure src="/attachments/refguide7/mobile/managing-app-signing-keys/cmdjdkexe.png" alt="keytool location" >}}

4. Type in the following command line prompt while still pointing to the *keystore.exe*: 

    ```text {linenos=false}
    "{{keytool -genkey -v -keystore file.keystore -alias YOUR_ALIAS_NAME -storepass YOUR_ALIAS_PWD -keypass YOUR_ALIAS_PWD -keyalg RSA -validity 36500}}"
    ```

    Be sure to replace `YOUR_ALIAS_NAME` and `YOUR_ALIAS_PWD` with your alias name and password:

    {{< figure src="/attachments/refguide7/mobile/managing-app-signing-keys/ktoolsetup.png" alt="name and password" >}}

5. Answer the subsequent questions, click **Enter** after each question, and type *yes* when asked to confirm your information: 

    {{< figure src="/attachments/refguide7/mobile/managing-app-signing-keys/qanda.png" alt="info questions" >}}

6. Finishing these questions generates a keystore which will be saved into a *file.keystore* file in your current working directory. 

### 3.2 Uploading Your Keystore to PhoneGap Build

After creating the keystore file, upload it to Adobe PhoneGap Build on your [account page](https://build.phonegap.com/). Then, complete the following instructions:

1. Go to the **Signing Keys** tab and click **Add a key** under **Android**. 
2. Select the keystore file, fill in a title for the key, and fill in the alias that you noted down in the previous step. 
3. After uploading the keystore file, unlock the key. Click the yellow lock icon on the right of the key and fill in both the keystore and the key passwords. The key is now ready to be used by your build job.
4. In the [Developer Portal](https://sprintr.home.mendix.com/index.html), navigate to **Deploy > Mobile app**, and click the **Publish for Mobile s** button. Then click the **Start PhoneGap Build job** button.
5. Once the app has been built for the first time, go back to [Adobe PhoneGap Build](https://build.phonegap.com/). Click your app's name to view its build details.
6. Under the **Builds** tab, select your key in the Android build drop-down menu. This will automatically rebuild the app using the key. From now on, the [Developer Portal](https://sprintr.home.mendix.com/index.html) will automatically use this key to build the app.
