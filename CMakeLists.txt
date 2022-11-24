project(uros_test)

link_directories(libmicroros)

add_executable(${PROJECT_NAME}
	uros_test.c
	pico_uart_transport.c
	)

# pull in our pico_stdlib which pulls in commonly used features
target_link_libraries(${PROJECT_NAME} pico_stdlib hardware_gpio hardware_adc hardware_pwm hardware_i2c microros)

target_include_directories(${PROJECT_NAME} PUBLIC
    libmicroros/include
)

SET(CMAKE_C_FLAGS  "${CMAKE_C_FLAGS} -ffunction-sections -fdata-sections")
SET(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} -ffunction-sections -fdata-sections")


# enable usb output, disable UART output
pico_enable_stdio_usb(${PROJECT_NAME} 1)
pico_enable_stdio_uart(${PROJECT_NAME} 0)

add_compile_definitions(PICO_UART_ENABLE_CRLF_SUPPORT=0)
add_compile_definitions(PICO_STDIO_ENABLE_CRLF_SUPPORT=0)
add_compile_definitions(PICO_STDIO_DEFAULT_CRLF=0)


# create map/bin/hex file etc.
pico_add_extra_outputs(${PROJECT_NAME})