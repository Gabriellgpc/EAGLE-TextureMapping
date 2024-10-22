cmake_minimum_required(VERSION 3.10)
project(PatchBasedTextureMapping)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)

# Find OpenCV
find_package(OpenCV REQUIRED)
find_package(OpenMP REQUIRED)
find_package(Eigen3 REQUIRED)
find_package(PCL REQUIRED)

# Include directories
include_directories(${OpenCV_INCLUDE_DIRS} ${EIGEN3_INCLUDE_DIR})
include_directories(${PCL_INCLUDE_DIRS})
include_directories(./lib)
include_directories(./rayint)

link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})
link_directories(./lib)

add_library(Eagle_Utils lib/Eagle_Utils.cpp lib/Eagle_Utils.h)
target_link_libraries(Eagle_Utils
    pcl_io_ply
    ${OpenCV_LIBS}
    ${PCL_LIBRARIES}
)

# Add executable
add_executable(texture_mapping main.cpp getalignresults.cpp getalignresults.h)

# Link libraries
target_link_libraries(texture_mapping
    ${OpenCV_LIBS}
    OpenMP::OpenMP_CXX
    Eigen3::Eigen
    pcl_io_ply
    ${PCL_LIBRARIES}
    Eagle_Utils
)