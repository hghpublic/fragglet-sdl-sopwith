cmake_minimum_required(VERSION 4.2)

project(sdl-sopwith
    VERSION 2.9.0
    DESCRIPTION "Classic bi-plane shoot-'em up"
    HOMEPAGE_URL https://github.com/fragglet/sdl-sopwith
    LANGUAGES C
)

# if using valgrind, set BUILD_WITH_ASAN to OFF
option(BUILD_WITH_ASAN "Build with ASAN" OFF)

find_package(SDL2 CONFIG REQUIRED)

set(target sopwith)
add_executable(${target})
target_include_directories(${target} PRIVATE ${PROJECT_SOURCE_DIR}/dev/include)
if(BUILD_WITH_ASAN)
    target_compile_options(${target} PRIVATE -fsanitize=address)
    target_link_options(${target} PRIVATE -fsanitize=address)
endif()
target_link_libraries(${target}
    PRIVATE
    $<TARGET_NAME_IF_EXISTS:SDL2::SDL2main>
    $<IF:$<TARGET_EXISTS:SDL2::SDL2>,SDL2::SDL2,SDL2::SDL2-static>
)

add_subdirectory(src)

# valgrind target

add_custom_target(valgrind
    COMMAND valgrind
        --leak-check=full
        --show-leak-kinds=all
        --track-origins=yes
        -s --suppressions=${CMAKE_SOURCE_DIR}/sopwith.valgrind.supp
        --gen-suppressions=all
        --log-file=${CMAKE_SOURCE_DIR}/dev/valgrind/logs/memcheck.log
        $<TARGET_FILE:${target}>
    DEPENDS ${target}
    WORKING_DIRECTORY $<TARGET_FILE_DIR:${target}>
    COMMENT "Running sopwith with valgrind"
)
