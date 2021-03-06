#规定最小版本
cmake_minimum_required(VERSION 3.4.1)
#包含目录
include_directories(
        #SDL包含目录
        include
        #assimp
        ext
)
#stbi
add_library(
        stb
        STATIC
        src/main/cpp/stb/stb_vorbis.c
        src/main/cpp/stb/deprecated/stb_image.c

)
#SDL2
add_library(
        SDL2
        SHARED
        IMPORTED
)
set_target_properties(
        SDL2
        PROPERTIES IMPORTED_LOCATION
        ${CMAKE_SOURCE_DIR}/jniLibs/${ANDROID_ABI}/libSDL2.so
)
#hidapi
add_library(
        hidapi
        SHARED
        IMPORTED
)
set_target_properties(
        hidapi
        PROPERTIES IMPORTED_LOCATION
        ${CMAKE_SOURCE_DIR}/jniLibs/${ANDROID_ABI}/libhidapi.so
)
#SDL2_mixer
add_library(
        SDL2_mixer
        SHARED
        IMPORTED
)
set_target_properties(
        SDL2_mixer
        PROPERTIES IMPORTED_LOCATION
        ${CMAKE_SOURCE_DIR}/jniLibs/${ANDROID_ABI}/libSDL2_mixer.so
)
#SKIA
add_library(
        SKIA
        SHARED
        IMPORTED
)
set_target_properties(
        SKIA
        PROPERTIES IMPORTED_LOCATION
        ${CMAKE_SOURCE_DIR}/jniLibs/${ANDROID_ABI}/libskia.so
)
add_library(
        main
        SHARED
        src/main/cpp/main.cpp
        src/main/cpp/GUI.cpp
        src/main/cpp/model.cpp
        src/main/cpp/AssetsHelper.cpp
        src/main/cpp/FileHelper.cpp
        src/main/cpp/MusicHelper.cpp
)
#assimp
add_library(
        assimp
        SHARED
        IMPORTED
)
set_target_properties(
        assimp

        PROPERTIES
        IMPORTED_LOCATION

        ${CMAKE_SOURCE_DIR}/jniLibs/${ANDROID_ABI}/libassimp.so
)
target_link_libraries(
        main
        hidapi
        SDL2
        SDL2_mixer
        SKIA
        assimp
        stb
        GLESv1_CM
        GLESv2
        GLESv3
        log
        android
)