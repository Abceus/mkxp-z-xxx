# Copy-pasted from https://github.com/xiph/theora/issues/10

include(FetchContent)

FetchContent_Declare(
    theora_origin
    GIT_REPOSITORY https://github.com/xiph/theora.git
    GIT_TAG        7ffd8b2ecfc2d93ae5e16028e7528e609266bfbf # v1.1.1
)

FetchContent_GetProperties(theora_origin)

# TODO: move this shit to dependency providers
if(NOT theora_origin_POPULATED)
    FetchContent_Populate(theora_origin)

    set(THEORA_SRC_DIR ${theora_origin_SOURCE_DIR})
    
    add_library(theora STATIC "${THEORA_SRC_DIR}/lib/apiwrapper.c"
        "${THEORA_SRC_DIR}/lib/bitpack.c" "${THEORA_SRC_DIR}/lib/dequant.c"
        "${THEORA_SRC_DIR}/lib/fragment.c" "${THEORA_SRC_DIR}/lib/idct.c"
        "${THEORA_SRC_DIR}/lib/info.c" "${THEORA_SRC_DIR}/lib/internal.c"
        "${THEORA_SRC_DIR}/lib/state.c" "${THEORA_SRC_DIR}/lib/quant.c"
        "${THEORA_SRC_DIR}/lib/decapiwrapper.c" "${THEORA_SRC_DIR}/lib/decinfo.c"
        "${THEORA_SRC_DIR}/lib/decode.c" "${THEORA_SRC_DIR}/lib/huffdec.c")
    
    target_include_directories(theora PRIVATE "${THEORA_SRC_DIR}/include")
    
    target_compile_options(theora PRIVATE -Wno-shift-negative-value
        -Wno-shift-op-parentheses)

    target_link_libraries(theora ogg)
endif()