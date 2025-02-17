
# Collect source files into the "sources" variable and unit test files into the
# "gtest_sources" variable
ign_get_libsources_and_unittests(sources gtest_sources)

# Create the library target
ign_create_core_library(SOURCES ${sources} CXX_STANDARD ${c++standard})

# Build the unit tests
ign_build_tests(TYPE UNIT SOURCES ${gtest_sources})

# graph namespace
add_subdirectory(graph)

# Bindings subdirectories
if (pybind11_FOUND AND NOT SKIP_PYBIND11)
  add_subdirectory(python_pybind11)
endif()

if (SWIG_FOUND AND NOT SKIP_SWIG)
  add_subdirectory(ruby)
endif()
