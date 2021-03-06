# Define the axisem executable
FILE(GLOB XPOST_PROC_SRCS "${AXISEM_SOURCE_DIR}/SOLVER/UTILS/post_processing.F90" "${AXISEM_SOURCE_DIR}/SOLVER/UTILS/nc_postroutines.F90")
ADD_EXECUTABLE(xpost_processing ${XPOST_PROC_SRCS})

FILE(GLOB XFIELD_TRANSFORM_SRCS "${AXISEM_SOURCE_DIR}/SOLVER/UTILS/field_transform.F90")
ADD_EXECUTABLE(xfield_transform ${XFIELD_TRANSFORM_SRCS})

# Set compile/link flags for post processors
SET(SOLVER_COMPILER_FLAGS "${SOLVER_COMPILER_FLAGS} ${OpenMP_Fortran_FLAGS}")
IF(NETCDF_FOUND)
    SET(SOLVER_COMPILER_FLAGS "${SOLVER_COMPILER_FLAGS} -Dunc")
    TARGET_LINK_LIBRARIES(xpost_processing ${NETCDF_LIBRARIES})
    TARGET_LINK_LIBRARIES(xfield_transform ${NETCDF_LIBRARIES})
ENDIF(NETCDF_FOUND)

SET_TARGET_PROPERTIES(xpost_processing PROPERTIES COMPILE_FLAGS ${SOLVER_COMPILER_FLAGS})
SET_TARGET_PROPERTIES(xpost_processing PROPERTIES LINK_FLAGS ${OpenMP_Fortran_FLAGS})

SET_TARGET_PROPERTIES(xfield_transform PROPERTIES COMPILE_FLAGS ${SOLVER_COMPILER_FLAGS})
SET_TARGET_PROPERTIES(xfield_transform PROPERTIES LINK_FLAGS ${OpenMP_Fortran_FLAGS})

