### Component types

| Type | Name              | param1    | param2 | param3 | Description                                                                                                                                                                                                                           |
| ---- | ----------------- | --------- | ------ | ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1    | Intent            |           |        |        | Intent is a messaging object used to request an action from another app component, [further details](https://developer.android.com/guide/components/intents-filters)                                                                  |
| 2    | SharedPreferences | Data path |        |        | SharedPreferences is an object that points to small xml file stored in the app's private directory, providing a simple read and write APIs, [further details](https://developer.android.com/training/data-storage/shared-preferences) |
| 3    | Calendar          |           |        |        | Calendar is an object that stores datetime and provides APIs to calculate between a different datetime and more, [further details](https://developer.android.com/reference/java/util/Calendar)                                        |
| 4    | Vibrator          |           |        |        | Vibrator is an object that provides an API to vibrate the device, [further details](https://developer.android.com/reference/android/os/Vibrator)                                                                                      |
| 5    | Timer             |           |        |        | Timer is an object that can schedule tasks for one-time execution, or for repeated execution at regular intervals, [further details](https://developer.android.com/reference/java/util/Timer)                                         |
| 6    | Firebase Database | Data path |        |        | Firebase (Realtime) Database is a database backend provided by [Firebase](https://firebase.google.com)                                                                                                                                |
| 7    | Dialog            |           |        |        | Dialog is an object that can build and show dialogs, [further details](https://developer.android.com/guide/topics/ui/dialogs)                                                                                                         |
| 8    | MediaPlayer       |           |        |        | MediaPlayer is an object that can play and control media files, best suited for long sound files or streams, [further details](https://developer.android.com/reference/android/media/MediaPlayer)                                     |
| 9    | SoundPool         |           |        |        | SoundPool is an object that can play audio files, best suited for small audio files, something like sound effects, [further details](https://developer.android.com/reference/android/media/SoundPool)                                 |
| 10   | ObjectAnimator    |           |        |        | ObjectAnimator is an object that can animate properties of a view over a fixed period of time, [further details](https://developer.android.com/reference/android/animation/ObjectAnimator)                                            |
| 11   | Gyroscope         |
| 12   | FirebaseAuth      |
| 13   | Interstitial Ad   |
| 14   | Firebase Storage  | Data path
| 15   | Camera            |
| 16   | FilePicker        | Mime type
| 17   | RequestNetwork    |
| 18   | TextToSpeech      |
| 19   | SpeechToText      |
| 20   | BluetoothConnect  |
| 21   | LocationManager   |

#### Random questions

> Why param2 and param3 are not used?

I'm just as confused as you as why param2 and param3 are not used at all. I believe it's for backwards-compatibility with older sketchware versions that may have a component that uses three parameters.
