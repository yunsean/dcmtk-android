cmake_minimum_required(VERSION 3.4.1)

SET(ROOT_DIR ${CMAKE_SOURCE_DIR})
INCLUDE_DIRECTORIES(${ROOT_DIR}/include)

add_library(libdcmdata STATIC IMPORTED)
set_target_properties(libdcmdata PROPERTIES IMPORTED_LOCATION ${ROOT_DIR}/lib/${ANDROID_ABI}/libdcmdata.a)
add_library(libi2d STATIC IMPORTED)
set_target_properties(libi2d PROPERTIES IMPORTED_LOCATION ${ROOT_DIR}/lib/${ANDROID_ABI}/libi2d.a)
add_library(liboflog STATIC IMPORTED)
set_target_properties(liboflog PROPERTIES IMPORTED_LOCATION ${ROOT_DIR}/lib/${ANDROID_ABI}/liboflog.a)
add_library(libofstd STATIC IMPORTED)
set_target_properties(libofstd PROPERTIES IMPORTED_LOCATION ${ROOT_DIR}/lib/${ANDROID_ABI}/libofstd.a)


add_library( native-lib
             SHARED
             native-lib.cpp )

find_library( log-lib
        log )
find_library( z-lib
        z )

target_link_libraries( native-lib
        libdcmdata
        libi2d
        liboflog
        libofstd
        ${log-lib}
        ${z-lib})