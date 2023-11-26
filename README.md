# homebridge-tapo-camera

Make your TP-Link TAPO security camera compatible with Homekit through Homebridge / HOOBS.

[![verified-by-homebridge](https://badgen.net/badge/homebridge/verified/purple)](https://github.com/homebridge/homebridge/wiki/Verified-Plugins)

![photo_2021-11-23 11 57 48](https://user-images.githubusercontent.com/839700/143013358-9f6eed44-3aad-40b0-b1e5-ddc2c5bb24e4.png)

The plugin exposes the camera RTSP video feed, 2 accessories to control "Privacy Mode" and "Alarm" and a motion detection accessory.

The accessory called _"Eyes"_ controls the privacy mode; when it's on it means that the camera is able to see
(this is to make sure we support the command "Hey Siri, turn _on_ Camera", as this will _disable_ privacy mode and enable alarm).

The accessory called _"Alarm"_ switches on/off the alarm sound, but keep in mind that notifications will still be sent to the phone.

The motion detection is built on top of the ONVIF protocol and it is enabled by default; therefore you can set up
automations and Homekit can send you notification when motion is detected.

## Installation

You can install it via Homebridge UI or manually using:

```sh
npm -g install homebridge-tapo-camera
```

### Configuration

It is highly recommended that you use either Homebridge Config UI X or the HOOBS UI to install and configure this plugin.

### Adding the unbridged accessory to Home

Once done you will have unbridged accessories, therefore you need to manually add them in your Home app.

### Manual configuration

If you want to have manual control over the configuration, add the following configuration in the `platforms` key:

```json5
{
  // ...
  platforms: [
    // Other platforms
    {
      // Note, if you've upgraded the plugin and you have no more camera in the Home app, you need to change this to "tapo-camera" lowercase (before v1.6.2 it was "TAPO-CAMERA")
      platform: "tapo-camera",
      cameras: [
        {
          name: "Adamo",

          ipAddress: "__IP_ADDRESS__",
          password: "__PASSWORD__",
          streamPassword: "__STREAM_PASSWORD__", // This must be only alphanumeric [A-Za-z0-9], no special characters allowed!
          streamUser: "__STREAM_USER__", // This must be only alphanumeric [A-Za-z0-9], no special characters allowed!

          // An object containing a video-config passed to camera-ffmpeg
          // Please check https://www.npmjs.com/package/homebridge-camera-ffmpeg for all the possible values\
          // Make sure you don't override default values provided by this plugin unless you know what you're doing!
          videoConfig: {}
      ],
    },
  ],
}
```

- `__IP_ADDRESS__` is the IP address of the camera in your local network; as long you have a bridge setup, you can also fully control the camera outside your Home.
- `__PASSWORD__` is the password of your TAPO Cloud account, the username/email is not needed.
- `__STREAM_USER__` and `__STREAM_PASSWORD__` are the credentials you set in Settings > Advanced Settings > Camera Account.
