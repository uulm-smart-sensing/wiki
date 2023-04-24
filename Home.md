Welcome to our Anwendungsprojekt 22-23 Wiki.

# Overview
- [Introduction and Motivation](#introduction-and-motivation)
- [Getting Started](#getting-started)
- [How it Works](#how-it-works)


## Introduction and Motivation

Study apps can be helpful for the successful conduct of medical and psychological studies. \
Especially the use of sensors, for example from smartphones or wearables, can provide useful data to support the study. 
Therefore, the development of such apps should be as simple as possible in order to be able to use them without great effort. 
\
\
That's why we develop a smart sensing library, which can be used to easily implement cross-platform apps with Flutter. 
This library will be able to track sensors from the smartphone and some wearables, collect the sensor data and save it. 
Additionally, it will be possible to either get live data or store and process the data. 


## Getting Started

1. Clone the repo

    ```bash
    git clone https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/smart-sensing-library.git
    ```

2. Execute setup script

    On Windows run:

    ```powershell
    .\setup.ps1
    ```

    On Linux/macOS run:

    ```bash
    bash setup.sh
    ```

3. Your setup is now complete and you're good to go.


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

### Linting

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

### Linting

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

### Smart Sensing Library 

Architectur

![Architectur](https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/documentation/-/blob/master/Software%20design%20document/Graphics/SmartSensingLibraryNew.png)

Class Diagram

![IOManager](https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/documentation/-/blob/master/Software%20design%20document/Graphics/SmartSensingLibraryNew.png)

![SensorManager](https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/documentation/-/blob/master/Software%20design%20document/Graphics/SmartSensingLibraryNew.png)