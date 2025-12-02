qt_add_executable(test
    externals/catch.hpp
    main.cpp
)
target_include_directories(test PRIVATE
    ../lib/include
    externals
)

target_link_libraries(test PRIVATE
    Qt::Core
    Qt::Network
)

target_compile_options(test PRIVATE -std=c++17)

if(CMAKE_BUILD_TYPE STREQUAL Release AND WIN32)
    target_link_directories(test PRIVATE
        ${CMAKE_CURRENT_BINARY_DIR}/../lib/release/
    )

    target_link_libraries(test PRIVATE
        QDhcpDiscovery
    )
endif()

if(CMAKE_BUILD_TYPE STREQUAL Debug AND WIN32 AND NOT CMAKE_BUILD_TYPE STREQUAL Release)
    target_link_directories(test PRIVATE
        ${CMAKE_CURRENT_BINARY_DIR}/../lib/debug/
    )

    target_link_libraries(test PRIVATE
        QDhcpDiscoveryd
    )
endif()

if(CMAKE_BUILD_TYPE STREQUAL Release AND UNIX)
    target_link_directories(test PRIVATE
        ${CMAKE_CURRENT_BINARY_DIR}/../lib/
    )

    target_link_libraries(test PRIVATE
        QDhcpDiscovery
    )
endif()

if(CMAKE_BUILD_TYPE STREQUAL Debug AND UNIX AND NOT CMAKE_BUILD_TYPE STREQUAL Release)
    target_link_directories(test PRIVATE
        ${CMAKE_CURRENT_BINARY_DIR}/../lib/
    )

    target_link_libraries(test PRIVATE
        QDhcpDiscoveryd
    )
endif()

install(TARGETS test
    BUNDLE DESTINATION .
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)

qt_generate_deploy_app_script(
    TARGET test
    OUTPUT_SCRIPT deploy_script
    NO_UNSUPPORTED_PLATFORM_ERROR
)
install(SCRIPT ${deploy_script})
