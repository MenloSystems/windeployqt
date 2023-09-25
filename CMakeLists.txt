cmake_minimum_required(VERSION 3.16)

project(windeployqt
    LANGUAGES CXX
    DESCRIPTION "Qt Windows Deployment Tool"
)

find_package(Qt6 REQUIRED COMPONENTS Core)
find_package(Qt6Core REQUIRED COMPONENTS Private)

add_executable(windeployqt
    qmlutils.cpp qmlutils.h
    qtmoduleinfo.cpp qtmoduleinfo.h
    utils.cpp utils.h
    main.cpp
)

target_link_libraries(windeployqt
    PRIVATE
        Qt::Core
        Qt::CorePrivate
        $<$<BOOL:${WIN32}>:shlwapi>
)
target_compile_definitions(windeployqt
    PRIVATE
        QT_NO_CAST_FROM_ASCII
        QT_NO_CAST_TO_ASCII
        QT_NO_FOREACH
)

install(TARGETS windeployqt
        RUNTIME DESTINATION bin
)
