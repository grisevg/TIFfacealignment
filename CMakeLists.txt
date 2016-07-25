cmake_minimum_required(VERSION 3.5)
project (TIFfacealignment)

#Boost
set(Boost_USE_STATIC_LIBS        ON)
set(Boost_USE_MULTITHREADED      ON)
set(Boost_USE_STATIC_RUNTIME    OFF)
find_package(Boost REQUIRED system thread serialization filesystem)

#OpenCV
find_package(OpenCV REQUIRED)

add_executable(
        TIF_sheep
        sheepface.cpp
        ./dlib-18.16/dlib/all/source.cpp
)


target_include_directories(TIF_sheep PRIVATE
        ${OpenCV_INCLUDE_DIRS}
        ${Boost_INCLUDE_DIRS}
        dlib-18.16
)

target_link_libraries(TIF_sheep
        ${OpenCV_LIBRARIES}
        ${Boost_LIBRARIES}
)

install(TARGETS TIF_sheep RUNTIME DESTINATION ${PROJECT_BINARY_DIR}/bin)


#Coppy OpenCV dynamic libraries 
if(OpenCV_SHARED)
        FILE(GLOB opencv_shared_libs "${OpenCV_DIR}/../bin/*${CMAKE_SHARED_LIBRARY_SUFFIX}")
        install(FILES ${opencv_shared_libs} DESTINATION ${PROJECT_BINARY_DIR}/bin)
endif()