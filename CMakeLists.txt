PROJECT ("ucos3-posix")
CMAKE_MINIMUM_REQUIRED(VERSION 2.8)
  
SET(TARGET_EXE "ucos3-posix")
SET(CMAKE_C_STANDARD 99)
SET(CMAKE_C_FLAGS_DEBUG "$ENV{CFLAGS} -static -O0 -g3 -Wall -fmessage-length=0  ")  #set debug mode c flags
SET(CMAKE_C_FLAGS_RELEASE "$ENV{CFLAGS} -O3 -Wall ")         #set release mode c flags
SET(CMAKE_BUILD_TYPE "Debug")     #set Debug or Release


### INCLUDE DIR ###
# Application
INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR}/app/Posix/GNU/OS3)

# Ucos-iii Kernel
INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR}/kernel/uC-CPU)
INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR}/kernel/uC-CPU/Posix/GNU)  
INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR}/kernel/uC-LIB)
INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR}/kernel/uCOS-III/Ports/Posix/GNU)
INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR}/kernel/uCOS-III/Source)


### SUB CMAKE DIR ###
# Ucos-iii Kernel
ADD_SUBDIRECTORY(kernel/uC-CPU/Posix/GNU)
ADD_SUBDIRECTORY(kernel/uC-CPU)
ADD_SUBDIRECTORY(kernel/uCOS-III/Source)
ADD_SUBDIRECTORY(kernel/uCOS-III/Ports/Posix/GNU)  
ADD_SUBDIRECTORY(kernel/uC-LIB)
  
# Application
AUX_SOURCE_DIRECTORY(app/Posix/GNU/OS3 APP_SRC)


### EXE ###
ADD_EXECUTABLE(${TARGET_EXE} ${APP_SRC})

### LINK LIBRARIES ###
SET_TARGET_PROPERTIES(${TARGET_EXE} PROPERTIES LINKER_LANGUAGE C)

# Target Link
TARGET_LINK_LIBRARIES(${TARGET_EXE} ucos-port ucos uclib cpu cpu-arch pthread)
