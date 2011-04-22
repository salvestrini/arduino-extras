find_program(AVR_OBJCOPY_EXECUTABLE avr-objcopy)
message(STATUS "Binary ${AVR_OBJCOPY_EXECUTABLE}")

find_program(AVR_SIZE_EXECUTABLE avr-size)
message(STATUS "Binary ${AVR_SIZE_EXECUTABLE}")

find_program(AVRDUDE_EXECUTABLE avrdude)
message(STATUS "Binary ${AVRDUDE_EXECUTABLE}")

set(AVRDUDE_DEVICE        "/dev/ttyUSB0"      CACHE FILEPATH "ISP programming device")
set(AVRDUDE_SPEED         "57600"             CACHE STRING   "ISP programming speed")
set(AVRDUDE_CONFIGURATION "/etc/avrdude.conf" CACHE FILEPATH "avrdude configuration file")

if(${ARDUINO_TYPE}     MATCHES "^uno$")
  set(FAMILY "m328p")
elseif(${ARDUINO_TYPE} MATCHES "^duemilanove$")
  set(FAMILY "m328p")
elseif(${ARDUINO_TYPE} MATCHES "^diecimila$")
  set(FAMILY "m168")
else()
  # A default value ...
  set(FAMILY "m168")
endif()

set(AVR_FAMILY @FAMILY@ CACHE STRING "ISP programming family")

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/isp.in ${CMAKE_CURRENT_BINARY_DIR}/isp)
