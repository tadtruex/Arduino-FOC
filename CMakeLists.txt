# v3.21 implemented semantic changes regarding $<TARGET_OBJECTS:...>
# See https://cmake.org/cmake/help/v3.21/command/target_link_libraries.html#linking-object-libraries-via-target-objects
cmake_minimum_required(VERSION 3.21)

add_library(Simple_FOC INTERFACE)
add_library(Simple_FOC_usage INTERFACE)

target_include_directories(Simple_FOC_usage INTERFACE
  src
)


target_link_libraries(Simple_FOC_usage INTERFACE
  base_config
  SPI
  Wire
)

target_link_libraries(Simple_FOC INTERFACE Simple_FOC_usage)



add_library(Simple_FOC_bin OBJECT EXCLUDE_FROM_ALL
  src/BLDCMotor.cpp
  src/common/base_classes/CurrentSense.cpp
  src/common/base_classes/FOCMotor.cpp
  src/common/base_classes/Sensor.cpp
  src/common/foc_utils.cpp
  src/common/lowpass_filter.cpp
  src/common/pid.cpp
  src/common/time_utils.cpp
  src/communication/Commander.cpp
  src/communication/SimpleFOCDebug.cpp
  src/communication/StepDirListener.cpp
  src/current_sense/GenericCurrentSense.cpp
  src/current_sense/hardware_specific/atmega_mcu.cpp
  src/current_sense/hardware_specific/due_mcu.cpp
  src/current_sense/hardware_specific/esp32/esp32_adc_driver.cpp
  src/current_sense/hardware_specific/esp32/esp32_mcpwm_mcu.cpp
  src/current_sense/hardware_specific/esp32/esp32_mcu.cpp
  src/current_sense/hardware_specific/generic_mcu.cpp
  src/current_sense/hardware_specific/rp2040/rp2040_mcu.cpp
  src/current_sense/hardware_specific/samd/samd21_mcu.cpp
  src/current_sense/hardware_specific/samd/samd_mcu.cpp
  src/current_sense/hardware_specific/stm32/b_g431/b_g431_hal.cpp
  src/current_sense/hardware_specific/stm32/b_g431/b_g431_mcu.cpp
  src/current_sense/hardware_specific/stm32/stm32_mcu.cpp
  src/current_sense/hardware_specific/stm32/stm32f1/stm32f1_hal.cpp
  src/current_sense/hardware_specific/stm32/stm32f1/stm32f1_mcu.cpp
  src/current_sense/hardware_specific/stm32/stm32f4/stm32f4_hal.cpp
  src/current_sense/hardware_specific/stm32/stm32f4/stm32f4_mcu.cpp
  src/current_sense/hardware_specific/stm32/stm32f4/stm32f4_utils.cpp
  src/current_sense/hardware_specific/stm32/stm32f7/stm32f7_hal.cpp
  src/current_sense/hardware_specific/stm32/stm32f7/stm32f7_mcu.cpp
  src/current_sense/hardware_specific/stm32/stm32f7/stm32f7_utils.cpp
  src/current_sense/hardware_specific/stm32/stm32g4/stm32g4_hal.cpp
  src/current_sense/hardware_specific/stm32/stm32g4/stm32g4_mcu.cpp
  src/current_sense/hardware_specific/stm32/stm32g4/stm32g4_utils.cpp
  src/current_sense/hardware_specific/stm32/stm32l4/stm32l4_hal.cpp
  src/current_sense/hardware_specific/stm32/stm32l4/stm32l4_mcu.cpp
  src/current_sense/hardware_specific/stm32/stm32l4/stm32l4_utils.cpp
  src/current_sense/hardware_specific/teensy/teensy4_mcu.cpp
  src/current_sense/hardware_specific/teensy/teensy_mcu.cpp
  src/current_sense/InlineCurrentSense.cpp
  src/current_sense/LowsideCurrentSense.cpp
  src/drivers/BLDCDriver3PWM.cpp
  src/drivers/BLDCDriver6PWM.cpp
  src/drivers/hardware_specific/atmega/atmega2560_mcu.cpp
  src/drivers/hardware_specific/atmega/atmega328_mcu.cpp
  src/drivers/hardware_specific/atmega/atmega32u4_mcu.cpp
  src/drivers/hardware_specific/due_mcu.cpp
  src/drivers/hardware_specific/esp32/esp32_driver_mcpwm.cpp
  src/drivers/hardware_specific/esp32/esp32_ledc_mcu.cpp
  src/drivers/hardware_specific/esp32/esp32_mcpwm_mcu.cpp
  src/drivers/hardware_specific/esp8266_mcu.cpp
  src/drivers/hardware_specific/generic_mcu.cpp
  src/drivers/hardware_specific/nrf52_mcu.cpp
  src/drivers/hardware_specific/portenta_h7_mcu.cpp
  src/drivers/hardware_specific/renesas/renesas.cpp
  src/drivers/hardware_specific/rp2040/rp2040_mcu.cpp
  src/drivers/hardware_specific/samd/samd21_mcu.cpp
  src/drivers/hardware_specific/samd/samd51_mcu.cpp
  src/drivers/hardware_specific/samd/samd_mcu.cpp
  src/drivers/hardware_specific/stm32/stm32_mcu.cpp
  src/drivers/hardware_specific/teensy/teensy3_mcu.cpp
  src/drivers/hardware_specific/teensy/teensy4_mcu.cpp
  src/drivers/hardware_specific/teensy/teensy_mcu.cpp
  src/drivers/StepperDriver2PWM.cpp
  src/drivers/StepperDriver4PWM.cpp
  src/sensors/Encoder.cpp
  src/sensors/GenericSensor.cpp
  src/sensors/HallSensor.cpp
  src/sensors/MagneticSensorAnalog.cpp
  src/sensors/MagneticSensorI2C.cpp
  src/sensors/MagneticSensorPWM.cpp
  src/sensors/MagneticSensorSPI.cpp
  src/StepperMotor.cpp
)
target_link_libraries(Simple_FOC_bin PUBLIC Simple_FOC_usage)

target_link_libraries(Simple_FOC INTERFACE
  Simple_FOC_bin
  $<TARGET_OBJECTS:Simple_FOC_bin>
)

