project ( sdlconsole )

cmake_minimum_required ( VERSION 2.8.5 )
set ( CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake/modules" )

option ( BUILD_EXAMPLE "Build example" OFF )
option ( BUILD_OPENGL "Enable OpenGL if available" ON )

find_package ( SDL2 COMPONENTS image)
if ( NOT SDL_FOUND )
  message ( FATAL_ERROR "Can't find SDL which is required" )
else ()
  include_directories ( ${SDL_INCLUDE_DIR} )
  message ( "found SDL ${SDL_MAJOR}.${SDL_MINOR}.${SDL_MICRO} (${SDL_LIBRARY_DIRS}:${SDL_INCLUDE_DIR})" )
endif ()

if ( NOT SDLIMAGE_FOUND )
  message ( FATAL_ERROR "Can't find SDL_image which is required" )
else ()
  include_directories ( ${SDLIMAGE_INCLUDE_DIR} )
  message ( "found SDL_image ${SDL_IMAGE_MAJOR}.${SDL_IMAGE_MINOR}.${SDL_IMAGE_MICRO} (${SDL_IMAGE_LIBRARY_DIRS}:${SDLIMAGE_INCLUDE_DIR})" )
endif ()

add_definitions(-DHAVE_SDLIMAGE)

if (BUILD_OPENGL)
  find_package(OpenGL)
#  find_package(GLUT)
  if (OPENGL_FOUND)
      include_directories ( ${OPENGL_INCLUDE_DIR} )
  endif()
endif()

include_directories(include)

add_subdirectory(src)

if (${BUILD_EXAMPLE})
  add_subdirectory(example)
endif()