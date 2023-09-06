# Copy-pasted from https://github.com/xiph/theora/issues/10

include(FetchContent)

FetchContent_Declare(
    pixman_origin
    GIT_REPOSITORY https://github.com/mkxp-z/pixman.git
    GIT_TAG        244383bf9f3493c014985de46876e40fd5db43f3 # pixman-0.40.0
)

FetchContent_GetProperties(pixman_origin)

# TODO: move this shit to dependency providers
if(NOT pixman_origin_POPULATED)
    FetchContent_Populate(pixman_origin)

    set(PIXMAN_SRC_DIR ${pixman_origin_SOURCE_DIR}/pixman)
    set(PIXMAN_GENERATED_SRC_DIR ${pixman_origin_SOURCE_DIR}/generated)

    set(PIXMAN_VERSION_MAJOR 0)
    set(PIXMAN_VERSION_MINOR 40)
    set(PIXMAN_VERSION_MICRO 0)

    configure_file(config.h.in ${PIXMAN_GENERATED_SRC_DIR}/config.h @ONLY)
    configure_file(${PIXMAN_SRC_DIR}/pixman-version.h.in ${PIXMAN_GENERATED_SRC_DIR}/pixman-version.h @ONLY)

    add_library(pixman_generated INTERFACE)
    target_include_directories(pixman_generated INTERFACE ${PIXMAN_GENERATED_SRC_DIR})
    
    add_library(pixman STATIC "${PIXMAN_SRC_DIR}/pixman.c"
        "${PIXMAN_SRC_DIR}/pixman-access.c"
        "${PIXMAN_SRC_DIR}/pixman-access-accessors.c"
        "${PIXMAN_SRC_DIR}/pixman-bits-image.c"
        "${PIXMAN_SRC_DIR}/pixman-combine32.c"
        "${PIXMAN_SRC_DIR}/pixman-combine-float.c"
        "${PIXMAN_SRC_DIR}/pixman-conical-gradient.c"
        "${PIXMAN_SRC_DIR}/pixman-filter.c"
        "${PIXMAN_SRC_DIR}/pixman-x86.c"
        "${PIXMAN_SRC_DIR}/pixman-mips.c"
        "${PIXMAN_SRC_DIR}/pixman-arm.c"
        "${PIXMAN_SRC_DIR}/pixman-ppc.c"
        "${PIXMAN_SRC_DIR}/pixman-edge.c"
        "${PIXMAN_SRC_DIR}/pixman-edge-accessors.c"
        "${PIXMAN_SRC_DIR}/pixman-fast-path.c"
        "${PIXMAN_SRC_DIR}/pixman-glyph.c"
        "${PIXMAN_SRC_DIR}/pixman-general.c"
        "${PIXMAN_SRC_DIR}/pixman-gradient-walker.c"
        "${PIXMAN_SRC_DIR}/pixman-image.c"
        "${PIXMAN_SRC_DIR}/pixman-implementation.c"
        "${PIXMAN_SRC_DIR}/pixman-linear-gradient.c"
        "${PIXMAN_SRC_DIR}/pixman-matrix.c"
        "${PIXMAN_SRC_DIR}/pixman-noop.c"
        "${PIXMAN_SRC_DIR}/pixman-radial-gradient.c"
        "${PIXMAN_SRC_DIR}/pixman-region16.c"
        "${PIXMAN_SRC_DIR}/pixman-region32.c"
        "${PIXMAN_SRC_DIR}/pixman-solid-fill.c"
        "${PIXMAN_SRC_DIR}/pixman-timer.c"
        "${PIXMAN_SRC_DIR}/pixman-trap.c"
        "${PIXMAN_SRC_DIR}/pixman-utils.c"
    )
    
    target_include_directories(pixman PUBLIC "${THEORA_SRC_DIR}")
    target_compile_definitions(pixman PRIVATE HAVE_CONFIG_H)
    target_link_libraries(pixman PRIVATE pixman_generated)
endif()