# WiiHey Manhole Cover Sensor Programming Guide

## Introduction

The WiiHey Manhole Cover Sensor is a product of the WiiHey DaaS Product Family. It is a cloud powered device that senses Manhole Cover state and send message to customer's Application Server via MQTT protocol.

## Prerequisites

We will be using WiiHey Manhole Cover Sensor with WiiHey DaaS Platform. So make sure that:

* You have received samples of the WiiHey Manhole Cover Sensor.
* You have setup a Application Server and connected to WiiHey DaaS Platform properly.

Otherwise, checkout following links:

* Product Info: [WiiHey Manhole Cover Sensor] (http://wiihey.com/en/products/wiilsw-manhole-cover-sensor.html)
* Getting Started with Application Server: [Sample Project] (https://github.com/wiihey/nodejs-mqtt-client-demo)
* WiiHey DaaS Platform MQTT API: [MQTT API](https://wiihey.github.io/wiihey-daas-platform-mqtt-api)

Please [Contact Us](http://wiihey.com/en/about.html) for any addtional information.

## Prepare Sensor

You might need to insert a SIM card before you can play with it. Read the [Installation Guide] to get more information.

## Getting Started

Now you have prepared everything needed. If everything goes fine, the WiiHey DaaS Platform will send message via MQTT when you toggle the sensor's state.

Check out the [MQTT API](https://wiihey.github.io/wiihey-daas-platform-mqtt-api) for details about the messages.

## Sensor Behavior

The Sensor will send message in two cases:

* State has changed. aka. Someone opens/closes the Manhole Cover.
* State has not changed for a long while (roughly 3 days). This is to notify the Application Server that the sensor is still working.

## FAQ

### How should Application Server handle those messages?

It is recommended that the Application Server stores the latest known sensor state in a database.

When receiving message from WiiHey DaaS Platform, lookup the record via DeviceID and compare the state. If new state is different, the Application Server will probably notify someone.

### Will the sensor retransmit message in case of failure?

Yes. Sometimes the sensor may encounter errors during communications and it will automatically retransmit up to 3 times. It will not retransmit forever in order not to kill its battery.

However, even all 3 transmission attempts failed, the sensor will still do transmission 3 days later. so sooner or later your Application Server will receive the message.

### How to use DeviceID?

The DeviceID is a simple and short hex string used to identify the sensor. We generally recommend customer to assign an ID for each Manhole Cover and bind the Manhole Cover ID with Manhole Cover Sensor ID.

### Why should I develop my own Application Server?

The WiiHey DaaS Platform is meant to empower customers who can develop software systems. It greatly reduces the complexities of developing a IoT system by hiding all the hassles under a simple and clean [MQTT API](https://wiihey.github.io/wiihey-daas-platform-mqtt-api). When the sensor detects something, you get a MQTT message and that is all.

This product can be potentially integrated into many different software systems (and this is happening right now). so it make most sensor to leave Application Server development to customers.

However, if you want to find someone to develop the Application Server for you or find an existing one to use. Please [Contact Us](http://wiihey.com/en/about.html) and we will find one of our software partners to work with you.

### What if I have more questions?

Feel free to [Contact Us](http://wiihey.com/en/about.html)


