#
# The Callpath class itself is a separate library b/c it's used by 
# tools and other libraries (like libeffort).
#
set(CALLPATH_SOURCES
	Callpath.cpp
	CallpathRuntime.cpp
	FrameId.cpp
	ModuleId.cpp
	FrameInfo.cpp
	Translator.cpp
	../util/io_utils.cpp
	../util/string_utils.cpp)

add_library(callpath SHARED ${CALLPATH_SOURCES})
target_link_libraries(callpath ${CALLPATH_STACKWALKER_EXTRA_LIBRARIES} ${CALLPATH_STACKWALKER_LIBRARIES})
###target_link_libraries(callpath ${MPI_C_LIBRARIES})
SET (TEMP "")
FOREACH (skip_flag ${MPI_CXX_SKIP_FLAGS})
    SET (TEMP "${TEMP} ${skip_flag}")
ENDFOREACH (skip_flag)
SET_TARGET_PROPERTIES(callpath PROPERTIES COMPILE_FLAGS "${TEMP}")

install(TARGETS callpath DESTINATION lib EXPORT callpath-libs)

set(CALLPATH_HEADERS
	FrameId.h
	Callpath.h
	CallpathRuntime.h
  UniqueId.h
	ModuleId.h
	FrameInfo.h
	Translator.h
	safe_bool.h)

install(FILES ${CALLPATH_HEADERS} DESTINATION include)

include_directories(
  ${CMAKE_CURRENT_BINARY_DIR}
       ${MPI_INCLUDE_PATH})
