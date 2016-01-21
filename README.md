# LTC2945 Wide Range I2C Power Monitor



An example device tree entry would be:

    dev_name {
        compatible = "ltc2945";
        reg = <0x10>;
    }; 

* @dev_name: this is the actual dev name that will be given to this sysfs entry in the hwmon class
* @compatible: this is used to probe the sensor driver using OF properties
* @reg: hexadecimal address of the sensor


In the example above 
