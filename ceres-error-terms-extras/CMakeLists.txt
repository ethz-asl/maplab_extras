cmake_minimum_required(VERSION 2.8.3)
project(ceres_error_terms_extras)

link_directories(${CATKIN_DEVEL_PREFIX}/lib)

find_package(catkin_simple REQUIRED)
catkin_simple(ALL_DEPS_REQUIRED)

add_definitions(-Wno-enum-compare)

cs_add_library(${PROJECT_NAME}
  src/parameterization/quaternion-param-eigen.cc
  src/parameterization/unit3-param.cc
  src/pose-prior-error-term-eigen.cc)

target_link_libraries(${PROJECT_NAME} pthread)

catkin_add_gtest(test_unit3_parameterization
  test/test_unit3_parameterization.cc)
target_link_libraries(test_unit3_parameterization ${PROJECT_NAME})

catkin_add_gtest(test_quaternion_parameterization_eigen
  test/test_quaternion_eigen_parameterization.cc)
target_link_libraries(test_quaternion_parameterization_eigen ${PROJECT_NAME})

catkin_add_gtest(test_aid_error_term
  test/test_aid_error_term.cc)
target_link_libraries(test_aid_error_term ${PROJECT_NAME})

cs_install()
cs_export()
