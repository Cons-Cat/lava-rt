cmake_minimum_required(VERSION 3.15)

project(liblava-extras VERSION 0.5.6 LANGUAGES C CXX)

set(LIBLAVA_EXTRAS_DIR ${CMAKE_CURRENT_SOURCE_DIR}/liblava-extras)

message(">> lava-extras::raytracing")

add_library(lava-extras.raytracing STATIC
        ${LIBLAVA_EXTRAS_DIR}/raytracing/acceleration_structure.hpp
        ${LIBLAVA_EXTRAS_DIR}/raytracing/acceleration_structure.cpp
        ${LIBLAVA_EXTRAS_DIR}/raytracing/pipeline.hpp
        ${LIBLAVA_EXTRAS_DIR}/raytracing/pipeline.cpp
        ${LIBLAVA_EXTRAS_DIR}/raytracing/shader_binding_table.hpp
        ${LIBLAVA_EXTRAS_DIR}/raytracing.hpp
        )

target_link_libraries(lava-extras.raytracing PUBLIC
        lava::app
        # lava::resource
        # lava::block
        )

target_include_directories(
        lava-extras.raytracing PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
        # $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>/raytracing
        )

if (CMAKE_COMPILER_IS_GNUCXX)
        target_compile_options(lava-extras.raytracing PUBLIC -fpermissive)
endif()

set_property(TARGET lava-extras.raytracing PROPERTY EXPORT_NAME raytracing)
add_library(lava-extras::raytracing ALIAS lava-extras.raytracing)
