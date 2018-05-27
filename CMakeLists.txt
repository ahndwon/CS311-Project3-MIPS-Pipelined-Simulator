cmake_minimum_required(VERSION 3.8)
project(Project3)

set(CMAKE_CXX_STANDARD 11)

set(SOURCE_FILES
        cs311.c
        parse.c
        parse.h
        run.c
        run.h
        util.c
        util.h)

add_executable(Project3 ${SOURCE_FILES})