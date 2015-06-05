include_directories("${PROJECT_SOURCE_DIR}/libclandmark")

find_package( OpenCV REQUIRED )
include_directories(${OpenCV_INCLUDE_DIR})

include_directories(${PROJECT_SOURCE_DIR}/3rd_party/rapidxml-1.13)
include_directories(${PROJECT_SOURCE_DIR}/3rd_party/CImg-1.5.6)

# propagate precision definition
if(DOUBLE_PRECISION)
    add_definitions( -DDOUBLE_PRECISION=1 )
else(DOUBLE_PRECISION)
    add_definitions( -DDOUBLE_PRECISION=0 )
endif(DOUBLE_PRECISION)

## Several examples using flandmark
set(EXAMPLES static_input video_input)
foreach(var ${EXAMPLES})
    add_executable(${var} ${var}.cpp)
    target_link_libraries(${var} flandmark ${OpenCV_LIBS})
endforeach()

install(TARGETS ${EXAMPLES} DESTINATION clandmark/examples)
