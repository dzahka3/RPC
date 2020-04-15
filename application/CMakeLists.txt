set(CMAKE_CXX_COMPILER g++)
set(CMAKE_CXX_FLAGS "-DERPC_INFINIBAND=true")

add_definitions(-std=c++11 -march=native -g)
add_definitions(-Wall -Wextra -Werror -pedantic -Wsign-conversion -Wold-style-cast)
add_definitions(-Wno-unused-function -Wno-nested-anon-types -Wno-keyword-macro)

add_executable(server server.cc common.h)
add_executable(client client.cc common.h)
target_include_directories(server PUBLIC ${CMAKE_SOURCE_DIR}/eRPC-master/src)
target_include_directories(client PUBLIC ${CMAKE_SOURCE_DIR}/eRPC-master/src)
target_link_libraries(server erpc pthread numa dl ibverbs)
target_link_libraries(client erpc pthread numa dl ibverbs)
