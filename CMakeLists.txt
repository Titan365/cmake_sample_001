# CMakeのバージョンを設定
cmake_minimum_required(VERSION 3.23)

# プロジェクト名と使用する言語を設定
project(cmake_sample C)

#GoogleTestの"CMakeLists.txt"を配置しているパスを設定
set(GTEST_PATH ./gtest/googletest-1.13.0)
add_subdirectory(${GTEST_PATH})
if(EXISTS ${GTEST_PATH})
	message("GoogleTestをBuildします。")
else()
	message("GoogleTestが存在しません。set(GTEST_PATH ...)にgoogletestが格納されているフォルダを設定してください。")
endif()

#GDBのオプション
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -g -O0")

#build
add_executable(test_sample main.c)

# gcovのための作法
target_compile_options(test_sample PUBLIC -coverage)
target_link_options(test_sample PUBLIC -coverage)



