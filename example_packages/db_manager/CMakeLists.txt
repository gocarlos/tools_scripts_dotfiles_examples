CMAKE_MINIMUM_REQUIRED(VERSION 3.5 FATAL_ERROR)

SET(DB_MANAGER "db_manager")

IF(NOT PROJECT_NAME)
  PROJECT (${DB_MANAGER})
ENDIF(NOT PROJECT_NAME)

SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c++11")

FIND_PACKAGE(Threads)

INCLUDE("${CMAKE_CURRENT_LIST_DIR}/cmake/settings.cmake")

ADD_SUBDIRECTORY("${CMAKE_CURRENT_LIST_DIR}/vendor/sqlite3")

INCLUDE_DIRECTORIES(
  ${CMAKE_CURRENT_LIST_DIR}/include
  ${SQLITE3_INCLUDE_DIRS}
)

ADD_EXECUTABLE(save_to_sqlite_db src/save_to_sqlite_db.cpp)
TARGET_LINK_LIBRARIES(save_to_sqlite_db
  Threads::Threads
  sqlite3
  dl
)
