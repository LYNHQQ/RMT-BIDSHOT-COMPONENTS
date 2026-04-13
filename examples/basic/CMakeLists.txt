cmake_minimum_required(VERSION 3.16)

set(EXTRA_COMPONENT_DIRS "../..")
set(IDF_TARGET "esp32s3")

include($ENV{IDF_PATH}/tools/cmake/project.cmake)
project(bidir_dshot_basic)
