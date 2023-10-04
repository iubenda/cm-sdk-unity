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

## API Documentation

### `Initialize`
Initializes the Consent Manager with the provided domain, code ID, app name, and language.
- **Parameters**:
  - `domain`: The domain of the Consent Management Platform.
  - `codeId`: The code ID for the application.
  - `appName`: The name of the application.
  - `language`: The language code (e.g., "EN", "DE") for localization.

### `SetAndroidCallbacks`
Sets Android-specific callbacks for CMP events.

### `SetIOSCallbacks`
Sets iOS-specific callbacks for CMP events.

### `HasConsent`
Checks if the user has given consent.
- **Returns**: `true` if user has given consent, `false` otherwise.

### `OpenConsentLayer`
Opens the Consent Layer to manage user's consent settings.

### `OpenConsentLayerOnCheck`
Opens the Consent Layer if necessary based on checks.

### `HasVendor`
Checks if a vendor with the specified ID has been selected by the user.
- **Parameters**:
  - `id`: The ID of the vendor to check.
- **Returns**: `true` if the vendor is selected, `false` otherwise.

### `HasPurpose`
Checks if a purpose with the specified ID has been selected by the user.
- **Parameters**:
  - `id`: The ID of the purpose to check.
- **Returns**: `true` if the purpose is selected, `false` otherwise.

### `GetAllPurposes`
Gets a list of all available purposes.
- **Returns**: A list of purpose IDs.

### `GetEnabledPurposes`
Gets a list of enabled purposes.
- **Returns**: A list of enabled purpose IDs.

### `GetDisabledPurposes`
Gets a list of disabled purposes.
- **Returns**: A list of disabled purpose IDs.

### `GetAllVendors`
Gets a list of all available vendors.
- **Returns**: A list of vendor IDs.

### `GetEnabledVendors`
Gets a list of enabled vendors.
- **Returns**: A list of enabled vendor IDs.

### `GetDisabledVendors`
Gets a list of disabled vendors.
- **Returns**: A list of disabled vendor IDs.

### `ExportCmpString`
Exports the Consent Management Platform (CMP) settings as a string.
- **Returns**: The exported CMP settings as a string.

### `GetGoogleAcString`
Gets the Google Advertiser Consent string.
- **Returns**: The Google Advertiser Consent string.

### `GetUsPrivacyString`
Gets the US Privacy string.
- **Returns**: The US Privacy string.

## Support

For bug reports, feature requests, or general inquiries, please [open an issue](https://support.iubenda.com/support/homer) on the repository.

## License

This plugin is licensed under the [MIT License](LICENSE).

## Credits

- Created and maintained by [Skander Ben Abdelmalak](skander@bentech.app).
