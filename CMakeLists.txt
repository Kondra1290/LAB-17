cmake_minimum_required(VERSION 3.16)

project(1_2_3 VERSION 0.1 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

find_package(Qt6 6.4 REQUIRED COMPONENTS Quick)

qt_standard_project_setup()

qt_add_executable(app1_2_3
    main.cpp
)

qt_add_qml_module(app1_2_3
    URI 1_2_3
    VERSION 1.0
    QML_FILES
    Main.qml
        QML_FILES GameOver.qml
        RESOURCES iconca.png
        RESOURCES images.qrc
)

# Qt for iOS sets MACOSX_BUNDLE_GUI_IDENTIFIER automatically since Qt 6.1.
# If you are developing for iOS or macOS you should consider setting an
# explicit, fixed bundle identifier manually though.
set_target_properties(app1_2_3 PROPERTIES
#    MACOSX_BUNDLE_GUI_IDENTIFIER com.example.app1_2_3
    MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
    MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
    MACOSX_BUNDLE TRUE
    WIN32_EXECUTABLE TRUE
)

target_link_libraries(app1_2_3
    PRIVATE Qt6::Quick
)

include(GNUInstallDirs)
install(TARGETS app1_2_3
    BUNDLE DESTINATION .
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
