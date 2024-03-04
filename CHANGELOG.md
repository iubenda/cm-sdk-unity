# Changelog

All notable changes to this project will be documented in this file.


## Version 1.0.0 (Released on 2024-03-04)

### Breaking Changes
- The layouting is now predefined and it's not necessary to define the UI Consent layer by pixels if custom layouts are desired
- UIConfig Class is added with UI configurations

### Added
- ATTracking support
- Google Consent Mode V2 Support
- Integration of predefined custom layouts.


## Version 0.99.0 (Released on 2023-12-18)

### Breaking Changes
- The `CmpSdk` class has been renamed to `CmpManager`.
- The Callbacks have been renamed to `IOnOpenCallback`, `IOnCloseCallback`, `IOnCmpNotOpenedCallback`, `IOnCmpButtonClickedCallback`, `IOnErrorCallback`.
- The `SetAndroidCallbacks` and `SetIOSCallbacks` method has been removed. The callbacks are now set in the `AddEventListeners` method.
- Renaming of Internal Classes and Methods

### Added
- Implementation of Assembler Files
- Editor Window for Build Scripts
- Integration of Custom Layouts for Android

### Refactor
- Streamlining Event Listener Implementation for iOS
- Optimization of Build Scripts
- Event Callbacks are now set in the `AddEventListeners` method
- Event Callbacks are now executed on the main thread

## Version 0.4.0 (Released on 2023-11-15)

### Added
- CmpConfig Object
- ImportCmpString

## Version 0.3.0 (Released on 2023-10-25)

### Added
- Custom Layout Feature and configuration class added.

### Refactor
- Optimised integration of iOS xcFramework

## Version 0.2.0 (Released on 2023-10-03)

### Added
- Support for older Gradle Versions 6.1.1

### Refactor
- Updated consentmanager SDK dependency and removed jitpack

## Version 0.1.0 (Released on 2023-08-24)

### Added
- Unity SDK Implementation for iOS and Android
