# Consent Management Platform (CMP) Unity Plugin

The Consent Management Platform (CMP) Unity Plugin allows you to easily integrate Consent Management functionality into your Unity applications for handling user consent and privacy preferences.

## Features

- Supports both iOS and Android platforms.
- Provides a bridge between Unity and native platform-specific CMP functionalities.
- Allows you to initialize, manage user consent, and handle privacy-related data.

## Getting Started

1. **Installation**: Add the CMP Unity Plugin package to your Unity project.

    - Import the package into your Unity project using Assets > Import Package > Custom Package.

2. **Usage**: Follow these steps to start using the plugin.

    - **Initialization**: To use the CMP functionality, initialize the CMPManager instance.

      ```csharp
      CmpManager.Instance.Initialize(domain, codeId, appName, language);
      ```

    - **Consent Layer**: Display the consent layer using the following:

      ```csharp
      CmpManager.Instance.OpenConsentLayer();
      ```

    - **Check Consent**: Check if the user has given consent:

      ```csharp
      bool hasConsent = CmpManager.Instance.HasConsent();
      ```

    - **Callbacks**: Set callback listeners for various events:

      ```csharp
      CmpManager.Instance.SetIOSCallbacks(openListener, closeListener, cmpNotOpenedCallback, onErrorCallback, onCmpButtonClickedCallback);
      ```

    - **Purpose and Vendor Checks**: Check for consent related to specific purposes and vendors:

      ```csharp
      bool hasPurpose = CmpManager.Instance.HasPurpose(id);
      bool hasVendor = CmpManager.Instance.HasVendor(id);
      ```

    - **Export Data**: Export CMP data:

      ```csharp
      string cmpString = CmpManager.Instance.ExportCmpString();
      ```

3. **Documentation**: For detailed API documentation and usage examples, refer to the [official documentation](https://help.consentmanager.net).

## Compatibility

- Unity 20XX.X.X or later
- iOS (via DllImport)
- Android (via JNI)

## iOS

### Using iOS Callbacks in Unity with CmpSdk

#### Import Namespaces
```csharp
using UnityEngine;
using AOT;
using CmpSdk.Callbacks;
```

#### Implement Callback Functions
Decorate your static callback methods with the `[MonoPInvokeCallback]` attribute to define the callback type.

```csharp
        [MonoPInvokeCallback(typeof(CmpOpenListenerBlock))]
        public static void OnWebViewOpenedStatic()
        {
            Debug.Log("CMPConsentTool opened");
        }

        [MonoPInvokeCallback(typeof(CmpCloseListenerBlock))]
        public static void DefaultCloseListener()
        {
            Debug.Log("DefaultCloseListener called");
        }

        [MonoPInvokeCallback(typeof(CmpNotOpenListenerBlock))]
        public static void DefaultNotOpenListener()
        {
            Debug.Log("DefaultNotOpenListener called");
        }

        [MonoPInvokeCallback(typeof(CmpErrorListenerBlock))]
        public static void DefaultErrorListener(CmpErrorType type, string message)
        {
            Debug.Log($"DefaultErrorListener called. ErrorType: {type}, Message: {message}");
        }

        [MonoPInvokeCallback(typeof(CmpButtonEventListenerBlock))]
        public static void DefaultCmpButtonClickedListener(CmpButtonEvent type)
        {
            Debug.Log($"DefaultCmpButtonClicked called. Type: {type}");
        }
```

#### Set Up Callbacks
Use the `SetIOSCallbacks` method from CmpSdk to link your static methods to native callbacks.

```csharp
_cmpManager.SetIOSCallbacks(OnWebViewOpenedStatic, DefaultCloseListener, DefaultNotOpenListener, DefaultErrorListener, DefaultCmpButtonClickedListener);
```

This will bind your Unity static methods to the native iOS callbacks, allowing seamless communication between Unity and native code.

## Android

To ensure compatibility with custom layout fragments, it is imperative to integrate an external dependency. This can be accomplished through two distinct methods:

1. **Manual Addition to maintemplate.gradle**:

   If you choose to handle dependencies manually, you must add the required library to your custom `maintemplate.gradle`. This process provides you with greater control over the versions and configurations.

   Please add the AppCompat Dependency to your Android mainTemplate.gradle file:
   ```
    implementation 'androidx.appcompat:appcompat:1.3.1'
   ```
2. **Utilization of External Dependency Manager**:

   For a more streamlined approach, the External Dependency Manager for Unity (EDM4U) can be used. If you've opted for this method:

   - Navigate to the `CmpSdkDependencies.xml` file located in your Unity project.
   - You'll find the necessary dependencies commented out for your convenience. Simply uncomment the relevant lines of code to activate them:
     ```xml
     <dependencies>
         <androidPackage>
             <dependency name="androidx.appcompat:appcompat:1.3.1" />
         </androidPackage>
     </dependencies>
     ```

By adhering to one of the aforementioned procedures, you can ensure that your Unity plugin remains compatible with custom layout fragments on Android.

### Setting Up Android Callbacks in Unity with CmpSdk

#### Implement Callback Interfaces
First, implement the required callback interfaces for Android in your Unity MonoBehaviour class.

```csharp
public class CmpSampleScript : MonoBehaviour, IOnOpenCallback, IOnCloseCallback, IOnCmpNotOpenedCallback, IOnCmpButtonClickedCallback, IOnErrorCallback,IOncCmpImportProcessed
{
    public void onWebViewOpened() { /*...*/ }
    public void onWebViewClosed() { /*...*/ }
    public void onCMPNotOpened() { /*...*/ }
    public void onButtonClicked(CmpButtonEvent buttonEvent) { /*...*/ }
    public void errorOccurred(CmpErrorType errorType, string message) { /*...*/ }
}
```

#### Set Callbacks
Finally, use the `SetAndroidCallbacks` method to register your callback implementations with the CmpSdk manager.

```csharp
_cmpManager.SetAndroidCallbacks(this, this, this, this, this);
```

Your MonoBehaviour class methods will be invoked when the corresponding events are triggered in the native Android code.

## Troubleshooting

### Advanced Changes: Editing AppCompat Style

If there's a need to make more intricate modifications, such as editing the AppCompat style, you have the flexibility to do so directly within the plugin's codebase.

#### Modifying AppCompat Style in `GradlePostProcessor.cs`

The specific values for the AppCompat style are housed in the `GradlePostProcessor.cs` class. To modify them:

1. Navigate to the `UpdateThemeAppCompatInAndroidManifestFile` function within the `GradlePostProcessor.cs` file.
2. Locate the following lines of code that define the theme styles:
   ```csharp
   var oldValue = @"android:theme=""@style/UnityThemeSelector""";
   var newValue = @"android:theme=""@style/Theme.AppCompat.DayNight""";

### Disabling AppCompatActivity in `UnityPlayerActivity`

If your project doesn't utilize a custom layout and you prefer not to add the `AppCompatActivity` to the `UnityPlayerActivity`, there's an option to disable the relevant post-build steps in the Gradle processor.

#### Steps to Disable:

1. Navigate to the `OnPostGenerateGradleAndroidProject` function within your processor script.
2. You'll find the post-build steps for updating the `UnityPlayerActivity` and the AppCompat theme. To disable these steps, simply comment out the corresponding lines of code:
   ```csharp
   // UpdateUnityPlayerActivity(path);
   // UpdateThemeAppCompatInAndroidManifestFile(path);

## Support

For bug reports, feature requests, or general inquiries, please [open an issue](https://support.iubenda.com/support/homer) on the repository.

## License

This plugin is licensed under the [MIT License](LICENSE).

## Credits

- Created and maintained by [Consentmanager](https://www.consentmanager.net).
