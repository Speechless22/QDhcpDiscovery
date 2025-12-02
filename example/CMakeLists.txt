qt_add_executable(example
    main.cpp
)

target_include_directories(example PRIVATE
    ../lib/include
)

target_link_libraries(example PRIVATE
    QDhcpDiscovery
    Qt6::Core
    Qt6::Network
)

target_compile_features(example PRIVATE cxx_std_17)

install(TARGETS example
    BUNDLE DESTINATION .
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)

qt_generate_deploy_app_script(
    TARGET example
    OUTPUT_SCRIPT deploy_script
    NO_UNSUPPORTED_PLATFORM_ERROR
)
install(SCRIPT ${deploy_script})