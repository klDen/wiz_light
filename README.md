# Wiz Light Bulb HASS integration

![Lint](https://github.com/sbidy/wiz_light/workflows/Lint/badge.svg) ![Pylint](https://github.com/sbidy/wiz_light/workflows/Pylint/badge.svg)

### Check out my latest post in the "Dev.-Blog"!!

[Click!!!](https://github.com/sbidy/wiz_light/discussions/78#discussioncomment-406814)

### Thank you for all sponsors and supporter!

## :bulb: wiz_light - [V0.4.5](https://github.com/sbidy/wiz_light/releases/tag/v0.4.5)

One short note: If you have multiple (>5) bulb connected to the HASS, please try to bring all online if you restart the HASS service/container.
Because on older HASS version the startup can be slowed down if multiple bulbs are offline.

## :muscle: Change Log 0.4.5 (possible breaking changes)

- Downstream all changes from the [HASS PR #44779](https://github.com/home-assistant/core/pull/44779). If you receive an error, `wiz_light: no setup was found` you have to update the HASS to the latest version.
- **YAML Config Support is no longer supported!**. Please re-add the bulbs via the UI. Auto-Discover is on the way.
- Colors now correctly calculated and shown
- The MAC for the bulb now displayed in the device info
- In general, multiple improvements and fixes are made
- Sate should be update accordingly

### What is declined or rejected:

- Change of the speed of the transition from on to off and off->on. This is not supported via the UDP API and can only be configured via WiZ App.
- The Motion Sensor is not integrated
- Color saturation is not supported by HASS

### :information_source: [Development Log](https://github.com/sbidy/wiz_light/discussions/78)

Here you can find some news and updates!!
I try to create a kind of Development Log to trace changes/decisions and made the current overall development status transparent to you!!

### :warning: Discussions

If you have questions or other comments please use the **new** [Discussions Board](https://github.com/sbidy/wiz_light/discussions).

## 📔 DNS / IP Address Tip

If you are using DHCP IP address features and looking for avoiding static IPs for the bulb, you can use the DNS names.
To avoid the mess with the IPs you can use the Hostnames of the bulbs.
The hostname will be created from the last 6 digest of the MAC and the `wiz-` prefix. Example: `wiz-123123` or `wiz-123ABC` .
So you can have dynamic IPs, but this hostname will not change. The MAC address you can find in your router or via `nc`.
One of the next versions of this integration will show the MAC in the "Device Properties" tab. Overall, your DNS resolution should work 😉.

## 🔄 Test Connction

To test the connection between the bulb and your Wi-Fi router, you can use the RSSI value.
You can test the [RSSI ](https://en.wikipedia.org/wiki/Received_signal_strength_indication) with this command: `echo '{"method":"getPilot","env":"pro","params":{}}' | nc -u -w 1 <AddressOfYourBulb> 38899`.
If the RSSI value is close to -100 the signal is not that good. Everything between -70 and 0 should be fine.

## :blue_heart: Kudos and contributions

Thank you [@angadsingh](https://github.com/angadsingh) for making such incredible improvements!

Thanks to [@simora](https://github.com/simora) for creating a HA Switch <-> WiZ Plug integration!

Thanks to [@jarpatus](https://github.com/jarpatus) for the feedback and enhancements!

Thanks to [@ChrisLizon](https://github.com/ChrisLizon) for the review, feedbacks and improvements!

Thanks to [@brettonw](https://github.com/brettonw) for improving the RGB-CW to HU tranistion!

Thanks to [@vodovozovge](https://github.com/vodovozovge) for the "insider support" for the community!

## :flight_departure: Dependencies

This component has a dependency on `pywizlight` which will be installed automatically by Home Assistant.

## :zap: Misc

### Bulb Type Definition

```config
e.g. ESP01_SHDW1C_31
ESP01 -- defines the module family (WiFi only bulb in this case)
SH -- Single Head light (most bulbs are single heads) / LED Strip
TW -- Tunable White - can only control CCT and dimming; no color
DW -- Dimmable White (most filament bulbs)
RGB -- Fullstack bulb
1C -- Specific to the hardware - defines PWM frequency + way of controlling CCT temperature
31 -- Related to the hardware revision
```

## Pull request in HA core

[https://github.com/home-assistant/core/pull/44779](https://github.com/home-assistant/core/pull/44779)

## Installation via HACS (Home Assistant Community Store)

[![Hacs Installtion](http://img.youtube.com/vi/_LTA07ENpBE/0.jpg)](http://www.youtube.com/watch?v=_LTA07ENpBE "Wiz Lightbulbs and Home Assistant walkthrough - 2021 Phillips Hue Killer?")

## Install for testing

1. Logon to your HA or HASS with SSH
2. Go to the HA 'custom_components' directory within the HA installation path (The directory is in the folder where the 'configuration.yaml' file is located. If this is not available - create this directory).

4. Run `cd custom_components`
5. Run `git clone https://github.com/sbidy/wiz_light` within the `custom_components` directory
6. Run `mv wiz_light/custom_components/wiz_light/* wiz_light/` to move the files in the correct diretory
7. Restart your HA/HASS service in the UI with `<your-URL>/config/server_control`
8. Add the bulbs either by:
HA UI by navigating to "Integrations" -> "Add Integration" -> "WiZ Light" (If it is not available, clear your web browser cache to renew the integrations list.)

Questions? Check out the github project [pywizlight](https://github.com/sbidy/pywizlight)

## Enable Debug

```YAML
logger:
    default: warning
    logs:
      homeassistant.components.wiz_light: debug
```
