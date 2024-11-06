cmake_minimum_required(VERSION 3.28)

cmake_policy(SET CMP0091 NEW)

project(tkrzwVcpkgIntegration
  VERSION "0.0.1"
  DESCRIPTION "Project using upstream-bundled examples to test vcpkg integration"
  HOMEPAGE_URL "https://dbmx.net/tkrzw/"
  LANGUAGES C CXX
)

include(CPack)

set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>$<IF:$<STREQUAL:${BUILD_SHARED_LIBS},SHARED>,DLL,>")

find_package(Threads)
find_package(tkrzw CONFIG REQUIRED)

set(EXAMPLES_CXX
	helloworld
	accesscounter
	transfer
	hashdbm_ex1
	hashdbm_ex2
	hashdbm_ex3
	treedbm_ex1
	treedbm_ex2
	treedbm_ex3
	treedbm_ex4
	skipdbm_ex1
	skipdbm_ex2
	skipdbm_ex3
	tinydbm_ex1
	tinydbm_ex2
	babydbm_ex1
	babydbm_ex2
	cachedbm_ex1
	stdtreedbm_ex1
	stdtreedbm_ex2
	polydbm_ex1
	sharddbm_ex1
	asyncdbm_ex1
	struct_ex1
	fileindex_ex1
	stdindex_ex1
	polyindex_ex1
	invindex_ex1
)
set(EXAMPLES_C
	langc_ex1
	langc_ex2
	langc_ex3
)

foreach(example IN LISTS EXAMPLES_C)
	add_executable(${example})
	target_sources(${example} PRIVATE tkrzw/example/${example}.c)
	target_link_libraries(${example} PRIVATE tkrzw)
endforeach()

foreach(example IN LISTS EXAMPLES_CXX)
	add_executable(${example})
	target_sources(${example} PRIVATE tkrzw/example/${example}.cc)
	target_link_libraries(${example} PRIVATE tkrzw)
endforeach()

enable_testing()
foreach(example IN LISTS EXAMPLES_C EXAMPLES_CXX)
	add_test(NAME ${example} COMMAND ${example})
endforeach()

install(TARGETS ${EXAMPLES_C} ${EXAMPLES_CXX}
	BUNDLE DESTINATION .
	RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
