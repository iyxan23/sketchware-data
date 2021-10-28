# Block opcodes
This document contains all of sketchware's blocks' opcodes (version 150)

## Return types
| Return type | Description |
| ----------- | ----------- |
| b           | boolean     |
| s           | String      |
| d           | Decimal     |

## Block categories

### Control flow
| Opcode  | Return type |
| ------- | ----------- |
| repeat  | c           |
| forever | c           |
| break   | f           |
| if      | c           |
| ifElse  | e           |

### Operators
| Opcode | Return type |
| ------ | ----------- |
| true | b |
| false | b |
| < | b |
| URLEncodedUtils.NAME_VALUE_SEPARATOR | b |
| > | b |
| && | b |
| \|\| | b |
| not | b |
| + | d |
| - | d |
| MediaType.WILDCARD | d |
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
| nnotationHandler.STRIN | s |
| toStringWithDecimal | s |
| toStringFormat | s |
| strToMap |   |
| mapToStr | s |
| strToListMap |   |
| listMapToStr | s |
| addSourceDirectly |   |

### Math
| Opcode | Return type |
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
| Opcode | Return type |
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

| Opcode | Return type |
| ------ | ----------- |
| isDrawerOpen | b |
| openDrawer |   |
| closeDrawer |   |

Always on:

| Opcode | Return type |
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

| Opcode | Return type |
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

| Opcode | Return type |
| ------ | ----------- |
| adViewLoadAd |   |

Only if Google Map is enabled:

| Opcode | Return type |
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
| Opcode | Return type |
| ------ | ----------- |
| doToast |   |
| copyToClipboard |   |
| setTitle |   |

#### Intent

| Opcode | Return type |
| ------ | ----------- |
| intentSetAction |   |
| intentSetData |   | 
| intentSetFlags |   |
| startActivity |   |

Only if there are multiple activities:

| Opcode | Return type |
| ------ | ----------- |
| intentSetScreen |   |
| intentPutExtra |   |
| intentGetString | s |
| finishActivity | f |

#### Unknown
| Opcode | Return type |
| ------ | ----------- |
| fileGetData | s |
| fileSetData |   |
| fileRemoveData |   |

#### Calendar
| Opcode | Return type |
| ------ | ----------- |
| calendarGetNow |   |
| calendarAdd |   |
| calendarSet |   |
| calendarFormat | s |
| calendarDiff | d |
| calendarGetTime | d |
| calendarSetTime |   |

#### Vibrator
| Opcode | Return type |
| ------ | ----------- |
| vibratorAction |   |

#### Timer
| Opcode | Return type |
| ------ | ----------- |
| timerAfter | c |
| timerEvery | c |
| timerCancel |   |

#### Dialog
| Opcode | Return type |
| ------ | ----------- |
| dialogSetTitle |   |
| dialogSetMessage |   |
| dialogOkButton | c |
| dialogCancelButton | c |
| dialogNeutralButton | c |
| dialogShow |   |

#### mediaplayer component

| Opcode | Return type |
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
| Opcode | Return type |
| ------ | ----------- |
| soundpoolCreate |   |
| soundpoolLoad | d |
| soundpoolStreamPlay | d |
| soundpoolStreamStop |   |

#### ObjectAnimator
| Opcode | Return type |
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
| Opcode | Return type |
| ------ | ----------- |
| firebaseAdd |   |
| firebasePush |   |
| firebaseGetPushKey | s |
| firebaseDelete |   |
| firebaseGetChildren | c |
| firebaseStartListen |   |
| firebaseStopListen |   |

#### Firebase Auth
| Opcode | Return type |
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
| Opcode | Return type |
| ------ | ----------- |
| gyroscopeStartListen |   |
| gyroscopeStopListen |   |

#### AdMob
| Opcode | Return type |
| ------ | ----------- |
| interstitialadCreate |   |
| interstitialadLoadAd |   |
| interstitialadShow |   |

#### Firebase Storage
| Opcode | Return type |
| ------ | ----------- |
| firebasestorageUploadFile |   |
| firebasestorageDownloadFile |   |
| firebasestorageDelete |   |

#### Camera
| Opcode | Return type |
| ------ | ----------- |
| camerastarttakepicture |   |

#### FilePicker
| Opcode | Return type |
| ------ | ----------- |
| filepickerstartpickfiles |   |

#### Requestnetwork
| Opcode | Return type |
| ------ | ----------- |
| requestnetworkSetParams |   |
| requestnetworkSetHeaders |   |
| requestnetworkStartRequestNetwork |   |

#### TextToSpeech
| Opcode | Return type |
| ------ | ----------- |
| textToSpeechSetPitch |   |
| textToSpeechSetSpeechRate |   |
| textToSpeechSpeak |   |
| textToSpeechIsSpeaking | b |
| textToSpeechStop |   |
| textToSpeechShutdown |   |

#### SpeechToText
| Opcode | Return type |
| ------ | ----------- |
| speechToTextStartListening |   |
| speechToTextStopListening |   |
| speechToTextShutdown |   |

#### BluetoothManager
| Opcode | Return type |
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
| Opcode | Return type |
| ------ | ----------- |
| locationManagerRequestLocationUpdates |   |
| locationManagerRemoveUpdates |   |
