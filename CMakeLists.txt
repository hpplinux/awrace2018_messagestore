cmake_minimum_required(VERSION 3.0)

project(queue_race)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_BUILD_TYPE Release)

include_directories(${CMAKE_SOURCE_DIR}/include)

set(SOURCE_FILES queue_store.cc storage.cc)

add_library(queue_race SHARED ${SOURCE_FILES})

target_link_libraries(queue_race tbb tcmalloc)

# In case you need boost::filesystem
#target_link_libraries(queue_race boost_filesystem boost_system)

# In case you need lz4
target_link_libraries(queue_race lz4)

# In case you need lzma
# target_link_libraries(queue_race lzma)

# In case you need snappy
target_link_libraries(queue_race snappy)

# In case you need lz
#target_link_libraries(queue_race z)

add_subdirectory(example)
add_subdirectory(third)

install(DIRECTORY ${CMAKE_SOURCE_DIR}/include/
        DESTINATION include)
install(TARGETS queue_race
        LIBRARY DESTINATION lib)
