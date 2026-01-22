if("${POLYSCOPE_BACKEND_OPENGL3_GLFW}")

  ## Glad
  if(NOT TARGET glad)
    add_subdirectory(deps/glad)
  endif()

  ## GLFW
  find_package(glfw3 REQUIRED)
  if(NOT TARGET glfw)
    set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
    set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
    set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
    set(GLFW_INSTALL OFF CACHE BOOL "" FORCE)
    add_subdirectory(deps/glfw)
  endif()
endif()

## glm
find_package(glm CONFIG REQUIRED)
add_compile_definitions(GLM_ENABLE_EXPERIMENTAL)
if(NOT TARGET glm::glm)
  add_subdirectory(deps/glm)
  target_compile_definitions(glm INTERFACE GLM_ENABLE_EXPERIMENTAL)
  set_target_properties(glm PROPERTIES LINKER_LANGUAGE CXX)
endif()

## Imgui
find_package(imgui REQUIRED)
if(NOT TARGET imgui::imgui)
  add_subdirectory(deps/imgui)
endif()

## Json
find_package(nlohmann_json REQUIRED)
if(NOT TARGET nlohmann_json::nlohmann_json)
  add_subdirectory(deps/json)
endif()

## MarchingCube
if(NOT TARGET MarchingCube::MarchingCube)
  add_subdirectory(deps/MarchingCubeCpp)
endif()

## stb
if(NOT TARGET stb)
  add_subdirectory(deps/stb)
endif()
