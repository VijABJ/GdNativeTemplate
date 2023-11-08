
cmake_minimum_required (VERSION 3.4)
project (SrgGodotExtensionsTemplate)

set_property (GLOBAL PROPERTY USE_FOLDERS OFF)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# always activate the highest warning level
if(ANDROID)
  set (ANDROID_API_LEVEL 19)
  add_definitions(-D__GXX_EXPERIMENTAL_CXX0X__)
  add_compile_options(
	  -g -ffor-scope -fno-exceptions -pipe -ffunction-sections 
	  -fdata-sections -ffast-math -pedantic -Werror -Wnon-virtual-dtor 
	  -Wsign-promo -fvisibility=hidden -fvisibility-inlines-hidden 
	  -Wstrict-null-sentinel -Os -funroll-all-loops -fpeel-loops 
	  -ftree-vectorize
	)
elseif(MSVC)
  add_compile_options(/W4 /EHsc /utf-8)
  set(CMAKE_CXX_FLAGS_RELEASE "/MT")
  set(CMAKE_CXX_FLAGS_DEBUG "/MD")
elseif(CMAKE_COMPILER_IS_GNUCC OR CMAKE_COMPILER_IS_GNUCXX)
  add_compile_options(-g -Wall -Wno-long-long -pedantic)
endif()

# this is for godot header files
add_compile_definitions(TYPED_METHOD_BIND NOMINMAX GUID_WINDOWS)

# where we want stuff to go
set(LIB_DESTINATION ${CMAKE_SOURCE_DIR}/__binaries)
set(EXE_DESTINATION ${CMAKE_SOURCE_DIR}/__binaries)

# set destinations
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${EXE_DESTINATION})
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${LIB_DESTINATION})
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${LIB_DESTINATION})

# include directories. build global stuff
include_directories("${CMAKE_SOURCE_DIR}/godot-cpp/gdextension")
include_directories("${CMAKE_SOURCE_DIR}/godot-cpp/include")
include_directories("${CMAKE_SOURCE_DIR}/godot-cpp/gen/include")

link_directories("${CMAKE_SOURCE_DIR}/godot-cpp/bin")

add_compile_definitions($<$<CONFIG:Debug>:_ITERATOR_DEBUG_LEVEL=0>)
add_compile_definitions($<$<CONFIG:Debug>:DEBUG>)
add_compile_definitions($<$<CONFIG:Debug>:_DEBUG>)

add_compile_definitions($<$<CONFIG:Release>:_ITERATOR_DEBUG_LEVEL=0>)

# the test module
#add_library(Catch INTERFACE)

#add_subdirectory(SrgGdHelpers)
add_subdirectory(SrgGdUtilities)

#enable_testing()
#add_test(
#  NAME "name-of-test"
#  WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}/bin
#  COMMAND output.exe)

