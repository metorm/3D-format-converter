cmake_minimum_required(VERSION 2.8.2)

set(PROJ_NAME "step2wrl")

# ==========================================
# This cmake file is for building the project with occ 6.3.1
# there is no stable cmake package
# so, edit following lines to set correct paths
set(OCC_MAIN_DIR "C:/OpenCASCADE6.3.0")
set(OCC_INCLUDE "${OCC_MAIN_DIR}/ros/inc")
set(OCC_LIB "${OCC_MAIN_DIR}/ros/win32/lib")
# ==========================================

# do not edit below unless you know what you are doing

cmake_policy(SET CMP0048 NEW)
project(${PROJ_NAME} VERSION 0.1.0 LANGUAGES CXX)

# set compiling parameters
include_directories(${OCC_INCLUDE})

set(CMAKE_CXX_FLAGS "/DWNT /EHsc")

set(SOURCE_FILES
	s3d_model.cpp s3d_model.h
	step_mesher.cpp step_mesher.h
	vrml_writer.cpp)

set(LIBS_TO_LINK
	PTKernel TKAdvTools  TKBin  TKBinL  TKBinTObj
	TKBinXCAF  TKBO  TKBool  TKBRep  TKCAF  TKCDF
	TKernel  TKFeat  TKFillet  TKG2d  TKG3d  TKGeomAlgo
	TKGeomBase  TKHLR  TKIGES  TKLCAF  TKMath  TKMesh
	TKMeshVS  TKNIS  TKOffset  TKPCAF  TKPLCAF  TKPrim
	TKPShape  TKShapeSchema  TKShHealing  TKStdLSchema
	TKStdSchema  TKSTEP209  TKSTEP  TKSTEPAttr  TKSTEPBase
	TKSTL  TKTObj  TKTopAlgo TKVRML  TKXCAF
	TKXCAFSchema  TKXDEIGES  TKXDESTEP  TKXMesh  TKXml
	TKXmlL  TKXmlTObj  TKXmlXCAF  TKXSBase  TKService
	TKOpenGl  TKV3d)

add_executable(${PROJ_NAME} ${SOURCE_FILES})

foreach(targetLibrary ${LIBS_TO_LINK})
	message(STATUS "Finding and linking ${targetLibrary} ...")

	find_library(OCC_LIB_${targetLibrary} NAMES ${targetLibrary} PATHS ${OCC_LIB})
	
	if(NOT OCC_LIB_${targetLibrary})
		message(FATAL_ERROR "${targetLibrary} not found!")
	endif()
	
	target_link_libraries(${PROJ_NAME} ${OCC_LIB_${targetLibrary}})
	
endforeach(targetLibrary)