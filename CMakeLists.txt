cmake_minimum_required(VERSION 3.20)
project(minknap C)

set(CMAKE_C_STANDARD 11)

add_library(minknap SHARED include/minknap.h src/minknap.c)

install(DIRECTORY "${minknap_SOURCE_DIR}/include/"
        DESTINATION include/
        FILES_MATCHING
        PATTERN "*.h"
)

install(TARGETS minknap
        EXPORT minknap_targets
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib
        RUNTIME DESTINATION bin
        INCLUDES DESTINATION include/
        PUBLIC_HEADER DESTINATION include/
)

install(EXPORT minknap_targets
        FILE minknapTargets.cmake
        DESTINATION lib/cmake/minknap
)

configure_file(minknapConfig.cmake.in minknapConfig.cmake @ONLY)

install(FILES
        "${CMAKE_CURRENT_BINARY_DIR}/minknapConfig.cmake"
        DESTINATION lib/cmake/minknap
)

