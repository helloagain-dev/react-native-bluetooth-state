# react-native-bluetooth-state
Native module for React Native to get the current bluetooth state of the device. This is a fork of [frostney/react-native-bluetooth-state](https://github.com/frostney/react-native-bluetooth-state), which adds the functionality for Android.

## Installation

Since v2.2.0 React Native >=0.40.0 is needed.

Install it via npm:
```
$ npm install --save https://github.com/Artirigo/react-native-bluetooth-state.git
```

## Link the libraries

### iOS
Follow the [React Native documentation for Linking Libraries](https://facebook.github.io/react-native/docs/linking-libraries-ios.html).

You also need to link the `CoreBluetooth.framework` to __Link Binary With Libraries__.

### Android
Add the following to your `android/settings.gradle`:
```
include ':react-native-bluetooth-state'
project(':react-native-bluetooth-state').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-bluetooth-state/android')
```

Add the following to the `dependencies`-section inside your `android/app/build.gradle`:
```
dependencies {
    // ... other dependencies
    compile project(':react-native-bluetooth-state')
}

```

Add the package in your `MainApplication.java`:

```java
// other imports
import com.artirigo.bluetoothstate.RNBluetoothStatePackage;

public class MainApplication extends Application implements ReactApplication {
    // ...

    protected List<ReactPackage> getPackages() {
        return Arrays.<ReactPackage>asList(
                new MainReactPackage(),
                // other packages
                new RNBluetoothStatePackage()); // <-- Add this line
    }
}
```

## Usage

The returned states are on both iOS and Android returned as String:

- `on`
- `off`
- `unknown` (currently default value on Android, if other states are returned from the native module)
- `unauthorized`
- `unsupported`

and only on iOS:

- `resetting`

```javascript
import BluetoothState from 'react-native-bluetooth-state';

const stateChangeHandler = bluetoothState => {
  // handle the state
  console.info(bluetoothState);
};

// subscribe to changes
BluetoothState.subscribe(stateChangeHandler);

// Initialize needs to be called otherwise we don't get the initial state
BluetoothState.initialize();

// unsubscribe specific handler
BluetoothState.unsubscribe(stateChangeHandler);

// remove all change handlers
BluetoothState.clear();
```

## License
MIT
