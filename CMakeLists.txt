cmake_minimum_required( VERSION 2.8.3 )
project( epnp )

# find_package(OpenCV REQUIRED)
# include( $ENV{OpenCV_DIR}/OpenCVConfig.cmake )
include( "C:/opencv/build/OpenCVConfig.cmake" )

include_directories( src )

add_library( ${PROJECT_NAME} src/epnp.cpp )
target_link_libraries( ${PROJECT_NAME} ${OpenCV_LIBRARIES} )

file( GLOB SRCS examples/*.cpp)
foreach( src ${SRCS} )
    string( REGEX REPLACE "(^.*/|.cpp$)" "" exe ${src} )
    message( STATUS "${exe} <-- ${src}" )
    add_executable( ${exe} ${src} )
    target_link_libraries( ${exe} ${PROJECT_NAME} ${OpenCV_LIBRARIES} )
endforeach( src )
