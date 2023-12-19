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
      CmpManager.Instance.AddEventListeners(openListener, closeListener, cmpNotOpenedCallback, onErrorCallback, onCmpButtonClickedCallback);
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

## CmpSdk Plugin Window

### Quick Guide

- **Access**: `Window` > `CmpSdk` > `CmpSdk Build Script Settings` in Unity Editor.
- **iOS Build Script**: Toggle to enable/disable automatic integration for iOS.
- **Android Build Script**: Toggle to enable/disable automatic integration for Android.
- **Custom Layout Integration (Android)**: Enable to use custom layouts for Android (available when Android Build Script is enabled).

---

## Troubleshooting

### Advanced Changes: Editing AppCompat Style

If there's a need to make more intricate modifications, such as editing the AppCompat style, you have the flexibility to do so directly within the plugin's codebase.

#### Modifying AppCompat Style Customization

To customize the AppCompat style more effectively, utilize the newly added `themes.xml` file in your Android build. This approach replaces the previous method of modifying style values in the `GradlePostProcessor.cs` class.

#### Steps for Customization

1. **Locate the Themes File**:
   - The `themes.xml` file is situated at the following path in your Android build:
     ```
     res/values/themes.xml
     ```

2. **Edit the AppCompat Style**:
   - Open the `themes.xml` file.
   - Here, you can directly modify the style attributes to tailor the AppCompat theme to your needs.
---

### Disabling AppCompatActivity in `UnityPlayerActivity`

If your project doesn't utilize a custom layout and you prefer not to add the `AppCompatActivity` to the `UnityPlayerActivity`, there's an option to disable the relevant post-build steps in the Gradle processor.
This will prevent the plugin from updating the `UnityPlayerActivity` and the AppCompat theme.
You can disable these steps by following the steps below:

- **Access**: `Window` > `CmpSdk` > `CmpSdk Build Script Settings` in Unity Editor, uncheck the "Integrate custom layout" options.

## Support

For bug reports, feature requests, or general inquiries, please [open an issue](https://support.iubenda.com/support/home) on the repository.

## License

This plugin is licensed under the [MIT License](LICENSE).

## Credits

- Created and maintained by [Consentmanager](https://www.consentmanager.net).
