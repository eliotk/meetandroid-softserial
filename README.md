meetandroid-softserial
======================

A modified version of the [Amarino](http://www.amarino-toolkit.net/) MeetAndroid library that includes the ability to use SoftwareSerial for Bluetooth communication as well as perform a Bluetooth module initialization routine. 

The modified version of the MeetAndroid library to allow for using SoftwareSerial with the Bluetooth module came from here:

http://www.double-oops.org/mini-blog/amarinowithsoftwareserial

I have added a new method called "send_plain" that allows plain serial messages to be sent to the Bluetooth module from the sketch. The default send method contained in the original library modifies the input string to communicate with Amarino on the Anrdoid side so it doesn't work for sending initialization commands to the Bluetooth module.

Usage
-----

Declared MeetAnrdoid in the Arduino sketch:

	MeetAndroid meetAndroid(3,2, 57600); // using digital pins 3 (Rx) and 2(Tx) for SoftwareSerial at a baud
										 // rate of 57600

Now you can send Bluetooth configuration commands:

	meetAndroid.send_plain("\r\n+STWMOD=0\r\n"); //set the bluetooth work in slave mode
	meetAndroid.send_plain("\r\n+STNA=SeeedBTSlave\r\n"); //set the bluetooth name as "SeeedBTSlave"
	meetAndroid.send_plain("\r\n+STOAUT=1\r\n"); // Permit Paired device to connect me
	meetAndroid.send_plain("\r\n+STAUTO=0\r\n"); // Auto-connection should be forbidden here
 	meetAndroid.send_plain("\r\n+INQ=1\r\n"); //make the slave bluetooth inquirable