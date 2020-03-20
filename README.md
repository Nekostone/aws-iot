# aws-iot

This repository contains code on how to connect IoT Devices to the AWS IoT Core, based on the (aws-iot-device-sdk-python-v2)[https://github.com/aws/aws-iot-device-sdk-python-v2].

## Setup Instructions

Install necessary packages and root-CA.crt from aws
```bash
./start.sh
```

For a start, run the command to see what kind of parameters are required for the test program `pubsub.py`

```bash
python pubsub.py -h
```

Run it with args as shown below. You can obtain the parameters below when you register a device, please refer to [AWS's IoT Device Registration Interface when logged in](https://us-east-2.console.aws.amazon.com/iot/home?region=us-east-2#/connIntro)

```bash
python pubsub.py --endpoint <ENDPOINT_URL> --cert <DEVICENAME.cert.pem> --key <DEVICENAME.private.key>
```

The result from the test program if you tried with the command above would be
```bash
Connecting to a1746xc73tg6ur-ats.iot.us-east-2.amazonaws.com with client ID 'samples-client-id'...
Connected!
Subscribing to topic 'samples/test'...
Subscribed with QoS.AT_LEAST_ONCE
Sending 3 message(s)
Publishing message to topic 'samples/test': Henlo world [1]
Received message from topic 'samples/test': b'Henlo world [1]'
Publishing message to topic 'samples/test': Henlo world [2]
Received message from topic 'samples/test': b'Henlo world [2]'
Publishing message to topic 'samples/test': Henlo world [3]
Received message from topic 'samples/test': b'Henlo world [3]'
3 message(s) received.
Disconnecting...
Disconnected!
```

To make life simpler, you can also choose to modify any of the default params in the file itself and rerun `python pubsub.py` to test out your registered device. 


## Project Structure

`pubsub.py`
This sample uses the Message Broker for AWS IoT to send and receive messages through an MQTT connection. On startup, 
1. the device connects to the server, 
2. subscribes to a topic, 
3. and begins publishing messages to that topic.
The device should receive those same messages back from the message broker, since it is subscribed to that same topic.