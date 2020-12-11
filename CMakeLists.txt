cmake_minimum_required(VERSION 3.19)


project ("lmt_ua_server")

add_executable (${PROJECT_NAME} "lmt_ua_server.cpp" "lmt_ua_server.h")


# -----------------------------------
# open62541 specific settings - BEGIN
# -----------------------------------
set(UA_ENABLE_AMALGAMATION ON CACHE BOOL "" FORCE)
set(UA_LOGLEVEL 300)
add_subdirectory ("open62541")

set_source_files_properties("${PROJECT_BINARY_DIR}/open62541/open62541.c" PROPERTIES GENERATED TRUE)
set(${PROJECT_NAME}_SRCS ${${PROJECT_NAME}_SRCS} "${PROJECT_BINARY_DIR}/open62541/open62541.c")
include_directories("${PROJECT_BINARY_DIR}/open62541/")
# -----------------------------------
# open62541 specific settings - END
# -----------------------------------

add_dependencies(${PROJECT_NAME} open62541 open62541-amalgamation-source open62541-amalgamation-header) 

target_link_libraries(${PROJECT_NAME} open62541)