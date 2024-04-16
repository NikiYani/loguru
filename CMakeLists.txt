cmake_minimum_required(VERSION 3.1)

project(loguru)

set(CMAKE_POSITION_INDEPENDENT_CODE ON)

add_library(${PROJECT_NAME} loguru.hpp loguru.cpp)
add_library(${PROJECT_NAME}::${PROJECT_NAME} ALIAS ${PROJECT_NAME})

target_compile_definitions(
    ${PROJECT_NAME}
    PUBLIC
        LOGURU_FILENAME_WIDTH=16
        LOGURU_THREADNAME_WIDTH=8
        LOGURU_SCOPE_TIME_PRECISION=3
        LOGURU_WITH_STREAMS=1
        LOGURU_WITH_FILEABS=1
        LOGURU_REDEFINE_ASSERT=1
        LOGURU_REPLACE_GLOG=1
        BOOST_ASIO_DISABLE_CONCEPTS
)

target_include_directories(${PROJECT_NAME} INTERFACE ${PROJECT_NAME})

target_link_libraries(${PROJECT_NAME} PRIVATE dl pthread)
