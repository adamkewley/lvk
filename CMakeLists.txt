cmake_minimum_required(VERSION 3.10)

project(learn-vulkan VERSION 0.0.1 LANGUAGES CXX)

find_package(glm REQUIRED CONFIG)

add_executable(lvk src/lvk.cpp)
target_compile_features(lvk INTERFACE cxx_std_17)