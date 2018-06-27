# MQTT API

## Overview

WiiHey Cloud forwards device's messages to Customer's Application via MQTTS (aka. MQTT over SSL).

## Connection Settings

> port: 8883
> host: 'iot.wiihey.com'
> username: {CustomerID}
> password: {CustomerKey}
> protocol: "mqtts"

The CustomerID and CustomerKey is provided by WiiHey.

## Evaluation Account

A pair of special ID&Key are provided for evaluation purpose:

> CustomerID: eval_id
> CustomerKey: eval_key

## Topics

### Inbox iot/{CustomerID}/inbox

Application subscribes the inbox topic to receive messages from WiiHey Cloud. The Cloud Server will route relevant device's messages to the customer inbox based on routing rules, which are configured before WiiHey ships devices out.

The message's format is:

> {
>   "CustomerID": "xxxxxxxx",
>   "DeviceID": "xxxxxxxx",
>   "Timestamp": "xxxxxxxxxxx", // epoch time in seconds
>   "State": "{open/close/offline}: // The Device's current state. can be "open", "close" or "offline".
>   "IMEI": "xxxxxxxx", // the IMEI string
>   "CCID": "xxxxxxxx", // the CCID string
>   "CSQ": "32", // The Signal Quality
> }

The Cloud sends state == open/close message when someone opens/closes the Manhole Cover. It sends the state == offline message when the Manhole Cover stops sending Keep-Alive token for a long period.

### Examples

#### Manhole cover open

> {
>   "CustomerID": "a6157a33",
>   "DeviceID": "5da6f03c",
>   "Timestamp": "1529553530",
>   "State": "open",
>   "IMEI": "351756051523999",
>   "CCID": "89014103243534707921",
>   "CSQ": "30"
> }

