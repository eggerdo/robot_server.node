# Robot Server

This node provides a Server using ØMQ sockets for command, video and event messages. It uses ZMQ.PULL sockets for incoming messages and ZMQ.PUB sockets for outgoing messages. The main function of the server is to relay messages received on it's incoming sockets to the corresponding outgoing socket, i.e. messages coming in on a command socket are relayed to the outgoing command socket. Thus, the server provides for each command, video and event one incoming (ZMQ.PULL) and one outgoing (ZMQ.PUB) socket.

For video messages, a second outgoing socket is available which publishes video frames encoded as base64.

The format of the command, video and event messages is described in the protocol document [here](https://raw.github.com/eggerdo/RoboTalk-Lib/master/docs/DoBotsZMQMessageProtocoll.pdf).

## Install

1. Since this is a node.js module, it requires that node (>= 0.8) and npm (>= 1.2) are installed. If not, follow the steps descriped [here](https://gist.github.com/isaacs/579814).

2. Install the ØMQ library

    	$ sudo apt-get install libzmq-dev
        
3. Install the robot server. Change to the robot_server.node folder and run

    	$ npm install

## Run

Run the Robot Server by calling

	$ node robot_server

This will use the following ports:

- Video
	- In 4000
	- Out 4001
	- Out (Base64) 4002
- Command
	- In 4010
	- Out 4011
- Event
	- In 4020
	- Out 4021

Alternatively, the incoming ports can be specified as command line arguments `node robot_server.node VIDEO_PORT COMMAND_PORT EVENT_PORT`. The outgoing ports will be set to incoming port + 1 (and incoming port + 2 for Base64 video messages).

	$ node robot_server 5000 5010 5020
