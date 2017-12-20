# NavitiaSDK UX for Cordova

Cordova plugin for using NavitiaSDK UX

## Installation

This plugin uses Carthage to build dependencies for iOS, please install it first:
https://github.com/Carthage/Carthage

Then use this command to install the plugin

    cordova plugin add cordova-plugin-navitia-sdk-ux

## Usage

### NavitiaSDKUX.init(config, success, failure)

| Parameters | Type | Required | Description | Example |
| --- | --- |:---:| --- | --- |
| config | Object | ✓ | Configuration | |
| config.token | String | ✓ | Token navitia | 0de19ce5-e0eb-4524-a074-bda3c6894c19 |
| success | Function | ✓ | Success callback function | function() {} |
| failure | Function | ✓ | Failure callback function | function(error) {} |

### NavitiaSDKUX.invokeJourneyResults(params, success, failure)

| Parameters | Type | Required | Description | Example |
| --- | --- |:---:| --- | --- |
| params | Object | ✓ | Parameters of the screen | |
| params.originId | String | ✓ | Origin coordinates, following the format `lon;lat` | 2.3665844;48.8465337 |
| params.destinationId | String | ✓ | Destination coordinates, following the format `lon;lat` | 2.2979169;48.8848719 |
| params.originLabel | String | ✗ | Origin label, if not set the address will be displayed | Home |
| params.destinationLabel | String | ✗ | Destination label, if not set the address will be displayed | Work |
| params.datetime | Date | ✗ | Requested date and time for journey results | new Date() |
| params.datetimeRepresents | NavitiaSDKUX.DatetimeRepresents | ✗ | Can be `NavitiaSDKUX.DatetimeRepresents.DEPARTURE` (journeys after datetime) or `NavitiaSDKUX.DatetimeRepresents.ARRIVAL` (journeys before datetime). | NavitiaSDKUX.DatetimeRepresents.DEPARTURE |
| params.forbiddenUris | [String] | ✗ | List of navitia uris | ['commercial_mode:Bus', 'line:1'] |
| params.firstSectionModes | [NavitiaSDKUX.SectionMode] | ✗ | List of modes to use at the begining of the journey | [NavitiaSDKUX.SectionMode.CAR] |
| params.lastSectionModes | [NavitiaSDKUX.SectionMode] | ✗ | List of modes to use at the end of the journey | [NavitiaSDKUX.SectionMode.BIKE, NavitiaSDKUX.SectionMode.BSS] |
| params.count | Integer | ✗ | The number of journeys that will be displayed | 3 |
| params.minNbJourneys | Integer | ✗ | The minimum number of journeys that will be displayed | 3 |
| params.maxNbJourneys | Integer | ✗ | The maximum number of journeys that will be displayed | 10 |
| success | Function | ✓ | Success callback function | function() {} |
| failure | Function | ✓ | Failure callback function | function(error) {} |

### Example

    var config = {
        token: 'my-token',
    };

    NavitiaSDKUX.init(config, function() {}, function(error) {
        console.log(error);
    });

    var journeyParams = {
        originLabel: 'My Home',
        originId: '2.3665844;48.8465337',
        destinationId: '2.2979169;48.8848719',
    };

    NavitiaSDKUX.invokeJourneyResults(journeyParams, function() {}, function(error) {
        console.log(error);
    });

## Known issues

- Color configuration not available yet (but soon!)

## Troubleshooting
### Specific android tools version : 26
In case you are having problems building and getting this kind of problems :
```
platforms/android/build/intermediates/res/merged/debug/values-v24/values-v24.xml:3: AAPT: Error retrieving parent for item: No resource found that matches the given name ...
```

You may try to override your android compiler environment variables :

```
export ORG_GRADLE_PROJECT_cdvCompileSdkVersion=android-26
export ORG_GRADLE_PROJECT_cdvBuildToolsVersion=26.0.1
```

More information on [Cordova website](https://cordova.apache.org/docs/en/7.x/guide/platforms/android/index.html#setting-gradle-properties) 