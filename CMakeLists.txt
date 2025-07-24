cmake_minimum_required(VERSION 3.20)

project(weight-loss, CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(PROVIDED_SRC_FILES
  src/person.h
  # add header files here

)

# per class do set and its .h and .cpp files
set(PERSON_SRC_FILES
  src/person.h
  src/person.cpp
)


add_executable(main
  ${PROVIDED_SRC_FILES}
  ${PERSON_SRC_FILES}
  src/main.cpp
)

find_package(GTest)
if (GTest_FOUND)
  set(KANEC_TEST_FILES
    gtest/gt-main
    gtest/gt-person
  )

  add_executable(kanec-gtests
    ${KANEC_TEST_FILES}
    ${PROVIDED_SRC_FILES}
    ${PERSON_SRC_FILES}
  )
  target_include_directories(kanec-gtests PRIVATE src ${GTEST_INCLUDE_DIRS})
  target_link_libraries(kanec-gtests PRIVATE ${GTEST_LIBRARIES})
endif()

