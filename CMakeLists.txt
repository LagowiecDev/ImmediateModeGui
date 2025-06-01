set(IMGUI_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(IMGUI_BACKENDS_DIR "${IMGUI_DIR}/backends")
set(IMGUI_OPENGL 0)

set(
	imgui_sources  
	"${IMGUI_DIR}/imgui.cpp"
	"${IMGUI_DIR}/imgui_demo.cpp"
	"${IMGUI_DIR}/imgui_draw.cpp"
	"${IMGUI_DIR}/imgui_tables.cpp"
	"${IMGUI_DIR}/imgui_widgets.cpp"
)

find_package(SDL2 QUIET)

if (GLFW_FOUND)
	list(APPEND imgui_sources "${IMGUI_BACKENDS_DIR}/imgui_impl_sdl2.cpp")
endif()

find_package(SDL3 QUIET)

if (SDL3_FOUND)
	list(APPEND imgui_sources "${IMGUI_BACKENDS_DIR}/imgui_impl_sdl3.cpp")
endif()

if(IMGUI_OPENGL EQUAL 1 OR IMGUI_OPENGL EQUAL 2)
    list(APPEND imgui_sources "${IMGUI_BACKENDS_DIR}/imgui_impl_opengl2.cpp")
endif()

if(IMGUI_OPENGL EQUAL 1 OR IMGUI_OPENGL EQUAL 3)
    list(APPEND imgui_sources "${IMGUI_BACKENDS_DIR}/imgui_impl_opengl3.cpp")
endif()

add_library("imgui"
	${imgui_sources}
)

target_include_directories("imgui" PRIVATE "${IMGUI_DIR}")
