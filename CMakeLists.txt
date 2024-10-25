cmake_minimum_required (VERSION 3.8)

if (POLICY CMP0141)
  cmake_policy(SET CMP0141 NEW)
  set(CMAKE_MSVC_DEBUG_INFORMATION_FORMAT "$<IF:$<AND:$<C_COMPILER_ID:MSVC>,$<CXX_COMPILER_ID:MSVC>>,$<$<CONFIG:Debug,RelWithDebInfo>:EditAndContinue>,$<$<CONFIG:Debug,RelWithDebInfo>:ProgramDatabase>>")
endif()

set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)

project ("UEcodegeneration")

set(CMAKE_CXX_STANDARD 11)

set(THIRDPARTYPATH thirdparty)

include_directories(${THIRDPARTYPATH}\\glfw\\include)
include_directories(${THIRDPARTYPATH}\\imgui)
include_directories(${THIRDPARTYPATH}\\imgui\\beckends)

#link_directories命令用于向CMake添加链接器搜索库文件的目录。这意味着，当链接器需要查找库文件时，它会在这些目录中搜索。
link_directories(${THIRDPARTYPATH}\\glfw\\lib-vc2022)#使用cl编译
#link_directories(${THIRDPARTYPATH}\\glfw\\lib-mingw-w64)#使用mingw编译

file(GLOB_RECURSE IMGUI_SRCS ${THIRDPARTYPATH}/imgui/*.cpp)

add_executable(imguiApp main.cpp ${IMGUI_SRCS})
#glfw必要
target_link_libraries(imguiApp glfw3.lib opengl32.lib)