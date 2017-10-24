
set(SRCROOT ${PROJECT_SOURCE_DIR}/examples/island)

# all source files
set(SRC ${SRCROOT}/Island.cpp)

# On X11 systems we need to explicitly prepare Xlib for multi-threaded usage
if(SFML_OS_LINUX OR SFML_OS_FREEBSD)
    find_package(X11 REQUIRED)
    if(NOT X11_FOUND)
        message(FATAL_ERROR "X11 library not found")
    endif()
    include_directories(${X11_INCLUDE_DIR})

    # define the island target
    sfml_add_example(island GUI_APP
                     SOURCES ${SRC}
                     DEPENDS sfml-graphics sfml-window sfml-system ${X11_LIBRARIES}
                     RESOURCES_DIR resources)
else()
    # define the island target
    sfml_add_example(island GUI_APP
                     SOURCES ${SRC}
                     DEPENDS sfml-graphics sfml-window sfml-system
                     RESOURCES_DIR resources)
endif()