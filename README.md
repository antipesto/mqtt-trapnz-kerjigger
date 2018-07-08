TrapNZMQTT
==========

Take MQTT messages from MySensors and post them to api.trap.nz
This is not written or endorsed by Groundspeak or Trap.NZ and is provided as is without warranty or claim to be fit for purpose.

### About

This is a Node Red project to take an MQTT feed containing messages from a door sensor type node based on Mysensors framework and publish heartbeat and state change messages to the Trap.NZ API.

## Usage
Once you have added the contents of Flows-Manager.json into Node-Red, there are a couple of steps to configuration as follows.

### API Credentials 
Open the "Configure" tab and edit the trap.nz credentials node to enter your API credentials. Leave "grant_type":"password" as it is, and change the other credentials with the ones you obtained from trap.nz

```json
{
    "grant_type": "password",
    "client_id": "client id",
    "client_secret": "client secret",
    "username": "user.name",
    "password": "yourpassword"
}
```
Node Red will attempt to store these in a file specified in the save creds node. In the code this is specified as a file path of /etc/trapnz.json but you can change this to whereever is relevant. 

You may need to "touch" an empty file in that location first and chown/chmod the permissions so that NodeRed can write the file.

If you do change the name or location from /etc/trapnz.json you will need to visit the "TrapNZ Oauth" tab and update the file path in the "Read Credentials" node.

### Configure the MQTT feed
Open the "Subscribe Sensors" tab and edit the "Trap-Sprung-Event" node. You will probably need to edit the Server parameter to target your MQTT broker - the default is to use an MQTT broker on the local host.

Take a look at the MQTT Messages comment node at the top, this has some notes about the topics that MySensors uses for a simple reed switch sensor. We are interested in the door tripped and armed messages and also the battery voltage in the heartbeat messages.

Alter the topics if needed in the Trap-Sprung-Event and Trap-Battery-Voltage nodes.

There is a node called "All The Things" which points at a debug node, this is useful for examining all the messages coming from the broker in the topic that its subscribed to and can help inform the correct topics in Trap-Sprung-Event and Trap-Battery-Voltage

## More Information
There are detailed comments in the project itself. At the top of each tab is a comments node with some details about what the nodes in the tab are doing.

More information on the trap.nz api itself is documented at https://api.trap.nz/
