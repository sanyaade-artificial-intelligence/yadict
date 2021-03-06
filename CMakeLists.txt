cmake_minimum_required(VERSION 2.6)
project(shanghainesedict)
include_directories(
    src
)

file (
    GLOB
    controllers_files
    src/controllers/*
)

file (
    GLOB
    models_files
    src/models/*
)

file (
    GLOB
    generics_files
    src/generics/*
)

file (
    GLOB
    contents_files
    src/contents/*
)


add_executable(
    shanghainesedict
    src/main.cpp
    src/shanghainesedict.cpp
    ${controllers_files}
    ${models_files}
    ${generics_files}
    ${contents_files}
    templates.cpp
)

target_link_libraries(
    shanghainesedict
    tato
    cppcms
    cppdb
    booster
    sqlite3
    tokyodystopia
)
add_custom_command(
    OUTPUT templates.cpp
    COMMAND ../tools/cppcms_tmpl_cc 
        ${CMAKE_CURRENT_SOURCE_DIR}/src/views/*/*.tmpl 
        ${CMAKE_CURRENT_SOURCE_DIR}/src/views/*.tmpl
        -o templates.cpp
    DEPENDS
        ${CMAKE_CURRENT_SOURCE_DIR}/src/views/*/*.tmpl 
        ${CMAKE_CURRENT_SOURCE_DIR}/src/views/*.tmpl
)

