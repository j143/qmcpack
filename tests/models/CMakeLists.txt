
# The errors on the total energy are numerical noise, not statistical errors
IF(QMC_MIXED_PRECISION)
  LIST(APPEND SHO_SCALARS "totenergy" "0.45  0.00000002")
ELSE()
  LIST(APPEND SHO_SCALARS "totenergy" "0.45  4.0e-14")
ENDIF()
  LIST(APPEND SHO_SCALARS "kinetic"   "0.225 0.0028")
  LIST(APPEND SHO_SCALARS "potential" "0.225 0.0028")
  LIST(APPEND SHO_SCALARS "latdev"    "1.0   0.013")

  QMC_RUN_AND_CHECK(short-sho-vmc
    "${CMAKE_SOURCE_DIR}/tests/models/sho"
    m5
    vmc_sho.xml
    1 16
    TRUE
    0 SHO_SCALARS # VMC
  )
  
  SIMPLE_RUN_AND_CHECK(short-sho-grad_lap
    "${CMAKE_SOURCE_DIR}/tests/models/sho"
    grad_lap.xml
    1 1
    ../../solids/bccH_3x3x3_ae/short-bccH_3x3x3_ae-deriv-1-1/check_grad_lap.py
  )
