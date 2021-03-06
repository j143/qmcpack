#//////////////////////////////////////////////////////////////////////////////////////
#// This file is distributed under the University of Illinois/NCSA Open Source License.
#// See LICENSE file in top directory for details.
#//
#// Copyright (c) 2016 Jeongnim Kim and QMCPACK developers.
#//
#// File developed by: Ye Luo, yeluo@anl.gov, Argonne National Laboratory
#//
#// File created by: Mark Dewing, markdewing@gmail.com, University of Illinois at Urbana-Champaign
#//////////////////////////////////////////////////////////////////////////////////////



SET(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${QMCPACK_UNIT_TEST_DIR})

SET(SRC_DIR numerics)
SET(UTEST_EXE test_${SRC_DIR})
SET(UTEST_NAME unit_test_${SRC_DIR})



SET(UTEST_SRCS test_grid_functor.cpp test_nr_spline.cpp test_stdlib.cpp test_bessel.cpp
               test_ylm.cpp test_e2iphi.cpp test_aligned_allocator.cpp
               test_gaussian_basis.cpp test_cartesian_tensor.cpp test_soa_cartesian_tensor.cpp)

# Run gen_gto.py to create these files.  They may take a long time to compile.
#SET(UTEST_SRCS ${UTEST_SRCS} test_full_cartesian_tensor.cpp test_full_soa_cartesian_tensor.cpp)

ADD_EXECUTABLE(${UTEST_EXE} ${UTEST_SRCS})


TARGET_LINK_LIBRARIES(${UTEST_EXE} qmcutil ${QMC_UTIL_LIBS} ${MPI_LIBRARY})

#ADD_TEST(NAME ${UTEST_NAME} COMMAND "${QMCPACK_UNIT_TEST_DIR}/${UTEST_EXE}")
ADD_UNIT_TEST(${UTEST_NAME} "${QMCPACK_UNIT_TEST_DIR}/${UTEST_EXE}")
SET_TESTS_PROPERTIES(${UTEST_NAME} PROPERTIES LABELS "unit")

