# Block opcodes
This document contains all of sketchware's blocks' opcodes (version 150)

## Types
A block type defines what a block type returns (bool, string, int) / what the block is (single/double-nested block, ending block). A block that doesn't have a type is a regular block.

| Type | Description           |
| ---- | --------------------- |
| b    | Boolean               |
| s    | String                |
| d    | Decimal / Number      |
| l    | List (any list)       |
| p    | Component             |
| v    | View                  |
| c    | A single-nested block |
| e    | A double-nested block |
| f    | "An ending block" A block that can't have another block after it |


If the block type is a `p` (component) or a `v` (view), the `typeName` field of the block gives the exact type of the variable its accessing.

Examples:
 - Type `p` has `typeName` value set to `ObjectAnimator`.
 - Type `v` has `typeName` value set to `LinearLayout`.

Lists does the same thing, but the `typeName` is a bit different. They're (exactly) `List String` if the list generic type is a string, `List Number` for numbers, and `List Map` for list maps.

> I really wonder why there isn't any list booleans lol

Examples:
 - Type `l` has `typeName` value set to `List String` means it returns a list string
 - Type `l` has `typeName` value set to `List Number` means it returns a list number

## The `getVar` block
The `getVar` block is a special block that represents variable access of any type through a combination of spec as the variable name, block type, and block `typeName` as the type.

The block type can be any of the block types defined above except the nested and ending block types.

Examples:
 - Type `b` with spec `isEnabled` represents a variable access of the boolean variable `isEnabled`.
 - Type `d` with spec `count` represents a variable access of the number variable `count`.

## Block categories

### Control flow
| Opcode  | Type |
| ------- | ---- |
| repeat  | c    |
| forever | c    |
| break   | f    |
| if      | c    |
| ifElse  | e    |

### Operators
| Opcode | Type |
| ------ | ----------- |
| true | b |
| false | b |
| < | b |
| = | b |
| > | b |
| && | b |
| \|\| | b |
| not | b |
| + | d |
| - | d |
| * | d |
| / | d |
| % | d |
| random | d |
| stringLength | d |
| stringJoin | s |
| stringIndex | d |
| stringLastIndex | d |
| stringSub | s |
| stringEquals | b |
| stringContains | b |
| stringReplace | s |
| trim | s |
| toUpperCase | s |
| toLowerCase | s |
| toNumber | d |
| toString | s |
| toStringWithDecimal | s |
| toStringFormat | s |
| strToMap |   |
| mapToStr | s |
| strToListMap |   |
| listMapToStr | s |
| addSourceDirectly |   |

### Math
| Opcode | Type |
| ------ | ----------- |
| mathGetDip | d |
| mathGetDisplayWidth | d |
| mathGetDisplayHeight | d |
| mathPi | d |
| mathE | d |
| mathPow | d |
| mathMin | d |
| mathMax | d |
| mathSqrt | d |
| mathAbs | d |
| mathRound | d |
| mathCeil | d |
| mathFloor | d |
| mathSin | d |
| mathCos | d |
| mathTan | d |
| mathAsin | d |
| mathAcos | d |
| mathAtan | d |
| mathExp | d |
| mathLog | d |
| mathLog10 | d |
| mathToRadian | d |
| mathToDegree | d |

### File operations
| Opcode | Type |
| ------ | ----------- |
| fileutilread | s |
| fileutilwrite |   |
| fileutilcopy |   |
| fileutilmove |   |
| fileutildelete |   |
| fileutilisexist | b |
| fileutilmakedir |   |
| fileutillistdir |   |
| fileutilisfile | b |
| fileutillength | d |
| fileutilStartsWith | b |
| fileutilEndsWith | b |
| fileutilGetLastSegmentPath | s |
| getExternalStorageDir | s |
| getPackageDataDir | s |
| getPublicDir | s |
| resizeBitmapFileRetainRatio |   |
| resizeBitmapFileToSquare |   |
| resizeBitmapFileToCircle |   |
| resizeBitmapFileWithRoundedBorder |   |
| cropBitmapFileFromCenter |   |
| rotateBitmapFile |   |
| scaleBitmapFile |   |
| skewBitmapFile |   |
| setBitmapFileColorFilter |   |
| setBitmapFileBrightness |   |
| setBitmapFileContrast |   |
| getJpegRotate | d |

### View operations

Only if there is a drawer in the activity:

| Opcode | Type |
| ------ | ----------- |
| isDrawerOpen | b |
| openDrawer |   |
| closeDrawer |   |

Always on:

| Opcode | Type |
| ------ | ----------- |
| setEnable |   |
| getEnable | b |
| setVisible |   |
| setRotate |   |
| getRotate | d |
| setAlpha |   |
| getAlpha | d |
| setTranslationX |   |
| getTranslationX | d |
| setTranslationY |   |
| getTranslationY | d |
| setScaleX |   |
| getScaleX | d |
| setScaleY |   |
| getScaleY | d |
| getLocationX | d |
| getLocationY | d |
| requestFocus |   |
| setText |   |
| getText | s |
| setTypeface |   |
| setHint |   |
| setChecked |   |
| getChecked | b |
| setBgColor |   |
| setBgResource |   |
| setTextColor |   |
| setHintTextColor |   |
| setImage |   |
| setColorFilter |   |
| setImageFilePath |   |
| setImageUrl |   |
| seekBarSetProgress |   |
| seekBarGetProgress | d |
| seekBarSetMax |   |
| seekBarGetMax | d |
| progressBarSetIndeterminate |   |

View-specific opcodes:

| Opcode | Type |
| ------ | ----------- |
| listSetData |   |
| listSetCustomViewData |   |
| listRefresh |   |
| listSmoothScrollTo |   |
| spnSetData |   |
| spnRefresh |   |
| spnSetSelection |   |
| spnGetSelection | d |
| webViewLoadUrl |   |
| webViewGetUrl | s |
| webViewSetCacheMode |   |
| webViewCanGoBack | b |
| webViewCanGoForward | b |
| webViewGoBack |   |
| webViewGoForward |   |
| webViewClearCache |   |
| webViewClearHistory |   |
| webViewStopLoading |   |
| webViewZoomIn |   |
| webViewZoomOut |   |
| calendarViewSetDate |   |
| calendarViewSetMinDate |   |
| calnedarViewSetMaxDate |   |

Only if admob is enabled:

| Opcode | Type |
| ------ | ----------- |
| adViewLoadAd |   |

Only if Google Map is enabled:

| Opcode | Type |
| ------ | ----------- |
| mapViewSetMapType |   |
| mapViewMoveCamera |   |
| mapViewZoomTo |   |
| mapViewZoomIn |   |
| mapViewZoomOut |   |
| mapViewAddMarker |   |
| mapViewSetMarkerInfo |   |
| mapViewSetMarkerPosition |   |
| mapViewSetMarkerColor |   |
| mapViewSetMarkerIcon |   |
| mapViewSetMarkerVisible |   |

### Component blocks
| Opcode | Type |
| ------ | ----------- |
| doToast |   |
| copyToClipboard |   |
| setTitle |   |

#### Intent

| Opcode | Type |
| ------ | ----------- |
| intentSetAction |   |
| intentSetData |   | 
| intentSetFlags |   |
| startActivity |   |

Only if there are multiple activities:

| Opcode | Type |
| ------ | ----------- |
| intentSetScreen |   |
| intentPutExtra |   |
| intentGetString | s |
| finishActivity | f |

#### Unknown
| Opcode | Type |
| ------ | ----------- |
| fileGetData | s |
| fileSetData |   |
| fileRemoveData |   |

#### Calendar
| Opcode | Type |
| ------ | ----------- |
| calendarGetNow |   |
| calendarAdd |   |
| calendarSet |   |
| calendarFormat | s |
| calendarDiff | d |
| calendarGetTime | d |
| calendarSetTime |   |

#### Vibrator
| Opcode | Type |
| ------ | ----------- |
| vibratorAction |   |

#### Timer
| Opcode | Type |
| ------ | ----------- |
| timerAfter | c |
| timerEvery | c |
| timerCancel |   |

#### Dialog
| Opcode | Type |
| ------ | ----------- |
| dialogSetTitle |   |
| dialogSetMessage |   |
| dialogOkButton | c |
| dialogCancelButton | c |
| dialogNeutralButton | c |
| dialogShow |   |

#### mediaplayer component

| Opcode | Type |
| ------ | ----------- |
| mediaplayerCreate |   |
| mediaplayerStart |   |
| mediaplayerPause |   |
| mediaplayerSeek |   |
| mediaplayerGetCurrent | d |
| mediaplayerGetDuration | d |
| mediaplayerIsPlaying | b |
| mediaplayerSetLooping |   |
| mediaplayerIsLooping | b |
| mediaplayerReset |   |
| mediaplayerRelease |   |

#### SoundPool
| Opcode | Type |
| ------ | ----------- |
| soundpoolCreate |   |
| soundpoolLoad | d |
| soundpoolStreamPlay | d |
| soundpoolStreamStop |   |

#### ObjectAnimator
| Opcode | Type |
| ------ | ----------- |
| objectanimatorSetTarget |   |
| objectanimatorSetProperty |   |
| objectanimatorSetValue |   |
| objectanimatorSetFromTo |   |
| objectanimatorSetDuration |   |
| objectanimatorSetRepeatMode |   |
| objectanimatorSetRepeatCount |   |
| objectanimatorSetInterpolator |   |
| objectanimatorStart |   |
| objectanimatorCancel |   |
| objectanimatorIsRunning | b |

#### Firebase Database
| Opcode | Type |
| ------ | ----------- |
| firebaseAdd |   |
| firebasePush |   |
| firebaseGetPushKey | s |
| firebaseDelete |   |
| firebaseGetChildren | c |
| firebaseStartListen |   |
| firebaseStopListen |   |

#### Firebase Auth
| Opcode | Type |
| ------ | ----------- |
| firebaseauthCreateUser |   |
| firebaseauthSignInUser |   |
| firebaseauthSignInAnonymously |   |
| firebaseauthIsLoggedIn | b |
| firebaseauthGetCurrentUser | s |
| firebaseauthGetUid | s |
| firebaseauthResetPassword |   |
| firebaseauthSignOutUser |   |

#### Gyroscope
| Opcode | Type |
| ------ | ----------- |
| gyroscopeStartListen |   |
| gyroscopeStopListen |   |

#### AdMob
| Opcode | Type |
| ------ | ----------- |
| interstitialadCreate |   |
| interstitialadLoadAd |   |
| interstitialadShow |   |

#### Firebase Storage
| Opcode | Type |
| ------ | ----------- |
| firebasestorageUploadFile |   |
| firebasestorageDownloadFile |   |
| firebasestorageDelete |   |

#### Camera
| Opcode | Type |
| ------ | ----------- |
| camerastarttakepicture |   |

#### FilePicker
| Opcode | Type |
| ------ | ----------- |
| filepickerstartpickfiles |   |

#### Requestnetwork
| Opcode | Type |
| ------ | ----------- |
| requestnetworkSetParams |   |
| requestnetworkSetHeaders |   |
| requestnetworkStartRequestNetwork |   |

#### TextToSpeech
| Opcode | Type |
| ------ | ----------- |
| textToSpeechSetPitch |   |
| textToSpeechSetSpeechRate |   |
| textToSpeechSpeak |   |
| textToSpeechIsSpeaking | b |
| textToSpeechStop |   |
| textToSpeechShutdown |   |

#### SpeechToText
| Opcode | Type |
| ------ | ----------- |
| speechToTextStartListening |   |
| speechToTextStopListening |   |
| speechToTextShutdown |   |

#### BluetoothManager
| Opcode | Type |
| ------ | ----------- |
| bluetoothConnectReadyConnection |   |
| bluetoothConnectReadyConnectionToUuid |   |
| bluetoothConnectStartConnection |   |
| bluetoothConnectStartConnectionToUuid |   |
| bluetoothConnectStopConnection |   |
| bluetoothConnectSendData |   |
| bluetoothConnectIsBluetoothEnabled | b |
| bluetoothConnectIsBluetoothActivated | b |
| bluetoothConnectActivateBluetooth |   |
| bluetoothConnectGetPairedDevices |   |
| bluetoothConnectGetRandomUuid | s |

#### LocationManager
| Opcode | Type |
| ------ | ----------- |
| locationManagerRequestLocationUpdates |   |
| locationManagerRemoveUpdates |   |
