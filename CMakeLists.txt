cmake_minimum_required(VERSION 3.16)
set(CMAKE_TOOLCHAIN_FILE ${CMAKE_CURRENT_SOURCE_DIR}/stm32-cmake/cmake/stm32_gcc.cmake)

# TODO: name your project
project(stm32-template C ASM CXX)

# TODO: require packages in there
find_package(CMSIS COMPONENTS STM32F407VG REQUIRED)
# find_package(HAL COMPONENTS STM32F4 REQUIRED)

# TODO: add some libraries depends
set(PROJECT_LIB "")
list(APPEND PROJECT_LIB STM32::NoSys)
list(APPEND PROJECT_LIB CMSIS::STM32::F407VG)
# list(APPEND PROJECT_LIB HAL::STM32::F4::RCC)

# TODO: add some source/header
aux_source_directory(src src)
set(PROJECT_SOURCE "")
set(PROJECT_INCLUD "")
list(APPEND PROJECT_SOURCE "${src}")
list(APPEND PROJECT_INCLUD inc)

set(CMAKE_PROJECT_NAME)

add_executable(${CMAKE_PROJECT_NAME} ${PROJECT_SOURCE})
target_include_directories(${CMAKE_PROJECT_NAME} PUBLIC ${PROJECT_INCLUD})
target_link_libraries(${CMAKE_PROJECT_NAME} PUBLIC ${PROJECT_LIB})
stm32_print_size_of_target(${CMAKE_PROJECT_NAME})
stm32_generate_binary_file(${CMAKE_PROJECT_NAME})
stm32_get_chip_info(STM32F407VG)