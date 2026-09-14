cmake_minimum_required(VERSION 3.16)
project(WithLand VERSION 1.0.0 LANGUAGES CXX)

# ============================================
# ОБЩИЕ НАСТРОЙКИ
# ============================================
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

option(ENABLE_GUI "Build GUI (Raylib). OFF = TUI" ON)

# ============================================
# ИСХОДНИКИ ЯДРА (без main.cpp)
# ============================================
set(CORE_SOURCES
    src/core/Colony.cpp
    src/core/Colonist.cpp
    src/core/Wedding.cpp
    src/core/Event.cpp
    src/core/Enum.cpp
    src/core/DayReport.cpp
    src/common/common.cpp
    src/common/FileManager.cpp
    src/common/Logger.cpp
)

# ============================================
# GUI ИЛИ TUI
# ============================================
if(ENABLE_GUI)
    list(APPEND CORE_SOURCES
        src/gui/GuiApp.cpp
        src/gui/lib/initWindowApp.cpp
        src/gui/lib/DataApp.cpp
    )

    # Ставим опции ДО FetchContent_Declare
    set(BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
    set(BUILD_GAMES    OFF CACHE BOOL "" FORCE)

    include(FetchContent)
    FetchContent_Declare(
        raylib
        GIT_REPOSITORY "https://github.com/raysan5/raylib.git"
        GIT_TAG        "5.5"
        GIT_SHALLOW    TRUE
    )
    FetchContent_MakeAvailable(raylib)

    message(STATUS "🔵 Building with GUI support (Raylib)")
else()
    list(APPEND CORE_SOURCES src/tui/ConsoleUI.cpp)
    message(STATUS "🟢 Building with TUI support (Console)")
endif()

# ============================================
# WARNINGS (интерфейсная либа)
# ============================================
add_library(withland_warnings INTERFACE)
if(MSVC)
    target_compile_options(withland_warnings INTERFACE /W4 /permissive-)
else()
    target_compile_options(withland_warnings INTERFACE
        -Wall -Wextra -Wpedantic -Wshadow
    )
endif()

# ============================================
# ЯДРО — статическая библиотека
# ============================================
add_library(withland_core STATIC ${CORE_SOURCES})

target_include_directories(withland_core PUBLIC
    ${CMAKE_SOURCE_DIR}/include
    ${CMAKE_SOURCE_DIR}/src
)
target_link_libraries(withland_core PUBLIC withland_warnings)

if(ENABLE_GUI)
    target_link_libraries(withland_core PUBLIC raylib)

    if(APPLE)
        target_link_libraries(withland_core PUBLIC
            "-framework CoreVideo"
            "-framework IOKit"
            "-framework Cocoa"
            "-framework OpenGL"
        )
    endif()
endif()

# ============================================
# КОПИРОВАНИЕ РЕСУРСОВ — одна функция на все цели
# ============================================
function(withland_copy_resources target)
    if(NOT ENABLE_GUI)
        return()
    endif()
    add_custom_command(TARGET ${target} POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_directory
            "${CMAKE_SOURCE_DIR}/resources"
            "$<TARGET_FILE_DIR:${target}>/resources"
        COMMENT "Копирование ресурсов для ${target}..."
    )
endfunction()

# ============================================
# ЦЕЛЬ 1: WithLand — чистый .app (без терминала)
# ============================================
add_executable(WithLand src/main.cpp)
target_link_libraries(WithLand PRIVATE withland_core)

if(ENABLE_GUI)
    # --- Иконка macOS ---
    if(APPLE)
        set(ICON_FILE "${CMAKE_SOURCE_DIR}/resources/assets/appIcon.icns")
        if(EXISTS ${ICON_FILE})
            set_source_files_properties(${ICON_FILE} PROPERTIES
                MACOSX_PACKAGE_LOCATION Resources)
            target_sources(WithLand PRIVATE ${ICON_FILE})
        endif()

        set_target_properties(WithLand PROPERTIES
            MACOSX_BUNDLE TRUE
            MACOSX_BUNDLE_INFO_PLIST       "${CMAKE_SOURCE_DIR}/Info.plist"
            MACOSX_BUNDLE_GUI_IDENTIFIER   "com.sharzhukov.withland"
            MACOSX_BUNDLE_BUNDLE_NAME      "WithLand"
            MACOSX_BUNDLE_ICON_FILE        "appIcon"
            MACOSX_BUNDLE_SHORT_VERSION_STRING "${PROJECT_VERSION}"
            XCODE_ATTRIBUTE_CODE_SIGN_IDENTITY ""
            XCODE_ATTRIBUTE_CODE_SIGNING_ALLOWED "NO"
        )
        message(STATUS "🍎 WithLand → macOS .app bundle")
    endif()

    # --- Иконка Windows (без консольного окна) ---
    if(WIN32)
        set_target_properties(WithLand PROPERTIES WIN32_EXECUTABLE TRUE)
        if(MSVC)
            target_link_options(WithLand PRIVATE /ENTRY:mainCRTStartup)
        endif()

        set(ICON_FILE "${CMAKE_SOURCE_DIR}/resources/assets/appIcon.ico")
        if(EXISTS ${ICON_FILE})
            configure_file(
                "${CMAKE_SOURCE_DIR}/resources/assets/appIcon.rc.in"
                "${CMAKE_CURRENT_BINARY_DIR}/appIcon.rc"
                @ONLY
            )
            target_sources(WithLand PRIVATE "${CMAKE_CURRENT_BINARY_DIR}/appIcon.rc")
        endif()
        message(STATUS "🪟 WithLand → Windows GUI app (no console)")
    endif()
endif()

withland_copy_resources(WithLand)

# ============================================
# ЦЕЛЬ 2: WithLandLog — app + терминал с логами
# ============================================
if(ENABLE_GUI)
    add_executable(WithLandLog src/main.cpp)
    target_link_libraries(WithLandLog PRIVATE withland_core)

    # Макрос, по которому код понимает: работаем в log-режиме
    target_compile_definitions(WithLandLog PRIVATE WITHLAND_LOG_MODE)

    # macOS: без MACOSX_BUNDLE → запуск из терминала, stdout/stderr в консоль
    # Windows: без WIN32_EXECUTABLE → консольное окно рядом с raylib
    withland_copy_resources(WithLandLog)

    message(STATUS "🐞 WithLandLog → console + GUI (log mode)")
endif()

# ============================================
# ИНФОРМАЦИЯ
# ============================================
if(ENABLE_GUI)
    set(_targets "WithLand, WithLandLog")
else()
    set(_targets "WithLand")
endif()

message(STATUS "")
message(STATUS "=====================================")
message(STATUS "Project:      ${PROJECT_NAME}")
message(STATUS "Version:      ${PROJECT_VERSION}")
message(STATUS "Build Type:   ${CMAKE_BUILD_TYPE}")
message(STATUS "C++ Standard: ${CMAKE_CXX_STANDARD}")
message(STATUS "GUI Support:  ${ENABLE_GUI}")
message(STATUS "Targets:      ${_targets}")
message(STATUS "=====================================")
message(STATUS "")