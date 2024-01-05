cmake_minimum_required(VERSION 3.15 FATAL_ERROR)

project(ZeekPluginNapatech)

include(ZeekPlugin)

list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

find_package(Napatech)

if ( NAPATECH_FOUND )
    include_directories(BEFORE ${NAPATECH_INCLUDE_DIR})
    zeek_plugin_begin(Zeek Napatech)
    zeek_plugin_cc(src/Plugin.cc)
    zeek_plugin_cc(src/Napatech.cc)
    zeek_plugin_bif(src/Napatech.bif)
    zeek_plugin_link_library(${NAPATECH_LIBRARY})
    zeek_plugin_dist_files(zeekctl/Napatech.py)
    zeek_plugin_end()
    message(STATUS "Napatech prefix      : ${NAPATECH_ROOT_DIR}")
else ()
    message(FATAL_ERROR "Napatech library and/or headers not found.")
endif ()
