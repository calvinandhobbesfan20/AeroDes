#cmake_minimum_required(VERSION 3.17)
cmake_minimum_required(VERSION 3.05)

# set the project name and version
project(aerolib VERSION 1.0.0 DESCRIPTION "open source aero design")

# specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# should we use debug mode
option(DBG "debug mode" OFF)

if(DBG)
    set(DBG_VALUE 1)
endif()

configure_file(config.hpp.in "${CMAKE_SOURCE_DIR}/src/wake/config.hpp" @ONLY)
configure_file(config.hpp.in "${CMAKE_SOURCE_DIR}/src/canareq/config.hpp" @ONLY)
configure_file(config.hpp.in "${CMAKE_SOURCE_DIR}/src/prandtline/config.hpp" @ONLY)

# add module libraries
add_subdirectory(src)
#add_subdirectory(src/wake)

include_directories(src)                # for variables.hpp
include_directories(src/prandtline)
include_directories(src/wake)

# executables
add_executable(cfmactu
        src/variables.hpp
        src/propulsion/cfmactu.cpp
        src/propulsion/cfmactu.hpp
        src/propulsion/main.cpp)

add_executable(prandtl
        src/variables.hpp
        src/prandtline/prandtline.cpp
        src/prandtline/prandtline.hpp
        src/prandtline/main.cpp)

add_executable(wake
        src/variables.hpp
        src/wake/wake.cpp
        src/wake/wake.hpp
        src/wake/main.cpp)

add_executable(canary
        src/variables.hpp
        src/wake/wake.cpp
        src/wake/wake.hpp
        src/canareq/canareq.cpp
        src/canareq/canareq.hpp
        src/canareq/main.cpp)

add_executable(smooth
        src/variables.hpp
        src/smoothpolar/smoothpolar.cpp
        src/smoothpolar/smoothpolar.hpp
        src/smoothpolar/main.cpp)

add_executable(tsd
        src/variables.hpp
        src/tsd/tsd.cpp
        src/tsd/tsd.hpp
        src/tsd/main.cpp)

install(TARGETS cfmactu)
install(TARGETS prandtl)
install(TARGETS wake)
install(TARGETS canary)
install(TARGETS tsd)
