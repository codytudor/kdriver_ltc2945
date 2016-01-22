# LTC2945 Wide Range I2C Power Monitor

The LTC2945 is a rail-to-rail system monitor that measures current, voltage, and power. The IC
provides an additional ADC input for external voltage measurments as well. This driver provides
sysfs entries in the hwmon class for accessing all of the registers in this device. 

Sysfs entries
-------------

Voltage readings provided by this driver are reported as obtained from the ADC
registers. If a set of voltage divider resistors is installed, calculate the
real voltage by multiplying the reported value with (R1+R2)/R2, where R1 is the
value of the divider resistor against the measured voltage and R2 is the value
of the divider resistor against Ground.

Current reading provided by this driver is reported as obtained from the ADC
Current Sense register. The reported value assumes that a 1 mOhm sense resistor
is installed. If a different sense resistor is installed, calculate the real
current by dividing the reported value by the sense resistor value in mOhm.

You can explicitly instantiate a device like the following example:

This will load the driver for an LTC2945 with I2C address 0x20 on I2C bus #1:
```
    $ modprobe ltc2945
    $ echo ltc2945 0x10 > /sys/bus/i2c/devices/i2c-1/new_device
``` 
    
Or you can statically define a sensor with given address using the OF subsystem.

An example device tree entry would be:

    dev_name {
        compatible = "ltc2945";
        reg = <0x10>;
    }; 

* @dev_name: this is the actual dev name that will be given to this sysfs entry in the hwmon class
* @compatible: this is used to probe the sensor driver using OF properties
* @reg: hexadecimal address of the sensor i.e. (address = 0xce) -> (reg = address >> 1)


In the example above the device will appear as a client of the i2c bus node
the phandle was defined under. 
