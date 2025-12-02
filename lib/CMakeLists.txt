qt_add_library(QDhcpDiscovery
    include/QDhcpDiscovery.h
    include/QDhcpDiscovery_global.h
    src/QDhcpDiscovery.cpp
)

target_include_directories(QDhcpDiscovery PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/include
)

target_link_libraries(QDhcpDiscovery PUBLIC
    Qt6::Core
    Qt6::Network
)

target_compile_features(QDhcpDiscovery PUBLIC cxx_std_17)

set_target_properties(QDhcpDiscovery PROPERTIES
    DEBUG_POSTFIX "d"
)

if(TEST_COVERAGE)
    target_link_libraries(QDhcpDiscovery PUBLIC
        gcov
    )

    target_compile_options(QDhcpDiscovery
        -fprofile-arcs
        -ftest-coverage
    )
endif()

install(TARGETS QDhcpDiscovery
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)