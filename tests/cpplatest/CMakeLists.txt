
# Compilers often don't use the latest C++ standard as the default. Periodically update this value (possibly conditioned
# on compiler) as new standards are ratified/support is available
set(CMAKE_CXX_STANDARD 20)

project(witest.cpplatest)
add_executable(witest.cpplatest)

if (${CMAKE_CXX_COMPILER_ID} STREQUAL "Clang")
    # Clang is not compatible with the experimental coroutine header, so temporarily disable some headers until full
    # C++20 support is available
    set(COROUTINE_SOURCES)
else()
    set(COROUTINE_SOURCES
        ${CMAKE_CURRENT_SOURCE_DIR}/../ComApartmentVariableTests.cpp)
endif()

target_sources(witest.cpplatest PUBLIC
    ${COMMON_SOURCES}
    ${COROUTINE_SOURCES}
    ${CMAKE_CURRENT_SOURCE_DIR}/../CppWinRTTests.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/../CppWinRT20Tests.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/../StlTests.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/../TokenHelpersTests.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/../UniqueWinRTEventTokenTests.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/../WatcherTests.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/../WinRTTests.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/../WinVerifyTrustTest.cpp
    )
