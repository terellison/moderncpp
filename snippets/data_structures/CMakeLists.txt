# Data structures
add_executable(sequential_containers sequential_containers.cpp)

add_executable(associative_containers associative_containers.cpp)

find_package(PMR)
if (PMR_FOUND)
    add_executable(memory_resource memory_resource.cpp)
else ()
    message("Your compiler does not support *PMR* yet")
endif ()

add_executable(span span.cpp)

add_executable(bitset bitset.cpp)

# Set options to not build pareto examples
# - Cache our own BUILD_EXAMPLES var so that pareto
#   doesn't mess with it
set(BUILD_MATPLOT_TARGETS OFF CACHE BOOL "" FORCE)
set(BUILD_EXAMPLES_PREV ${BUILD_EXAMPLES})
set(BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
FetchContent_Declare(pareto GIT_REPOSITORY https://github.com/alandefreitas/pareto.git GIT_TAG v1.2.0)
FetchContent_MakeAvailable(pareto)
set(BUILD_EXAMPLES ${BUILD_EXAMPLES_PREV} CACHE BOOL "" FORCE)
add_executable(spatial_containers spatial_containers.cpp)
target_link_libraries(spatial_containers PUBLIC pareto)

