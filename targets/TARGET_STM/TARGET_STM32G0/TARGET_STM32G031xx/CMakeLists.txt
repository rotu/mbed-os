# Copyright (c) 2020 ARM Limited. All rights reserved.
# SPDX-License-Identifier: Apache-2.0

add_subdirectory(TARGET_NUCLEO_G031K8 EXCLUDE_FROM_ALL)

if(${MBED_TOOLCHAIN} STREQUAL "GCC_ARM")
    set(STARTUP_FILE TOOLCHAIN_GCC_ARM/startup_stm32g031xx.S)
    set(LINKER_FILE TOOLCHAIN_GCC_ARM/stm32g031xx.ld)
elseif(${MBED_TOOLCHAIN} STREQUAL "ARM")
    set(STARTUP_FILE TOOLCHAIN_ARM/startup_stm32g031xx.S)
    set(LINKER_FILE TOOLCHAIN_ARM/stm32g031xx.sct)
endif()

add_library(STM32G031xx INTERFACE)

target_sources(STM32G031xx
    INTERFACE
        ${STARTUP_FILE}
)

target_include_directories(STM32G031xx
    INTERFACE
        .
)

mbed_set_linker_script(STM32G031xx ${CMAKE_CURRENT_SOURCE_DIR}/${LINKER_FILE})

target_link_libraries(STM32G031xx INTERFACE STM32G0)
