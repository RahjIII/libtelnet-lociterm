
find_package(ZLIB)
add_definitions(-DHAVE_ZLIB=1)
add_definitions(-DHAVE_ZSTD=1)

add_executable(telnet-chatd telnet-chatd.c)
target_link_libraries(telnet-chatd
    libtelnet
    $<$<C_COMPILER_ID:MSVC>:wsock32>
    $<$<C_COMPILER_ID:MSVC>:ws2_32>
    ZLIB::ZLIB
    zstd
)

if (UNIX)
    add_executable(telnet-client telnet-client.c)
    target_link_libraries(telnet-client
        libtelnet
        ZLIB::ZLIB
        zstd
    )
endif ()

add_executable(telnet-test telnet-test.c)
target_link_libraries(telnet-test
    libtelnet
    ZLIB::ZLIB
    zstd
)

add_executable(telnet-proxy telnet-proxy.c)
target_link_libraries(telnet-proxy
    libtelnet
    $<$<C_COMPILER_ID:MSVC>:wsock32>
    $<$<C_COMPILER_ID:MSVC>:ws2_32>
    ZLIB::ZLIB
    zstd
)
