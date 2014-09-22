cmake_minimum_required(VERSION 2.8 FATAL_ERROR)

find_package(Boost REQUIRED COMPONENTS system)
include_directories(${Boost_INCLUDE_DIRS})
link_directories(${Boost_LIBRARY_DIRS})

include (FindPkgConfig)
if (PKG_CONFIG_FOUND)
  pkg_check_modules(GAZEBO gazebo)
endif()
include_directories(${GAZEBO_INCLUDE_DIRS})
link_directories(${GAZEBO_LIBRARY_DIRS})

# attempt to find bullet
find_package (Bullet)
if (BULLET_FOUND)
  add_definitions (-DHAVE_BULLET)
  include_directories (BULLET_INCLUDE_DIRS)
  link_directories (BULLET_LIBRARIES)
endif (BULLET_FOUND)

add_library(juggler SHARED controller.cpp WorldParams.cpp)
target_link_libraries(juggler ${GAZEBO_LIBRARIES} ${Boost_LIBRARIES})

