cmake_minimum_required(VERSION 2.8.3)
project(frsm)
set(POD_NAME frsm)
include(cmake/pods.cmake)

find_package(catkin REQUIRED)
find_package(PkgConfig REQUIRED)


catkin_package(
    INCLUDE_DIRS src
    LIBRARIES frsm
)


include_directories(
    src/libfrsm)

file(GLOB SOURCE_LIST src/libfrsm/*.cpp)
add_library(frsm SHARED ${SOURCE_LIST})
target_link_libraries(frsm glib-2.0)
pods_use_pkg_config_packages(frsm glib-2.0)

install(TARGETS frsm
    ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
    LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
    RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

file(GLOB INCLUDE_LIST src/libfrsm/*.h*)
install(FILES ${INCLUDE_LIST}
    DESTINATION ${CATKIN_GLOBAL_INCLUDE_DESTINATION}/libfrsm
)
