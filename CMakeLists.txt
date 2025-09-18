project(imgui)

set(IMGUI_SOURCES
    imgui.cpp
    imgui_demo.cpp
    imgui_draw.cpp
    imgui_tables.cpp
    imgui_widgets.cpp
    backends/imgui_impl_glfw.cpp
    backends/imgui_impl_vulkan.cpp
)

add_library(imgui STATIC ${IMGUI_SOURCES})

target_include_directories(imgui PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/backends
)

target_compile_definitions(imgui PUBLIC
    IMGUI_ENABLE_DOCKING
    IMGUI_DEFINE_MATH_OPERATORS    # Add this line
)

find_package(Vulkan REQUIRED)

target_link_libraries(imgui PUBLIC 
    ${Vulkan_LIBRARIES}
    glfw
)

target_include_directories(imgui PUBLIC 
    ${Vulkan_INCLUDE_DIRS}
)

if(WIN32)
    target_compile_definitions(imgui PRIVATE _CRT_SECURE_NO_WARNINGS)
endif()
