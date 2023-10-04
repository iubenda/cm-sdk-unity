# Consent Management Platform (CMP) Unity Plugin

The Consent Management Platform (CMP) Unity Plugin allows you to easily integrate Consent Management functionality into your Unity applications for handling user consent and privacy preferences.

## Features

- Supports both iOS and Android platforms.
- Provides a bridge between Unity and native platform-specific CMP functionalities.
- Allows you to initialize, manage user consent, and handle privacy-related data.

## Getting Started

1. **Installation**: Add the CMP Unity Plugin package to your Unity project.

    - [Download the latest release](https://assetstore.unity.com/packages/tools/utilities/cmpsdk-263894) of the plugin.
    - Import the package into your Unity project using Assets > Import Package > Custom Package.

    - Or download the .unitypackage from this repository

2. **Preparation**: In order to use the Unity SDK please follow these steps.

***iOS***

- For iOS you just to be sure that the `CmpSdk.xcframework` is added accordingly to the unity Project.
- Typically for the `Unity-iPhone` target the xcframework should be added as `Embed frameworks`.
- For the `UnityFramework` you have to add the xcframework as `Link Binary With Libraries`

1. **Usage**: Follow these steps to start using the plugin.

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

2. **Documentation**: For detailed API documentation and usage examples, refer to the [official documentation](https://help.consentmanager.net).

## Compatibility

- Unity 20XX.X.X or later
- iOS (via DllImport)
- Android (via JNI)

## Support

For bug reports, feature requests, or general inquiries, please [open an issue](https://support.iubenda.com/support/homer) on the repository.

## License

This plugin is licensed under the [MIT License](LICENSE).

## Credits

- Created and maintained by [Skander Ben Abdelmalak](skander@bentech.app).
