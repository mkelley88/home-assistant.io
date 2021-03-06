---
layout: page
title: "TP-Link"
description: "Instructions on how to integrate TP-Link routers into Home Assistant."
date: 2015-06-22 10:30
sidebar: true
comments: false
sharing: true
footer: true
logo: tp-link.png
ha_category: Presence Detection
ha_release: pre 0.7
---


The `tplink` platform allows you to detect presence by looking at connected devices to a [TP-Link](https://www.tp-link.com) device.

Currently supported devices includes the following:

- Archer C7 firmware version 150427
- Archer C9 firmware version 150811
- EAP-225 AP with latest firmware version
- Archer D9 firmware version 0.9.1 0.1 v0041.0 Build 160224 Rel.59129n

<p class='note'>
TP-Link devices typically only allow one login at a time to the admin console.  This component will count towards your one allowed login. Depending on how aggressively you configure device_tracker you may not be able to access the admin console of your TP-Link device without first stopping Home Assistant. Home Assistant takes a few seconds to login, collect data, and log out. If you log into the admin console manually, remember to log out so that Home Assistant can log in again.
</p>

## {% linkable_title Configuration %}

To enable this device tracker, add the following lines to your `configuration.yaml`:

```yaml
# Example configuration.yaml entry
device_tracker:
  - platform: tplink
    host: YOUR_ROUTER_IP
    username: YOUR_ADMIN_USERNAME
    password: YOUR_ADMIN_PASSWORD
```

{% configuration %}
host:
  description: The IP address of your router, e.g., 192.168.1.1.
  required: true
  type: string
username:
  description: The username of an user with administrative privileges, usually *admin*. The Archer D9 last firmware does not require a username.
  required: true
  type: string
password:
  description: The password for your given admin account.
  required: true
  type: string
{% endconfiguration %}

For Archer C9 models running firmware version 150811 or later please use the encrypted password you can retrieve like this:

1. Go to the login page of your router. (default: 192.168.0.1)
2. Type in the password you use to login into the password field.
3. Click somewhere else on the page so that the password field is not selected anymore.
4. Open the JavaScript console of your browser (usually by pressing F12 and then clicking on "Console").
5. Type `document.getElementById("login-password").value;` or `document.getElementById("pcPassword").value;`, depending on your firmware version.
6. Copy the returned value to your Home Assistant configuration as password.

See the [device tracker component page](/components/device_tracker/) for instructions how to configure the people to be tracked.

For Archer D9 model the default ip is 192.168.1.1, the username is not necessary and you can leave that field blank.
