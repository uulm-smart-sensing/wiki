Welcome to our Anwendungsprojekt 22-23 Wiki.

# Overview
- [Introduction and Motivation](#introduction-and-motivation)
- [Getting Started](#getting-started)
- [How it Works](#how-it-works)
- [Sensors](#sensors)


## Introduction and Motivation

Study apps can be helpful for the successful conduct of medical and psychological studies. \
Especially the use of sensors, for example from smartphones or wearables, can provide useful data to support the study. 
Therefore, the development of such apps should be as simple as possible in order to be able to use them without great effort. 
\
\
That's why we develop a smart sensing library, which can be used to easily implement cross-platform apps with Flutter. 
This library will be able to track sensors from the smartphone and some wearables, collect the sensor data and save it. 
Additionally, it will be possible to either get live data or store and process the data. 

All further information, about how you can use and test the library and a demo app can be found in the [smart-sensing-library](https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/smart-sensing-library) repository.

## Development hints

### Keeping Pigeon code up to date

Pigeon is a plugin that generates API code for all three of our platforms (Dart, Android, iOS).
The API code is defined in the `./pigeons` directory. If the content changes, run the following command to keep the code up to date.

On Windows run:

```powershell
.\run_pigeon.ps1
```

On Linux/macOS run:

```bash
bash run_pigeon.sh
```

### Working on Android

We use Android Studio to write code for our Android sensor implementations.
In order for Android Studio to recognize all dependencies, it is mandatory to open the `./example/android/` directory with Android Studio. If any other directory is opened, the dependencies won't be recognized.

#### Linting

We use [Ktlint](https://pinterest.github.io/ktlint/) to lint our Kotlin code.

For a simple check, run:

```bash
./gradlew ktlintCheck
```

For Ktlint to format the code automatically, run:

```bash
./gradlew ktlintFormat
```

### Working on iOS

For the development of the iOS platform code, which is written in Swift, we use Xcode.
In order for Xcode to recognize all dependencies and correctly set up the project structure, it is mandatory to open the `./example/ios/` directory with Xcode.

#### Linting

To lint the Swift code we use [Swiftlint](https://github.com/realm/SwiftLint) (see [here](https://github.com/realm/SwiftLint#installation) for installation guide).
If *Swiftlint* is installed successfully, you can manually check the Swift files by running

```bash
swiftlint
```
and correct fixable linting issues with

```bash
swiftlint --fix
```

For further configuration of the `swiftlint` command, it is recommended to use a `.swiftlint.yml` file, which already exists in this repository and can be extended.

---

If you want *Swiftlint* to be automatically run by Xcode, you need to set up a new "Run script phase" in the "Build phases" of your target and execute the `swiftlint` command there, as described [here](https://github.com/realm/SwiftLint#xcode).


## How it Works

### Software Architecture
This section covers the software architecture. It is split into two core components: \
[Smart Sensing Library](https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/smart-sensing-library) and the [Sensing Plugin](https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/sensing-plugin). 
\
\
The reason for this is that we have one component to read and standardize sensor data in a platform-independent way, while the other component represents most of the smart features like storage and filtering of values.

More information can be found in the software design document in [Documentation](https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/documentation).

#### Smart Sensing Library 

Architectur

![Architectur](https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/documentation/-/blob/master/Software%20design%20document/Graphics/SmartSensingLibraryNew.png)

Class Diagram

![IOManager](https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/documentation/-/blob/master/Software%20design%20document/Graphics/SmartSensingLibraryNew.png)

![SensorManager](https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/documentation/-/blob/master/Software%20design%20document/Graphics/SmartSensingLibraryNew.png)

## Sensors

### Guideline on how to add support for a new sensor

When adding a new sensor to our `sensing_plugin` the following steps should be followed. It's best to do all of the steps in the [Flutter](#flutter) section first. Once this is done, the `run_pigeon` script must be run to generate the changes for the platforms.

#### Flutter

1. Add a new value to the `SensorId` enum in [api_sensor_manager.dart](https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/sensing-plugin/-/blob/main/pigeons/api_sensor_manager.dart).

    ```dart
    enum SensorId {
        ...
        newSensor,
    }
    ```

2. If the unit of the values that the sensor produces is not already present, add the unit to the `Unit` enum in [api_sensor_manager.dart](https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/sensing-plugin/-/blob/main/pigeons/api_sensor_manager.dart).

    ```dart
    enum Unit {
        ...
        // New unit category
        newUnit,
    }
    ```

3. Consider adding units from the same category to which the values can be converted to.
4. If a new unit is added, an according conversion method must be added in [unit_converter.dart](https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/sensing-plugin/-/blob/main/lib/src/preprocessing/unit_converter.dart).

    ```dart
    final unitConversionMethods = <Unit, double Function(double, Unit, Unit)>{
        ...
        Unit.newUnit: _convertNewUnitCategory,
    };

    ...

    double _convertNewUnitCategory(
        double value,
        Unit sourceUnit,
        Unit targetUnit,
    ) {
        ...
    }
    ```

5. The best way to convert units within a category is to convert each source unit to a single unit and then convert that unit to the target unit.
6. Don't forget to add conversion tests in [unit_converter_test.dart](https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/sensing-plugin/-/blob/main/test/preprocessing/unit_converter_test.dart).
7. Now you are all set up to implement the sensors on Android and iOS.

#### Android

To support a new sensor on the Android platform, first check whether it is possible to access this data and what permissions are necessary.

1. Add a new Kotlin class to the [sensors package](https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/sensing-plugin/-/tree/main/android/src/main/kotlin/de/uniulm/sensing_plugin/sensors) and name it after the new sensor (`NewSensor.kt`).
2. The constructor should take two parameters: a `SensorManager` `sensorManager` and a `Long` `timeIntervalInMicroseconds`.
3. The class must be derived from `SensorStreamHandler`. `sensorManager` and `timeIntervalInMicroseconds` can be passed to the base constructor.
4. For `sensorId` pass the appropriate `Sensor.TYPE_*` constant and for `unit` pass the appropriate `Unit` enum value.
5. In the end, the file will look like this:

    ```kotlin
    package de.uniulm.sensing_plugin.sensors

    ...

    class NewSensor(
        sensorManager: SensorManager,
        timeIntervalInMicroseconds: Long
    ) : SensorStreamHandler(
        sensorManager,
        Sensor.TYPE_NEW_SENSOR,
        timeIntervalInMicroseconds,
        Unit.NEW_UNIT
    )
    ```

6. If you have added a sensor that is not already listed in [sensor_information.md](sensor_information.md) or if something about the information has changed, update the document.
7. Now you are all set up on the Android side.

#### iOS

To support a new sensor on the iOS platform, first check whether it is possible to access this data and what permissions and swift packages are necessary.
> For example the `Gyroscope` sensor can provide data (= `CMGyroData`) when using the class `CMMotionManager` resp. package `CoreMotion` in general.
If it is possible to access the sensor or access at least collected sensor data, do the following steps:

1. Create a new class for the sensor and inherit the `IStreamHandler` protocol.
2. If the class, which provide access to the sensor should only be instantiated once: register the class in the `ManagerCollection` by creating a `get<name of the manager>Manager()` method, which returns a singleton instance
3. Collect all necessary information about the sensor and use this information (e. g. accuracy, if known) to fill the related methods (e. g. `getSensorInfo()`)
4. Implement the protocol methods from the `IStreamHandler` by accessing the manager methods and format the retrieved data (c. f. `GyroscopeHandler` for a basic example, how the implementation could look like)
5. Register the stream handler in the `init` method of the `SensorManager` by placing an instance in the corresponding map
6. Document everything by adding comments (possible warnings, addional information, ...) and checking, whether the information already (completely) exist in the [sensor_information.md](sensor_information.md) file

### Sensor implementation information

See [sensor_information.md](https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/documentation/-/blob/master/Sensors/sensor_information.md) for information about how the sensors work and how to implement them.
