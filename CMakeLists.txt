cmake_minimum_required(VERSION 3.4.1)
project(fdk-aac)

set(FDK_AAC_INCLUDES
  libAACdec/include
  libAACenc/include
  libPCMutils/include
  libFDK/include
  libSYS/include
  libMpegTPDec/include
  libMpegTPEnc/include
  libSBRdec/include
  libSBRenc/include
  libArithCoding/include
  libDRCdec/include
  libSACdec/include
	libSACenc/include
)
	
file(GLOB AACDEC_SRC libAACdec/src/*.cpp)
file(GLOB AACENC_SRC libAACenc/src/*.cpp)
file(GLOB PCMUTILS_SRC libPCMutils/src/*.cpp)
file(GLOB FDK_SRC libFDK/src/*.cpp)
file(GLOB SYS_SRC libSYS/src/*.cpp)
file(GLOB MPEGTPDEC_SRC libMpegTPDec/src/*.cpp)
file(GLOB MPEGTPENC_SRC libMpegTPEnc/src/*.cpp)
file(GLOB SBRDEC_SRC libSBRdec/src/*.cpp)
file(GLOB SBRENC_SRC libSBRenc/src/*.cpp)
file(GLOB ARITHCODING_SRC libArithCoding/src/*.cpp)
file(GLOB DRCDEC_SRC libDRCdec/src/*.cpp)
file(GLOB SACDEC_SRC libSACdec/src/*.cpp)
file(GLOB SACENC_SRC libSACenc/src/*.cpp)

set(libfdk_aac_SOURCES
    ${AACDEC_SRC} ${AACENC_SRC}
    ${MPEGTPDEC_SRC} ${MPEGTPENC_SRC}
    ${SBRDEC_SRC} ${SBRENC_SRC}
    ${PCMUTILS_SRC} ${FDK_SRC} ${SYS_SRC}
		${ARITHCODING_SRC} ${DRCDEC_SRC} ${SACDEC_SRC} ${SACENC_SRC}
)


set(aac_enc_SOURCES aac-enc.c wavreader.c)

list(APPEND FDK_AAC_INCLUDES ${CMAKE_CURRENT_SOURCE_DIR})


add_library(AACdec ${AACDEC_SRC})
add_library(AACenc ${AACENC_SRC})
add_library(FDK ${FDK_SRC})
add_library(MpegTPDec ${MPEGTPDEC_SRC})
add_library(MpegTPEnc ${MPEGTPENC_SRC})
add_library(PCMutils ${PCMUTILS_SRC})
add_library(SBRdec ${SBRDEC_SRC})
add_library(SYS ${SYS_SRC})
add_library(SBRenc ${SBRENC_SRC})
add_library(ArithCoding ${ARITHCODING_SRC})
add_library(DRCdec ${DRCDEC_SRC})
add_library(SACdec ${SACDEC_SRC})
add_library(SACenc ${SACENC_SRC})

add_library(fdk-aac ${libfdk_aac_SOURCES})

add_executable(aac-enc ${libfdk_aac_SOURCES} ${aac_enc_SOURCES})

target_include_directories (AACdec PUBLIC ${FDK_AAC_INCLUDES})
target_include_directories (AACenc PUBLIC ${FDK_AAC_INCLUDES})
target_include_directories (FDK PUBLIC ${FDK_AAC_INCLUDES})
target_include_directories (MpegTPDec PUBLIC ${FDK_AAC_INCLUDES})
target_include_directories (MpegTPEnc PUBLIC ${FDK_AAC_INCLUDES})
target_include_directories (PCMutils PUBLIC ${FDK_AAC_INCLUDES})
target_include_directories (SBRdec PUBLIC ${FDK_AAC_INCLUDES})
target_include_directories (SYS PUBLIC ${FDK_AAC_INCLUDES})
target_include_directories (SBRenc PUBLIC ${FDK_AAC_INCLUDES})
target_include_directories (ArithCoding PUBLIC ${FDK_AAC_INCLUDES})
target_include_directories (DRCdec PUBLIC ${FDK_AAC_INCLUDES})
target_include_directories (SACdec PUBLIC ${FDK_AAC_INCLUDES})
target_include_directories (SACenc PUBLIC ${FDK_AAC_INCLUDES})

target_include_directories (fdk-aac PUBLIC ${FDK_AAC_INCLUDES})

target_include_directories (aac-enc PUBLIC ${FDK_AAC_INCLUDES})

set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT aac-enc)
