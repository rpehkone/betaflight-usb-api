# Fork of [betaflight-configurator](https://github.com/betaflight/betaflight-configurator)

## Goals
- Gain understanding of the usb serial connection
- Auto connect
- Read sensors over serial
- Control motors over serial

## App build via Vite (web)

### Development

1. Install node.js (refer to [.nvmrc](./.nvmrc) for required version)
2. Install yarn: `npm install yarn -g`
3. Change to project folder and run `yarn install`.
4. Run `yarn dev`.

The web app will be available at http://localhost:8000 with full HMR.

### Build Preview

1. Run `yarn build`.
2. Run `yarn preview` after build has finished.
3. Alternatively run `yarn review` to build and preview in one step.

The web app should behave directly as in production, available at http://localhost:8080.

## App build via NW.js (windows/linux/macos) or Cordova (android)

### Development

1. Install node.js (refer to [.nvmrc](./.nvmrc) for required version)
2. Install yarn: `npm install yarn -g`
3. (For Android platform only) Install Java JDK 8, Gradle and Android Studio (Android SDK at least level 19). On Windows you have to extract Gradle binaries to C:\Gradle and set up some environmental variables.

| Variable Name | Value |
|---|---|
| ANDROID_HOME | %LOCALAPPDATA%\Android\sdk |
| ANDROID_SDK_ROOT | %LOCALAPPDATA%\Android\sdk |
| Path | %ANDROID_HOME%\tools<br>%ANDROID_HOME%\platform-tools<br>C:\Gradle\bin |
4. Change to project folder and run `yarn install`.
5. Run `yarn start`.

### App build and release

The tasks are defined in `gulpfile.js` and can be run with through yarn:
```
yarn gulp <taskname> [[platform] [platform] ...]
```

List of possible values of `<task-name>`:
* **dist** copies all the JS and CSS files in the `./dist` folder [2].
* **apps** builds the apps in the `./apps` folder [1].
* **debug** builds debug version of the apps in the `./debug` folder [1][3].
* **release** zips up the apps into individual archives in the `./release` folder [1].

[1] Running this task on macOS or Linux requires Wine, since it's needed to set the icon for the Windows app (build for specific platform to avoid errors).
[2] For Android platform, **dist** task will generate folders and files in the `./dist_cordova` folder.
[3] For Android platform, you need to configure an emulator or to plug an Android device with USB debugging enabled

#### Build or release app for one specific platform
To build or release only for one specific platform you can append the plaform after the `task-name`.
If no platform is provided, the build for the host platform is run.

* **MacOS X** use `yarn gulp <task-name> --osx64`
* **Linux** use `yarn gulp <task-name> --linux64`
* **Windows** use `yarn gulp <task-name> --win64`
* **Android** use `yarn gulp <task-name> --android`

**Note:** Support for cross-platform building is very limited due to the requirement for platform specific build tools. If in doubt, build on the target platform.

You can also use multiple platforms e.g. `yarn gulp <taskname> --osx64 --linux64`. Other platforms like `--win32`, `--linux32` and `--armv8` can be used too, but they are not officially supported, so use them at your own risk.

#### Leverage GitHub-Actions to build binaries

You can use the GitHub `Actions` tab in your fork to build binaries as well. Select `Actions`>`Manual Build`>`Run Workflow`. Choose your custom branch and click `Run workflow`. The workflow will dispatch in a few moments and upon completion, the build "Artifacts" will be available for download from within the workflow run.
