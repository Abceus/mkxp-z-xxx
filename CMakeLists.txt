cmake_minimum_required(VERSION 3.27.4)
project(mkxp-z-xxx)

include(FetchContent)

# ogg
FetchContent_Declare(
    ogg
    GIT_REPOSITORY https://github.com/mkxp-z/ogg.git
    GIT_TAG        bada45718453ac27b56773ae663f7e65112f6a6e # v1.3.4
)

FetchContent_MakeAvailable(ogg)

set(OGG_LIBRARY ogg)
get_target_property(OGG_INCLUDE_DIR ogg INCLUDE_DIRECTORIES)

# Theora
add_subdirectory("cmake/theora")

# vorbis
FetchContent_Declare(
    vorbis
    GIT_REPOSITORY https://github.com/mkxp-z/vorbis.git
    GIT_TAG        0657aee69dec8508a0011f47f3b69d7538e9d262 # v1.3.7
)

FetchContent_MakeAvailable(vorbis)

# pixman
add_subdirectory("cmake/pixman")