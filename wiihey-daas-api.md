# WiiHey DaaS Platform MQTT API

## Getting Started

### MQTT Basics

[MQTT](https://en.wikipedia.org/wiki/MQTT) is a lightweight publish-subscribe messaging protocol which is probably the most suitable protocol for various IoT use cases. WiiHey DaaS Platform acts as an MQTT Broker over SSL/TLS with predefined topics.

### Client Setup

You can find a large number of MQTT client libraries on the web. The [Sample Project](https://github.com/wiihey/nodejs-mqtt-client-demo) we provided is based on NodeJS and MQTT.js. In order to setup them, follow instructions in the project README.

## Getting Connected

We are using MQTT over SSL/TLS for security concerns, so make sure they are enabled in your MQTT Client. Follow the [Sample Project](https://github.com/wiihey/nodejs-mqtt-client-demo) if your Application Server are based on NodeJS.

```
port: 8883
host: 'iot.wiihey.com'
username: {APP-ID}
password: {APP-KEY}
protocol: "mqtts"
```

## Authentication

We use APP-ID and APP-KEY to identify and authenticate your Application Server. WiiHey Customer Support Team will provide to you these credentials.

## Key Value Format

All messages are Key-Value content in JSON. Key is always string while Value can be string, boolean and number.

For example:
```
{
  "key-1": "a string value",
  "key-2": 123,
  "key-3": true
}
```

### Incoming Message API

To receive message from WiiHey DaaS Platform, Subscribe to the following topic:

```
iot/{APP-ID}/inbox
```

Message looks like:

```
{
   "APP-ID": "xxxxxxxx",
   "DeviceID": "xxxxxxxx",
   "Timestamp": "xxxxxxxxxxx",
   "State": "Device State":
   "IMEI": "xxxxxxxx",
   "CCID": "xxxxxxxx",
   "CSQ": 32,
 }
```

## Keys

### APP-ID

Application Server's ID

### DeviceID

Device's ID. 

### Timestamp

This is the [Unix time](https://en.wikipedia.org/wiki/Unix_time) when the message is arrived at WiiHey DaaS Platform.

### State

Device's State. For Manhole Sensor the states are 'open' and 'close'.

### IMEI

IMEI is a string that identifies the Modem module in the Device.

### ICCID

ICCID is a string that identifies the SIM card.

### CSQ

CSQ is a number that describes the signal strength.

### Examples

#### Manhole cover open

```
{
   "CustomerID": "a6157a33",
   "DeviceID": "5da6f03c",
   "Timestamp": "1529553530",
   "State": "open",
   "IMEI": "351756051523999",
   "ICCID": "89014103243534707921",
   "CSQ": 30
}
```

