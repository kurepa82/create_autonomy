cmake_minimum_required(VERSION 2.8.3)
project(ca_driver)

add_compile_options(-std=c++11)

find_package(libcreate REQUIRED)

find_package(catkin REQUIRED COMPONENTS
  ca_msgs
  diagnostic_msgs
  diagnostic_updater
  geometry_msgs
  nav_msgs
  roscpp
  sensor_msgs
  std_msgs
  tf
)

catkin_package(
  INCLUDE_DIRS include
  CATKIN_DEPENDS
    ca_msgs
    diagnostic_msgs
    diagnostic_updater
    geometry_msgs
    nav_msgs
    roscpp
    sensor_msgs
    std_msgs
    tf
  DEPENDS libcreate
)

include_directories(
  include
  ${libcreate_INCLUDE_DIRS}
  ${catkin_INCLUDE_DIRS}
)

add_executable(${PROJECT_NAME} src/create_driver.cpp)

target_link_libraries(${PROJECT_NAME}
  ${libcreate_LIBRARIES}
  ${catkin_LIBRARIES}
)

add_dependencies(${PROJECT_NAME} ${catkin_EXPORTED_TARGETS})

install(TARGETS ${PROJECT_NAME}
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY include
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.h"
)

install(DIRECTORY launch config
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)
