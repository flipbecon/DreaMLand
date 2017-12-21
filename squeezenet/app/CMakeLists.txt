# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.

cmake_minimum_required(VERSION 3.4.1)


#ncnn
include_directories(src/main/cpp/include
                    src/main/cpp)

add_library(
            libncnn
            STATIC
            IMPORTED
            )
set_target_properties(libncnn PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/src/main/jniLibs/${ANDROID_ABI}/libncnn.a)

#squeezencnn
add_library(squeezencnn SHARED src/main/cpp/squeezencnn_jni.cpp)

find_library( # Sets the name of the path variable.
              log-lib

              # Specifies the name of the NDK library that
              # you want CMake to locate.
              log )


target_link_libraries( # Specifies the target library.
                       squeezencnn
                       libncnn
                       z
                       jnigraphics
                       # Links the target library to the log library
                       # included in the NDK.
                       ${log-lib} )