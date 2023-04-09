cmake_minimum_required(VERSION 3.10)

# set the project name
SET(BS_LOGGER_LIB_NAME BSlogger)

project(${BS_LOGGER_LIB_NAME} VERSION 0.1.0 LANGUAGES CXX)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_CXX_FLAGS "-fsanitize=address -fsanitize=undefined -Wall -Wextra ${CMAKE_CXX_FLAGS}")
set(CMAKE_CXX_STANDARD 17)

# add the executable
SET(BS_LOGGER_COMPILE_FEATURES
        cxx_lambdas
        )

add_library(${BS_LOGGER_LIB_NAME}
        src/bslogger_examples.cpp
        )

add_executable(bslogger-examples src/bslogger_examples.cpp)

target_include_directories(${BS_LOGGER_LIB_NAME}
        PRIVATE
        $<BUILD_INTERFACE:${${BS_LOGGER_LIB_NAME}_BINARY_DIR}/src>
        $<BUILD_INTERFACE:${${BS_LOGGER_LIB_NAME}_SOURCE_DIR}/src>
        PUBLIC
        $<BUILD_INTERFACE:${${BS_LOGGER_LIB_NAME}_BINARY_DIR}/include>
        $<BUILD_INTERFACE:${${BS_LOGGER_LIB_NAME}_SOURCE_DIR}/include>
        )

target_link_libraries(${BS_LOGGER_LIB_NAME}
        PRIVATE
        )

set_target_properties(${BS_LOGGER_LIB_NAME} PROPERTIES OUTPUT_NAME ${BS_LOGGER_LIB_NAME})
target_compile_features(${BS_LOGGER_LIB_NAME} PUBLIC ${BS_LOGGER_COMPILE_FEATURES})