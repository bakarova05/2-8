cmake_minimum_required(VERSION 3.5.0)
set(PATCH_VERSION "1" CACHE INTERNAL "Patch version")
set(PROJECT_VESRION 0.0.${PATCH_VERSION})
project(laba2 VERSION ${PROJECT_VESRION})
find_package(Boost COMPONENTS unit_test_framework REQUIRED)

add_executable(laba2 lab2.cpp)

set_target_properties(laba2 PROPERTIES
    CXX_STANDARD 14
    CXX_STANDARD_REQUIRED ON
)

if (MSVC)
    target_compile_options(laba2 PRIVATE
        /W4
    )
else ()
    target_compile_options(laba2 PRIVATE
        -Wall -Wextra 
    )
endif()

install(TARGETS laba2 RUNTIME DESTINATION bin)

if (${CMAKE_SYSTEM} MATCHES "Linux")
    set(CPACK_GENERATOR DEB)
else ()
    set(CPACK_GENERATOR ZIP)
endif()

set(CPACK_PACKAGE_VERSION_MAJOR "${PROJECT_VERSION_MAJOR}")
set(CPACK_PACKAGE_VERSION_MINOR "${PROJECT_VERSION_MINOR}")
set(CPACK_PACKAGE_VERSION_PATCH "${PROJECT_VERSION_PATCH}")

set(CPACK_PACKAGE_CONTACT example@example.com)

include(CPack)
enable_testing()

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})