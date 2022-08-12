# QPCPP Zephyr application template and example
# SPDX-License-Identifier: GPL-3.0-or-later OR LicenseRef-QL-commercial

cmake_minimum_required(VERSION 3.20.0)

# location of the QPCPP Zephyr module
# NOTE: might need to adjust for your project
#
set(QPCPP ${CMAKE_CURRENT_SOURCE_DIR}/qpcpp)

# Zephyr stuff
set(ZEPHYR_EXTRA_MODULES ${QPCPP})
find_package(Zephyr REQUIRED HINTS $ENV{ZEPHYR_BASE})

# project name
# NOTE: Adjust for your project
#
project(my_zephyr)

# sources for your project
# NOTE: Adjust for your project
#
target_sources(app PRIVATE
 src/main.cpp
 src/bsp.cpp
 src/philo.cpp
 src/table.cpp
)

# option to turn QSPY software tracing ON or OFF
# NOTE: Typically specified on command-line, e.g.:
# west build -b <board> -- -DQSPY=ON
#
option(QSPY "QSPY software tracing" OFF)

