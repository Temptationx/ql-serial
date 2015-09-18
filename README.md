# ql-serial
Serial port access from QML.
Donate: Paypal edartuz@gmail.com


Registration:

```C++
#include "lib/ql-channel-serial.hpp"

qmlRegisterType<QlChannelSerial>("QlChannelSerial", 1,0, "QlChannelSerial");
```


Usage:

```Javascript
import QlChannelSerial 1.0

ApplicationWindow { id:app; visible:true;

	QlChannelSerial { id:serial }

	Component.onCompleted: {
		// open first available port
		serial.open(serial.channels()[0]);

		// if success - configure port parameters
		if (serial.isOpen()){
			serial.paramSet('baud', '9600');
			serial.paramSet('bits', '8');
			serial.paramSet('parity', 'even');
			serial.paramSet('stops', '0');

			serial.paramSet('dtr', '0');
			serial.paramSet('rts', '1');
			
			// write bytes/ASCII string
			serial.writeBytes([1,2,3,4,5]);
			serial.writeString('123456789');
			
			// read received bytes
			var data = serial.readBytes();
		}
	}
}
```

