# Connect to HiveMQ Cloud using Python

## Install dependencies

```bash
pip3 install paho-mqtt
```

## Publish a simple message

The following snippet publishes two messages:
- "test 1" under the topic "my test"
- "test 2" under the topic "my test"

Please, use your own `USERNAME`, `PASSWORD` & `HOSTNAME`

```python
import ssl
from paho import mqtt
import paho.mqtt.client as paho
import paho.mqtt.publish as publish

# create a set of 2 test messages that will be published at the same time
msgs = [{'topic': "my test", 'payload': "test 1"}, ("my test", "test 2", 0, False)]

# use TLS for secure connection with HiveMQ Cloud
sslSettings = ssl.SSLContext(mqtt.client.ssl.PROTOCOL_TLS)

# put in your cluster credentials and hostname
auth = {'username': "USERNAME", 'password': "PASSWORD"}
publish.multiple(msgs, hostname="HOSTNAME", port=8883, auth=auth,
                 tls=sslSettings, protocol=paho.MQTTv31)
```

Copy and paste the snippet into a Python file (using the terminal), and execute it:
```bash
python3 my_publisher.py
```

Check those messages appear on the WebClient on your cluster.

>Insert a screenshot of your WebClient here.

## Subscribe to a service

Now, you can also read the messages coming through your cluster. Just use the following snippet:
```python
import ssl
import paho.mqtt.client as paho
import paho.mqtt.subscribe as subscribe
from paho import mqtt


# callback to print a message once it arrives
def print_msg(client, userdata, message):
    """
        Prints a mqtt message to stdout ( used as callback for subscribe )

        :param client: the client itself
        :param userdata: userdata is set when initiating the client, here it is userdata=None
        :param message: the message with topic and payload
    """
    print("%s : %s" % (message.topic, message.payload))


# use TLS for secure connection with HiveMQ Cloud
sslSettings = ssl.SSLContext(mqtt.client.ssl.PROTOCOL_TLS)

# put in your cluster credentials and hostname
auth = {'username': "USERNAME", 'password': "PASSWORD"}
subscribe.callback(print_msg, "#", hostname="HOSTNAME", port=8883, auth=auth,
                   tls=sslSettings, protocol=paho.MQTTv31)
```

- Execute this file on a terminal. Leave it open.
- Execute the previous file on a different terminal.
- Observe the output on the first one.

> Screeshot of both terminal.s