INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR})

INCLUDE(${QT_USE_FILE})
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fopenmp")

# .cxx sources
SET(HCD_SRCS_CXX
  hcd.cpp
  main.cpp
)

# files which need to be moc'd by Qt
SET(HCD_MOC_SRCS
  
)

# this moc's the above variable and appends to the cxx sources
QT4_WRAP_CPP(HCD_SRCS_CXX ${HCD_MOC_SRCS})

IF(UNIX)
  ADD_EXECUTABLE(hcd_p ${HCD_SRCS_CXX})
ELSEIF(APPLE)
  ADD_EXECUTABLE(hcd_p MACOSX_BUNDLE ${HCD_SRCS_CXX})
ELSEIF(WIN32)
  ADD_EXECUTABLE(hcd_p WIN32 ${HCD_SRCS_CXX})
ENDIF()

TARGET_LINK_LIBRARIES(hcd_p ${QT_LIBRARIES})
