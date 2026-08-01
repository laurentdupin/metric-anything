cmake_minimum_required(VERSION 3.20)
project(metricanything_native VERSION 0.1.0 LANGUAGES C CXX)

set(MOGE2_NATIVE_SOURCE_DIR
    "${CMAKE_CURRENT_SOURCE_DIR}/../../moge-2/native"
    CACHE PATH "Path to the shared MoGe-2 native operator implementation")
if(NOT EXISTS "${MOGE2_NATIVE_SOURCE_DIR}/CMakeLists.txt")
  message(FATAL_ERROR
    "MOGE2_NATIVE_SOURCE_DIR must identify the pinned MoGe-2 native source")
endif()

# MetricAnything Student PointMap is a MoGe-2 ViT-L fine-tune. The shared
# source builds a distinct family-neutral ABI2 DLL target while keeping the
# final runtime dependency-free.
add_subdirectory("${MOGE2_NATIVE_SOURCE_DIR}"
  "${CMAKE_CURRENT_BINARY_DIR}/moge2-native")
set_target_properties(metricanything_native PROPERTIES
  RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/$<CONFIG>"
  LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/$<CONFIG>"
  ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/$<CONFIG>")
