cmake_minimum_required(VERSION 3.20)
project(ZeroRelay VERSION 0.1 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

find_package(Boost 1.75 REQUIRED COMPONENTS system thread)

if(NOT Boost_FOUND)
  message(FATAL_ERROR "Boost not found")
endif()

include_directories(${Boost_INCLUDE_DIRS} include)

file(GLOB_RECURSE SOURCES src/*.cpp)

add_executable(ZeroRelay ${SOURCES})

target_link_libraries(ZeroRelay Boost::system Boost::thread pthread)

if(MSVC)
  target_compile_options(ZeroRelay PRIVATE /W4 /WX)
else()
  target_compile_options(ZeroRelay PRIVATE -Wall -Wextra -Wpedantic -Werror)
endif()
