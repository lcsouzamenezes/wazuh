# Defs
set(SRC_DIR ${CMAKE_CURRENT_LIST_DIR}/src)
set(INC_DIR ${CMAKE_CURRENT_LIST_DIR}/include)
set(IFACE_DIR ${CMAKE_CURRENT_LIST_DIR}/interface)

add_library(logpar STATIC src/logpar.cpp)
target_include_directories(logpar
PUBLIC
  include
PRIVATE
  include/logpar
)
target_link_libraries(logpar PUBLIC hlp fmt base schemf::ischema parsec)

# Tests
if(ENGINE_BUILD_TEST)
set(TEST_SRC_DIR ${CMAKE_CURRENT_LIST_DIR}/test/src)
set(UNIT_SRC_DIR ${TEST_SRC_DIR}/unit)

add_executable(logpar_utest
    ${UNIT_SRC_DIR}/logpar_test.cpp
)
target_link_libraries(logpar_utest PRIVATE logpar gtest_main schemf::mocks)

endif(ENGINE_BUILD_TEST)
