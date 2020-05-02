# CCS811 Driver for C

Originally designed and created for [UMass ECE Senior Design Project Team 03 Weatherbox](http://www.ecs.umass.edu/ece/sdp/sdp20/team03/).

Based off the [Bosch BME280 C Driver](https://github.com/BoschSensortec/BME280_driver).

## What's Included

### ccs8111_defs.h

* Includes `#define`s for any major addresses, length, sensor operation modes, bit masks, etc.

* Includes type definitions for function pointers for reading, writing, and delaying.
  
* Includes struct definitions for

  * Measurement Data (eCO2, tvoc, status, error_id, raw_data)
  
  * Threadhold Registers (low, high and hysteresis)
  
  * Raw Data (current, and raw ADC reading)
  
  * Environmental Data (humidity percentage & fraction, temperature percentage and fraction)
  
  * NTC Data Register (Voltage across R_ref and R_ntc)
  
  * Firmware Boot Version (Major, Minor, and Trivial version numbers)
  
  * Firmware App Version  (Major, Minor, and Trivial version numbers)
  
  * CCS811 Device Struct
  
    * Hardware ID

    * Hardware Version

    * Device Address

    * Status Register

    * Measurement Mode Register

    * Error Register

    * CCS811 Function Pointer for Reading

    * CCS811 Function Pointer for Writing

    * CCS811 Function Pointer for Delaying

### ccs811.h & ccs811.c

 * ccs811_init - Initialization

    * Takes in a pointer to the CCS811 device struct as an argument.

    * Goes through initialization process for CCS811 driver.

    * Attempts each portion of the process 5 times before running resulting error code.

 * ccs811_set_regs - Set Registers

    * Takes in a pointer to the internal CCS811 register address, a pointer to the data to write to the register, the length of the data, and a pointer to the CCS811 device struct as arguments.

    * Writes data to the specified internal CCS811 register address. Returns 0 on success. Other codes mean error.

 * ccs811_read_regs - Read Registers

    * Takes in a pointer to the internal CCS811 register address, a pointer to the data buffer to store the data, the length of the data, and a pointer to the CCS811 device struct as arguments.

    * Reads data from the specified internal CCS811 register address to the data buffer. Returns 0 on success. Other codes mean error.

 * ccs811_read_status_reg - Read Status Register

    * Takes in a pointer to the CCS811 device struct as an argument.

    * Utilizes ccs811_read_regs to read from status register into the CCS811 device structs status register.

 * ccs811_read_meas_mode_reg - Read Measurement Mode Register

    * Takes in a pointer to the CCS811 device struct as an argument.

    * Utilizes ccs811_read_regs to read from the measurement mode register into the CCS811 device structs measurement mode register.

 * ccs811_set_meas_mode_reg - Set Measurement Mode Register

    * Takes in a pointer to the CCS811 device struct as an argument.

    * Utilizes ccs811_read_regs to read from the measurement mode register into the CCS811 device structs measurement mode register.

 * ccs811_read_alg_result_data - Reads Algorithm Result Data Registers

    * Takes in a pointer to the CCS811 measurement data struct, and a pointer to the CCS811 device struct as arguments.

    * Utilizes ccs811_read_regs to read from the Algorithm Result Data register.

    * Formats and places data into the algorithm data struct.

 * ccs811_read_raw_data - Reads Raw Data Registers

    * Takes in a pointer to the CCS811 raw data struct, and a pointer to the CCS811 device struct as arguments.

    * Utilizes ccs811_read_regs to read from the Raw Data register.

    * Formats and places data into the raw data struct.

 * ccs811_set_env_data - Set Environmental Data Register

    * Takes in a pointer to the CCS811 environmental data struct, and a pointer to the CCS811 device struct as arguments.

    * Utilizes ccs811_set_regs to write to the Environmental Data register.

    * Formats the data from the environmental data struct into a buffer for writing.

 * ccs811_read_ntc - Read NTC Register

    * Takes in a pointer to the CCS811 NTC struct, and a pointer to the CCS811 device struct as arguments.

    * Utilizes ccs811_read_regs to read from the NTC register.

    * Formats read data into the NTC struct.

 * ccs811_set_threshold_reg - Set Threshold Register

    * Takes in a pointer to the CCS811 threshold struct, and a pointer to the CCS811 device struct as arguments.

    * Utilizes ccs811_set_regs to write to the Threshold register.

    * Formats threshold data into buffer for writing.

 * ccs811_read_baseline_reg - Read Baseline Register

    * Takes in a pointer to a 16 bit integer as the baseline, and a pointer to the CCS811 device struct as arguments.

    * Utilizes ccs811_read_regs to read from the Baseline register.

    * Formats baseline data into the 16 bit integer.

 * ccs811_set_baseline_reg - Set Baseline Register
 
    * Takes in a pointer to a 16 bit integer as the baseline, and a pointer to the CCS811 device struct as arguments.

    * Utilizes ccs811_set_regs to write to the Threshold register.

    * Formats baseline data into buffer for writing.

 * ccs811_read_hw_id - Read Hardware ID Register

    * Takes in a pointer to the CCS811 device struct as the argument.

    * Utilizes ccs811_read_regs to read from the hardware ID register.

 * ccs811_read_hw_version - Read Hardware Version Register

    * Takes in a pointer to the CCS811 device struct as the argument.

    * Utilizes ccs811_read_regs to read from the hardware version register.

    * Formats data into the hw_version struct.

 * ccs811_read_fw_boot_version - Read Firmware Boot Version Register

    * Takes in a pointer to the CCS811 device struct as the argument.

    * Utilizes ccs811_read_regs to read from the firmware boot version register.

    * Formats data into the fm_boot_version struct.

 * ccs811_read_fw_app_version - Read Firmware App Version Register

    * Takes in a pointer to the CCS811 device struct as the argument.

    * Utilizes ccs811_read_regs to read from the firmware app version register.

    * Formats data into the fm_app_version struct.

 * ccs811_read_error_id - Read Error Register

    * Takes in a pointer to the CCS811 device struct as the argument.

    * Utilizes ccs811_read_regs to read from the error register.

 * ccs811_perform_sw_reset - Performs Software Reset on the device

    * Takes in a pointer to the CCS811 device struct as the argument.

    * Utilizes the ccs811_set_regs to perform a software reset on the device.

 * ccs811_perform_app_erase - Performs Application Reset on the device

    * Takes in a pointer to the CCS811 device struct as the argument.

    * Utilizes the ccs811_set_regs to perform the application reset on the device.

 * ccs811_set_app_data - Set Application Data Register

    * Takes in a pointer to application data, and the CCS811 device struct as the arguments.

    * Utilizes the ccs811_set_regs to set the application data on the device.

 * ccs811_app_start - Start the Sensor

    * Takes in a pointer to the CCS811 device struct as the argument.

    * Utilizes the ccs811_set_regs to set the device from boot mode to application mode.

 * ccs811_convert_temp_and_humid_to_env_data - Set Measurement Mode Register

    * Takes in a 32 bit int for humidity, a 32 bit int for temperature, and a pointer to the environmental data struct

    * Converts given humidity and temperature into the environmental data structure. Creates the percentage and fraction values.

## How to Use

