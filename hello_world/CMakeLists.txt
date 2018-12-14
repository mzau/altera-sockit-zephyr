cmake_minimum_required(VERSION 3.8.2)

if (BOARD STREQUAL "sockit")
   set(BOARD_ROOT ${CMAKE_CURRENT_LIST_DIR}/../)
   set(SOC_ROOT ${CMAKE_CURRENT_LIST_DIR}/../)
endif()

include($ENV{ZEPHYR_BASE}/cmake/app/boilerplate.cmake NO_POLICY_SCOPE)
project(hello_world)

target_sources(app PRIVATE src/main.c)
