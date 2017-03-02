# Sensibility API functions

This documents describes the function calls specific to the Sensibility Testbed
Sandbox. For the general Repy API (Repy is the programming language available to
the Sensibility Testbed Sandbox) check out the [Repy V2 Library Reference](https://github.com/SeattleTestbed/docs/blob/master/Programming/RepyV2API.md)
and the [RepyV2 Tutorial](https://github.com/SeattleTestbed/docs/blob/master/Programming/RepyV2Tutorial.md).

Note that some of the following functions might not be available on your
Android device.

## Overview
__Sensor functions__
- [get_sensor_list()](#get_sensor_list)
- [get_acceleration()](#get_acceleration)
- [get_ambient_temperature()](#get_ambient_temperature)
- [get_game_rotation_vector()](#get_game_rotation_vector)
- [get_geomagnetic_rotation_vector()](#get_geomagnetic_rotation_vector)
- [get_gravity()](#get_gravity)
- [get_gyroscope()](#get_gyroscope)
- [get_gyroscope_uncalibrated()](#get_gyroscope_uncalibrated)
- [get_heart_rate()](#get_heart_rate)
- [get_light()](#get_light)
- [get_linear_acceleration()](#get_linear_acceleration)
- [get_magnetic_field()](#get_magnetic_field)
- [get_magnetic_field_uncalibrated()](#get_magnetic_field_uncalibrated)
- [get_pressure()](#get_pressure)
- [get_proximity()](#get_proximity)
- [get_relative_humidity()](#get_relative_humidity)
- [get_rotation_vector()](#get_rotation_vector)
- [get_step_counter()](#get_step_counter)

__Location functions__
- [get_location()](#get_location)
- [get_lastknown_location()](#get_lastknown_location)
- [get_geolocation(latitude, longitude, max_results)](#get_geolocation)

__Media functions__
- [tts_speak(message)](#tts_speak)
- [microphone_record(file_name, duration)](#microphone_record)
- [is_media_playing()](#is_media_playing)
- [is_tts_speaking()](#is_tts_speaking)

__Miscellaneous functions__
- [get_bluetooth_info()](#get_bluetooth_info)
- [get_bluetooth_scan_info()](#get_bluetooth_scan_info)
- [is_wifi_enabled()](#is_wifi_enabled)
- [get_wifi_state()](#get_wifi_state)
- [get_wifi_connection_info()](#get_wifi_connection_info)
- [get_wifi_scan_info()](#get_wifi_scan_info)
- [get_network_info()](#get_network_info)
- [get_cellular_provider_info()](#get_cellular_provider_info)
- [get_cell_info()](#get_cell_info)
- [get_sim_info()](#get_sim_info)
- [get_phone_info()](#get_phone_info)
- [get_mode_settings()](#get_mode_settings)
- [get_display_info()](#get_display_info)
- [get_volume_info()](#get_volume_info)
- [get_battery_info()](#get_battery_info)

__Functions for User Interaction__
- [android_log(message)](#android_log)
- [toast(message)](#toast)
- [prompt(message)](#prompt)
- [notify(message)](#notify)

## Detailed Description

### Sensor functions
The sensor functions available to Sensibility rely on the sensor functions
available in Android. Most of the function descriptions are taken verbatim
from the Android documentation. For more information about sensors in Android
check out the [Android documentation](https://source.android.com/devices/sensors/sensor-types.html).

Note: Many of the sensor function have an event time as first item in the
returned data. This is the time when the device received received an update for
the returned sensor reading in seconds relative to your programs start time.

#### get_sensor_list()
----
Get a list of all available sensors on your device with per sensor information.

##### Returns
List of dictionaries with sensor information.

##### Example
```python
>>> get_sensor_list()
[{ "max_range": 100, "vendor": "Sensortek", "name": "STK3310 Proximity sensor", "power": 3, "fifo_reserved_event_count": 0, "is_wakeup_sensor": True, "fifo_max_event_count": 0, "string_type": "android.sensor.proximity", "max_delay": 0, "reporting_mode": 1, "version": 1, "type": 8, "resolution": 100, "min_delay": 0}, ... ]
```

#### get_acceleration()
----
An accelerometer sensor reports the acceleration of the device along the 3
sensor axes. The measured acceleration includes both the physical acceleration
(change of velocity) and the gravity.
All values are in SI units (m/s^2) and measure the acceleration of the device
minus the force of gravity along the 3 sensor axes.

The readings are calibrated using: temperature compensation, online bias
calibration, online scale calibration.

##### Returns
List containing event time and acceleration force along the x, y and z axes

##### Example
```python
>>> get_acceleration()
[3.3610000000000002, -0.1340179443359375, -0.2076416015625, 9.9420013427734375]
```

#### get_ambient_temperature()
----
This sensor provides the ambient (room) temperature in degrees Celsius.
##### Returns
Degrees Celsius

```python
>>> get_ambient_temperature()
22.6621284485
```

#### get_game_rotation_vector()
----
A game rotation vector sensor is similar to a rotation vector sensor but not
using the geomagnetic field. Therefore the Y axis doesn't point north but
instead to some other reference. That reference is allowed to drift by the same
order of magnitude as the gyroscope drifts around the Z axis.

##### Returns
List containing event time and rotation vector values along x, y, z axes
(axis * sin(θ/2) and rotation angle cos(θ/2)

##### Example
```python
>>> get_game_rotation_vector()
[23.927, -0.0007171630859375, -0.0029296875, -0.9038848876953125, 0.4277801513671875]
```

#### get_geomagnetic_rotation_vector()
----
A geomagnetic rotation vector is similar to a rotation vector sensor but using
a magnetometer and no gyroscope.

##### Returns
List containing event time and rotation vector values along x, y, z axes
(axis * sin(θ/2) and rotation angle cos(θ/2)

##### Example
```python
>>> get_geomagnetic_rotation_vector()
[23.90, -0.0003204345703125, -0.002471923828125, -0.6276397705078125, 0.77850341796875, 0]
```

#### get_gravity()
----
A gravity sensor reports the direction and magnitude of gravity in the device's
coordinates.

If the device possesses a gyroscope, the gravity sensor must use the gyroscope
and accelerometer as input.

If the device doesn't possess a gyroscope, the gravity sensor must use the
accelerometer and the magnetometer as input.

##### Returns
List containing event time and gravity vector values (m/s^2) in the x, y and z
fields of the acceleration

##### Example
```python
>>> get_gravity()
[23.927, 0.036956787109375, 0.0456390380859375, 9.8063507080078125]
```

#### get_gyroscope()
----
A gyroscope sensor reports the rate of rotation of the device around the 3
sensor axes.

Rotation is positive in the counterclockwise direction (right-hand rule).
That is, an observer looking from some positive location on the x, y or z axis
at a device positioned on the origin would report positive rotation if the
device appeared to be rotating counter clockwise. Note that this is the
standard mathematical definition of positive rotation and does not agree with
the aerospace definition of roll.

The readings are calibrated using, temperature compensation,
factory (or online) scale compensation, online bias calibration
(to remove drift).

##### Returns
List containing event time and X, Y and Z in radians per second (rad/s)

##### Example
```python
>>> get_gyroscope()
[27.061, -0.00061086524510756135, -0.0036651915870606899, -0.025656340643763542]
```

#### get_gyroscope_uncalibrated()
An uncalibrated gyroscope reports the rate of rotation around the sensor axes
without applying bias compensation to them, along with a bias estimate.
All values are in radians/second and are reported in the fields.

##### Returns
List containing event time and angular speed (w/o drift compensation) around
X, Y and Z axes, and estimated drift around X, Y and Z axis

##### Example
```python
>>> get_gyroscope_uncalibrated()
[27.847, 0.0097738439217209816, -0.0097738439217209816, 0.0085521135479211807, 0.011301007121801376, -0.0085521135479211807, 0.034513887017965317]
```

#### get_heart_rate()
----
A heart rate sensor reports the current heart rate of the person touching the
device.

##### Returns
Heart rate in beats per minute (BPM)

##### Example
```python
>>> get_heart_rate()
70
```

#### get_light()
----
A light sensor reports the current illumination in SI lux units.

##### Returns
Illumination in SI lux units

##### Example
```python
>>> get_light()
103
```

#### get_linear_acceleration()
----
A linear acceleration sensor reports the linear acceleration of the device in
the sensor frame, not including gravity.

The output is conceptually the output of the accelerometer minus the output of
the gravity sensor. It is reported in m/s^2 in the x, y and z fields of the
acceleration vector.

Readings on all axes should be close to 0 when the device is immobile.

If the device possesses a gyroscope, the linear acceleration sensor must use
the gyroscope and accelerometer as input.

If the device doesn't possess a gyroscope, the linear acceleration sensor must
use the accelerometer and the magnetometer as input.

##### Returns
A list containing event time and X, Y and Z in m/s^2 of the acceleration vector

##### Example
```python
>>> get_linear_acceleration()
[23.927, 0.061187744140625, 0.074066162109375, 0.0697174072265625]
```

#### get_magnetic_field()
----
A magnetic field sensor (also known as magnetometer) reports the ambient
magnetic field, as measured along the 3 sensor axes.

The readings are calibrated using, temperature compensation, factory (or online)
soft-iron calibration and online hard-iron calibration.

##### Returns
A list containing event time and magnetic field vector values along X, Y, Z axes in micro-Tesla (uT)

##### Example
```python
>>> get_magnetic_field()
[29.628, -51.126998901367188, -162.73100280761719, -45.080001831054688]
```
#### get_magnetic_field_uncalibrated()
----
An uncalibrated magnetic field sensor reports the ambient magnetic field
together with a hard iron calibration estimate. Values are in micro-Tesla (uT).

##### Returns
A list containing event time and magnetic field (w/o hard-iron compensation) along X, Y, Z axes and
estimated hard-iron bias along X, Y, Z axes

##### Example
```python
>>> get_magnetic_field_uncalibrated()
[23.920, -59.91668701171875, 9.1705322265625, -89.7186279296875, -24.712890625, 1.043701171875, -78.17840576171875]
```

#### get_pressure()
----
A pressure sensor (also known as barometer) reports the atmospheric pressure in
hectopascal (hPa).

The readings are calibrated using, temperature compensation, factory bias
calibration and factory scale calibration.

The barometer is often used to estimate elevation changes. To estimate absolute
elevation, the sea-level pressure (changing depending on the weather) must
be used as a reference.

##### Returns
Atmospheric pressure in hPa (millibar)

##### Example
```python
>>> get_pressure()
[23.585, 985.56365966796875, 0, 0]
```

#### get_proximity()
----
A proximity sensor reports the distance from the sensor to the closest visible
surface.

##### Returns
Distance in centimeters to closest visible surface

##### Example
```python
>>> get_proximity()
5.00
```

#### get_relative_humidity()
----
A relative humidity sensor measures relative ambient air humidity and returns
a value in percent.

##### Returns
Relative ambient air humidity in percent

##### Example
```python
>>> get_relative_humidity()
50.4251441956
```

#### get_rotation_vector()
----
A rotation vector sensor reports the orientation of the device relative to
the East-North-Up coordinates frame. It is usually obtained by integration of
accelerometer, gyroscope, and magnetometer readings.
The East-North-Up coordinate system is defined as a direct orthonormal
basis where X points east and is tangential to the ground, Y points north and is
tangential to the ground and Z points towards the sky and is perpendicular to
the ground.

The orientation of the phone is represented by the rotation necessary to align
the East-North-Up coordinates with the phone's coordinates. That is,
applying the rotation to the world frame (X, Y, Z) would align them with
the phone coordinates (x, y, z).

The rotation can be seen as rotating the phone by an angle theta around an axis
rot_axis to go from the reference (East-North-Up aligned) device orientation to
the current device orientation.

The rotation vector (list) is encoded as the four unit-less
x, y, z, w components of a unit quaternion.

##### Returns
A list containing event time and rotation vector values along x, y, z axes (axis * sin(θ/2), and rotation
angle cos(θ/2)

##### Example
```python
>>> get_rotation_vector()
[31.649, 0.017976691946387291, 0.030638189986348152, -0.98753070831298828, 0.15336622297763824, 0]

```

#### get_step_counter()
----
A step counter reports the number of steps taken by the user since the last
reboot while activated.

The step counter detect when the user is walking, running and walking up the
stairs. It should not trigger when the user is biking, driving or in other
vehicles.

##### Returns
Step count

##### Example
```python
>>> get_step_counter()
100
```


## Location functions
Check out the [Android Documentation](https: //developer.android.com/training/location/index.html)
for more information about location functions.

#### get_location()
----
Returns last location update received by SensibilityApp for all available
location providers: network, gps and fused.

##### Returns
A dictionary with location providers as keys and location info dictionaries
as values

##### Example
```python
>>> get_location()
{"fused": {"bearing": 0, "altitude": 0, "longitude": -73.987226800000002, "time_sample": 1467211033628, "time_polled": 1467211037064, "latitude": 40.691905499999997, "speed": 0, "accuracy": 699.9990234375 , "network": {"bearing": 0, "altitude": 0, "extras": {"travelState": "stationary", "nlpVersion": 2021, "networkLocationType": "cell"}, "longitude": -73.987226800000002, "time_sample": 1467211033628, "time_polled": 1467211037030, "latitude": 40.691905499999997, "speed": 0, "accuracy": 699.9990234375 }, "gps": {"bearing": 0, "altitude": 129, "extras": {"satellites": 8}, "longitude": -73.985975449999998, "time_sample": 1466541236000, "time_polled": 1467211037029, "latitude": 40.692894889999998, "speed": 0, "accuracy": 44}}
```

#### get_lastknown_location()
----
Returns last location update received by the device (e.g. by another App)
for all available location providers: network, gps and fused.

##### Returns
A dictionary with location providers as keys and location info dictionaries
as values

##### Example
```python
>>> get_lastknown_location()
{"fused": {"bearing": 0, "altitude": 115, "longitude": 0.0000201999999998, "time_sample": 1487932931311L, "time_polled": 1487932931312L, "latitude": 00.000963700000003, "speed": 0, "accuracy": 11}, "network": {"bearing": 0, "time_sample": 1487932917996L, "altitude": 0, "longitude": 0.0000627999999996, "extras": {"travelState": "stationary", "networkLocationType": "wifi", "nlpVersion": 2023, "com.qualcomm.location.nlp: ready": True}, "time_polled": 1487932931306L, "latitude": 00.000037700000001, "speed": 0, "accuracy": 19.448999404907227}, "gps": {"bearing": 0, "time_sample": 1487932931000L, "altitude": 115, "longitude": 0.0000202399999996, "extras": {"satellites": 6}, "time_polled": 1487932931305L, "latitude": 00.000063649999999, "speed": 0, "accuracy": 11}}
```

#### get_geolocation(latitude, longitude, max_results)
----
Returns at most a specified amount (max_results) of address information for a
given Location (Latitude and Longitude).

This process is called reverse geo coding and requires an Internet connection
and a connection to Google Play Service API.

##### Arguments
Latitude (float), Longitude (float), Desired max results (int)

##### Returns
A list of address info dictionaries for the passed location.

##### Example
```python
>>> get_geolocation(40.692, -73.986, 2)
[{"thoroughfare": "Jay St", "lines": ["375 Jay St", "Brooklyn, NY 11201"], "admin_area": "New York", "feature_name": "375", "country_code": "US", "country_name": "United States", "postal_code": "11201", "sub_locality": "Brooklyn", "sub_thoroughfare": "375"}, {"locality": "Brooklyn", "lines": ["Downtown Brooklyn", "Brooklyn, NY"], "sub_admin_area": "Kings County", "admin_area": "New York", "feature_name": "Downtown Brooklyn", "country_code": "US", "country_name": "United States", "sub_locality": "Downtown Brooklyn"}]
```



## Media functions

#### tts_speak(message)
----
Takes a String and synthesizes it to speech using the TTS default engine of
the device. This is a non-blocking operation, i.e. it might return before
text was synthesized.
##### Arguments
Text to synthesize (str)

##### Example
```python
>>> tts_speak("Cackle cackle cackle")
# Device cackling ... (non-blocking)
```

#### ~~microphone_record(file_name, duration)~~ *(currently disabled)*
----
~~Records from the default microphone to a file at passed "file_name" for a given
"duration" (ms). This is a blocking operation.~~

##### ~~Arguments~~
~~File name (str) to record to and duration (int) to record for~~

##### ~~Example~~
```python
>>> microphone_record("cackle_cackle.mp4", 10)
# Record from microphone to file "cackle_cackle.mp4" for 10 seconds (blocking)
```

#### is_media_playing()
----
Find out if any App on the device is currently playing audio.
##### Returns
True if audio is playing and False otherwise
##### Example
```python
>>> is_media_playing()
True
```

#### is_tts_speaking()
----
Find out if text is currently being synthesized or in the queue waiting to
be synthesized.

##### Returns
True if text is being synthesized (or in the queue) and False otherwise

##### Example
```python
>>> is_tts_speaking()
True # Assuming that your device is still cackling your TTS from above
```





## Miscellaneous functions

#### get_bluetooth_info()
----
Get information about device's Bluetooth interface.

##### Returns
A dictionary with Bluetooth interface information

##### Example
```python
>>> get_bluetooth_info()
{"local_address": "02:00:00:...", "local_name": "XT1064", "scan_mode": 21, "state": 12}
```

#### get_bluetooth_scan_info()
----
Runs a Bluetooth discovery and returns information about surrounding Bluetooth
devices.

##### Returns
A list of dictionaries of information about surrounding Bluetooth devices

##### Example
```python
>>> get_bluetooth_scan_info()
[{"address": "76:78:58:...", "bond_state": 10, "type": 2}, {"address": "49:BD:52:...", "bond_state": 10, "type": 2}]
```

#### is_wifi_enabled()
----
Find out whether the device's WiFi interface is currently enabled.

##### Returns
True if the device's WiFi interface is enabled, False otherwise

##### Example
```python
>>> is_wifi_enabled()
True
```

#### get_wifi_state()
----
Get the WiFi enabled state.

##### Returns
An int, one of 0 (disabling), 1 (disabled), 2 (enabling), 3 (enabled), 4 (unknown)

##### Example
```python
>>> get_wifi_state()
3
```
#### get_wifi_connection_info()
----
Get information about the WiFi network the device is currently connected to.

##### Returns
A dictionary of information about the WiFi the device is connected to

##### Example
```python
>>> get_wifi_connection_info()
 {"ssid": "...", "bssid": "1c:1d:86:...", "network_id": 0, "supplicant_state": "COMPLETED", "link_speed": 72, "frequency": 2437, "mac_address": "02:00:00:...", "rssi": -57, "ip_address": 1544822444, "hidden_ssid": false}
```

#### get_wifi_scan_info()
----
Runs a WiFi scan and returns info's about surrounding WiFi networks.

##### Returns
List of dictionaries of information about discovered WiFi networks

##### Example
```python
>>> get_wifi_scan_info()
[{"rssi": -57, "frequency": 2437, "ssid": "...", "bssid": "1c:1d:86:...", "capabilities": "[ESS]"}, {"rssi": -47, "frequency": 2437, "ssid": "...", "bssid": "64:e9:50:...", "capabilities": "[WPA2-EAP-CCMP][ESS]"}, {"rssi": -45, "frequency": 2427, "ssid": "...", "bssid": "18:d6:c7:...", "capabilities": "[WPA-PSK-CCMP+TKIP][WPA2-PSK-CCMP+TKIP][WPS][ESS]"}]

```
#### get_network_info()
----
Gets information about surrounding networks (WiFi, GPRS, UMTS, etc...)

##### Returns
A list of dictionaries of information of surrounding networks

##### Example
```python
>>> get_network_info()
[{"is_failover": false, "type": 1, "type_name": "WIFI", "detailed_state": "CONNECTED", "state": "CONNECTED", "subtype_name": "", "subtype": 0, "is_roaming": false, "is_available": true, "is_connected_or_connecting": true, "is_connected": true, "extra_info": "\"nyuguest\""}]
```

#### get_cellular_provider_info()
----
Get information about the device's cellular provider.

##### Returns
A dictionary containing information about the cellular provider

##### Example
```python
>>> get_cellular_provider_info()
{"network_operator_name": "AT&T", "network_operator": "310410"}
```

#### get_cell_info()
----
Get all observed cell information from all radios on the device including the
primary and neighboring cells.

Returned items differ across network types (CDMA, LTE, GSM, WCDMA).

##### Returns
A list of dictionaries of information about observed cells

##### Example
```python
>>> get_cell_info()
[{"mnc": 410, "dbm": -89, "cid": 166524355, "psc": 54, "level": 4, "mcc": 310, "lac": 11939, "is_registered": true, "asu_level": 12}, {"mnc": 2147483647, "dbm": -101, "cid": 2147483647, "psc": 54, "level": 2, "mcc": 2147483647, "lac": 2147483647, "is_registered": false, "asu_level": 6}]
```

#### get_sim_info()
----
Get information about the Subscriber Identity Module (SIM)
##### Returns
A dictionary of SIM information
##### Example
```python
>>> get_sim_info()
{"SIM_country_code": "de", "SIM_operator_name": "", "SIM_operator": "26207", "SIM_serial_number": "nope", "SIM_state": 5}
```

#### get_phone_info()
----
Get information about the telephone.

##### Returns
A dictionary of information about the telephone

##### Example
```python
>>> get_phone_info()
{"phone_type": 1, "subscriber_id": "310410890286033", "data_activity": 0, "call_state": 0, "data_state": 0, "device_software_version": "04", "network_type": 13, "device_id": "356266070625857"}
```

#### get_mode_settings()
----
Get information about ringer and airplane mode.

##### Returns
A dictionary with information about the device's current airplane and ringer mode

##### Example
```python
>>> get_mode_settings()
{"airplane_mode": False, "ringer_mode": 1}
```

#### get_display_info()
----
Get information about the device's display.

##### Returns
A dictionary with information about the device's display

##### Example
```python
>>> get_display_info()
{"name": "Built-in Screen", "brightness_mode": "0", "brightness": "255", "state": 2, "size_x": 480, "size_y": 800, "timeout": "30000", "rotation": 0}
```

#### get_volume_info()
----
Returns information about the device's current and maximal media and ringer volume.

##### Returns
A dictionary with volume information

##### Example
```python
>>> get_volume_info()
{"max_media_volume": 15, "media_volume": 0, "max_ringer_volume": 15, "ringer_volume": 0}
```

#### get_battery_info()
----
Get information about the device's battery

##### Returns
A dictionary with battery information

##### Example
```python
>>> get_battery_info()
{"status": 3, "temperature": 257, "level": 99, "battery_present": True, "plugged": 2, "health": 2, "voltage": 4186, "technology": "Li-ion"}
```

## Functions for User Interaction

#### android_log(message)
----
Log a message to the device's system log.

You can use Android Studio's logcat or the command line utility `adb logcat`
to read the log, providing that your device is connected to a computer and has
USB debugging enabled.

##### Arguments
The message to log (str)

##### Example
```python
>>> android_log("You can read this text using e.g. `adb logcat`")
```

#### toast(message)
----
Write a message to the device's Graphical User Interface.
##### Arguments
The message to toast (str)

##### Example
```python
>>> toast("This message will appear on the device UI for ~3 seconds")
```

#### prompt(message)
----
Prompt for user input. The prompt will be displayed on the device's graphical
user interface. The function only returns after the user has tapped
either Yes or No.

##### Arguments
The message to pompt (str)

##### Returns
True if the user tapped "Yes", False otherwise

##### Example
```python
>>> prompt("Do you like me (no maybe)?")
# Prompts the user with a Yes/No dialog
```

#### notify(message)
----
Write a message to the device's notification drawer. The message will be
truncated to the width of the device's screen.

##### Arguments
The message to send to the notification drawer (str)

##### Example
```python
>>> notify("This message should be shor...")
```