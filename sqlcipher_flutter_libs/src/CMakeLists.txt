cmake_minimum_required(VERSION 3.10)
set(PROJECT_NAME "sqlcipher_flutter_libs")
project(${PROJECT_NAME} LANGUAGES C CXX)

option(OPENSSL_USE_STATIC_LIBS "Whether to prefer linking to OpenSSL statically" ON)
find_package(OpenSSL REQUIRED)

add_library(sqlcipher_flutter_libs SHARED
  "sqlcipher.c"
)

set_target_properties(sqlcipher_flutter_libs PROPERTIES
  PUBLIC_HEADER sqlite3.h
  OUTPUT_NAME sqlcipher
)

target_compile_definitions(sqlcipher_flutter_libs PUBLIC DART_SHARED_LIB)

# Note: Keep in sync with https://github.com/simolus3/sqlite-native-libraries/blob/master/sqlite3-native-library/cpp/CMakeLists.txt
target_compile_definitions(sqlcipher_flutter_libs PRIVATE
  SQLITE_HAS_CODEC
  SQLITE_DQS=0
  SQLITE_THREADSAFE=1
  SQLITE_DEFAULT_MEMSTATUS=0
  SQLITE_TEMP_STORE=2
  SQLITE_MAX_EXPR_DEPTH=0
  SQLITE_OMIT_AUTHORIZATION
  SQLITE_OMIT_DECLTYPE
  SQLITE_OMIT_DEPRECATED
  SQLITE_OMIT_PROGRESS_CALLBACK
  SQLITE_OMIT_SHARED_CACHE
  SQLITE_OMIT_TCL_VARIABLE
  SQLITE_OMIT_TRACE
  SQLITE_USE_ALLOCA
  SQLITE_UNTESTABLE
  SQLITE_HAVE_ISNAN
  SQLITE_ENABLE_DBSTAT_VTAB
  SQLITE_ENABLE_FTS5
  SQLITE_ENABLE_JSON1
  SQLITE_ENABLE_RTREE
)
