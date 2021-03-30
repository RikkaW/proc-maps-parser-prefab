cmake_minimum_required(VERSION 3.4.1)

project(proc-maps-parser)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Wextra -Werror -fvisibility=hidden -Wno-builtin-macro-redefined -D__FILE__=__FILE_NAME__")

add_library(proc-maps-parser STATIC pmparser.c)
include_directories("include")
target_link_libraries(proc-maps-parser)

add_custom_command(TARGET proc-maps-parser POST_BUILD
        COMMAND ${CMAKE_OBJCOPY} --remove-section=.comment --strip-debug "libproc-maps-parser.a")
