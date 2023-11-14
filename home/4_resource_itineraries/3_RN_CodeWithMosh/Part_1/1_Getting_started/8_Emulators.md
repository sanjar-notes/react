# 8. Emulators
Created Tue Nov 14, 2023 at 2:01 PM

## General
To test apps quickly, we use emulators provided by Android Studio/Xcode. They're not a replacement for "testing", but are essential for quick development.

When RN runs, it provides some dev options inside the device (emulator/physical). This is activated by Pressing Ctrl + M (in emulator) or by shaking the device (for physical device). Options here include:
1. 'Reload'
2. 'Inspector' - Elements tree/styling inspector
3. 'Debug' - Managing debug daemon

## Android
For Android. Open Android Studio (no need to open a project), go to AVD and create a device.


Close Android Studio/Xcode.

To start the app, need to run two terminals simultaneously.
1. `npm start` - start Metro
2. `npm run android` or `npm run ios` - install/update app on emulator by running 

If any physical device are connected via adb, they'll also update without interfering with the emulator.

## iOS
For iOS. Open the project in Xcode, go to platforms and create a device with Rosetta (on M1 laptops).

Close Xcode.

To start the app, need to run two terminals simultaneously.
1. `npm start` - start Metro
2. `npm run ios` - install/update app on emulator by running

If any physical device are connected via adb, they'll also update without interfering with the emulator.


## Windows
TBD