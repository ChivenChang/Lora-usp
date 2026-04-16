# SPDX-License-Identifier: BSD-3-Clause-Clear
# FLRC Burst Examples

cmake_minimum_required(VERSION 3.25)

set(DESCRIPTION "FLRC burst data transfer")

################################################################################
# Toolchain and Project

include(${CMAKE_CURRENT_SOURCE_DIR}/../../toolchain.cmake)
project(flrc_burst LANGUAGES C ASM DESCRIPTION "${DESCRIPTION}")
include(${CMAKE_CURRENT_SOURCE_DIR}/../../common.cmake)

################################################################################
# Create targets

set(FLRC_BURST_SOURCES
    ${CMAKE_CURRENT_SOURCE_DIR}/main_flrc_burst.c
    ${CMAKE_CURRENT_SOURCE_DIR}/flrc_burst_tx.c
    ${CMAKE_CURRENT_SOURCE_DIR}/flrc_burst_rx.c
    ${CMAKE_CURRENT_SOURCE_DIR}/flrc_burst_utils.c
)

# Transmitter
add_executable(flrc_burst_tx ${FLRC_BURST_SOURCES})
setup_example_target(flrc_burst_tx)
register_example(flrc_burst_tx "${DESCRIPTION} (transmitter)")
target_compile_definitions(flrc_burst_tx PRIVATE ROLE=TRANSMITTER)
target_include_directories(flrc_burst_tx PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})

# Receiver
add_executable(flrc_burst_rx ${FLRC_BURST_SOURCES})
setup_example_target(flrc_burst_rx)
register_example(flrc_burst_rx "${DESCRIPTION} (receiver)")
target_compile_definitions(flrc_burst_rx PRIVATE ROLE=RECEIVER)
target_include_directories(flrc_burst_rx PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})

# Build both targets
add_custom_target(flrc_burst DEPENDS flrc_burst_tx flrc_burst_rx)