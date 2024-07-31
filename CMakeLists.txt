cmake_minimum_required(VERSION 3.12)  # Adjust this version if necessary

# Set up the Pico SDK path
set(PICO_SDK_PATH "C:/Program Files/Raspberry Pi/Pico SDK v1.5.1/pico-sdk")


# Include the Pico SDK import file
include(${PICO_SDK_PATH}/external/pico_sdk_import.cmake)

# Define the project name
set(projname "main")

# Define the project
project(${projname} C CXX ASM)


# Set C and C++ standards
set(CMAKE_C_STANDARD 11)
set(PICO_BOARD pico_w)
set(CMAKE_CXX_STANDARD 17)

# Initialize the Pico SDK
pico_sdk_init()

# Add the executable
add_executable(${projname}
    main.c
)

# Enable USB Virtual COM Port and disable UART
pico_enable_stdio_usb(${projname} 1)
pico_enable_stdio_uart(${projname} 0)

# Link the libraries
target_link_libraries(${projname}
    pico_stdlib
    pico_cyw43_arch_none
    hardware_spi
    hardware_i2c
    pico_binary_info
)

# Add extra outputs (like UF2 file)
pico_add_extra_outputs(${projname})
