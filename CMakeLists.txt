CMAKE_MINIMUM_REQUIRED (VERSION 3.10.1)

PROJECT (pbterm VERSION 0.0.1)

SET (CMAKE_VERBOSE_MAKEFILE ON)

set(CMAKE_CXX_STANDARD 17)

set(CMAKE_SYSTEM_NAME Linux)
set(CMAKE_SYSTEM_VERSION 1.0)
set(CMAKE_SYSTEM_PROCESSOR armv7a)
set(BUILD_SHARED_LIBS ON)

SET (TOOLCHAIN_PATH "../SDK/SDK-6.8/SDK-B300")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

set(CMAKE_FIND_ROOT_PATH "${TOOLCHAIN_PATH}/usr/arm-obreey-linux-gnueabi/sysroot/")
set(CMAKE_INCLUDE_PATH "/usr/include")
message("CMAKE_FIND_ROOT_PATH=${CMAKE_FIND_ROOT_PATH}")
set(CMAKE_FIND_ROOT_PATH_MODE_PROGRAM NEVER)
set(CMAKE_FIND_ROOT_PATH_MODE_INCLUDE ONLY)
set(CMAKE_FIND_ROOT_PATH_MODE_LIBRARY ONLY)
include_directories("${TOOLCHAIN_PATH}/usr/arm-obreey-linux-gnueabi/sysroot/usr/include/freetype2")
list(APPEND CMAKE_MODULE_PATH "${TOOLCHAIN_PATH}/usr/share/cmake/modules")
list(REMOVE_DUPLICATES CMAKE_MODULE_PATH)
set(QT_QMAKE_EXECUTABLE "${TOOLCHAIN_PATH}/usr/arm-obreey-linux-gnueabi/sysroot/usr/qt5/bin/qmake")
set(CMAKE_PREFIX_PATH "${TOOLCHAIN_PATH}/usr/arm-obreey-linux-gnueabi/sysroot/ebrmain/lib/cmake")

set(CMAKE_C_COMPILER "${TOOLCHAIN_PATH}/usr/bin/arm-obreey-linux-gnueabi-clang")
set(CMAKE_CXX_COMPILER "${TOOLCHAIN_PATH}/usr/bin/arm-obreey-linux-gnueabi-clang++")
set(CMAKE_C_FLAGS "-v -fsigned-char -Werror-return-type" CACHE STRING "" FORCE)
set(CMAKE_CXX_FLAGS "-v -Wl,--copy-dt-needed-entries -fsigned-char -Werror-return-type" CACHE STRING "" FORCE)
set(CMAKE_CXX_FLAGS_RELEASE "-DNDEBUG -O2 -pipe -fomit-frame-pointer -march=armv7-a -mtune=cortex-a8 -mfpu=neon -mfloat-abi=softfp " CACHE STRING "" FORCE)
set(CMAKE_C_FLAGS_RELEASE "-DNDEBUG -O2 -pipe -fomit-frame-pointer -march=armv7-a -mtune=cortex-a8 -mfpu=neon -mfloat-abi=softfp " CACHE STRING "" FORCE)
set(CMAKE_C_FLAGS_DEBUG "-DDEBUG -O0 -g -pipe -fomit-frame-pointer -march=armv7-a -mtune=cortex-a8 -mfpu=neon -mfloat-abi=softfp " CACHE STRING "" FORCE)
set(CMAKE_CXX_FLAGS_DEBUG "-DDEBUG -O0 -g -pipe -fomit-frame-pointer -march=armv7-a -mtune=cortex-a8 -mfpu=neon -mfloat-abi=softfp " CACHE STRING "" FORCE)
set(CMAKE_EXE_LINKER_FLAGS_RELEASE "-s " CACHE STRING "" FORCE)
set(CMAKE_SHARED_LINKER_FLAGS_RELEASE "-s" CACHE STRING "" FORCE)
set(CMAKE_SHARED_LINKER_FLAGS "-Wl,-z,defs" CACHE STRING "" FORCE)

add_definitions(-DPLATFORM_FC)
set(PB_PLATFORM "ARM" CACHE STRING "ARM|PC Readonly!")

set(CMAKE_INSTALL_PREFIX "${TOOLCHAIN_PATH}/usr/arm-obreey-linux-gnueabi/sysroot/usr/local" CACHE PATH "Installation Prefix")
set(CMAKE_BUILD_TYPE Release CACHE STRING "Debug|Release|RelWithDebInfo|MinSizeRel")
set(ENV{PKG_CONFIG_DIR} "")
set(ENV{PKG_CONFIG_LIBDIR} ${CMAKE_FIND_ROOT_PATH}/usr/lib/pkgconfig)
set(ENV{PKG_CONFIG_SYSROOT_DIR} ${CMAKE_FIND_ROOT_PATH})
set(ENV{LD_LIBRARY_PATH} ${TOOLCHAIN_PATH}/usr/lib)
list(APPEND PB_LINK_DIRECTORIES "${TOOLCHAIN_PATH}/usr/arm-obreey-linux-gnueabi/sysroot/usr/lib")
list(APPEND PB_LINK_DIRECTORIES "${TOOLCHAIN_PATH}/usr/arm-obreey-linux-gnueabi/sysroot/usr/local/lib")
list(APPEND PB_INCLUDE_DIRECTORIES "${TOOLCHAIN_PATH}/usr/arm-obreey-linux-gnueabi/sysroot/usr/include")

SET (SRC_LIST
	${CMAKE_SOURCE_DIR}/src/pbterm.cpp
	${CMAKE_SOURCE_DIR}/src/Messenger.cpp
    ${CMAKE_SOURCE_DIR}/src/Logger.cpp	
    ${CMAKE_SOURCE_DIR}/src/Config.cpp
    ${CMAKE_SOURCE_DIR}/src/Term.cpp	
    ${CMAKE_SOURCE_DIR}/src/Display.cpp
    ${CMAKE_SOURCE_DIR}/src/Keyboard_Handler.cpp
    ${CMAKE_SOURCE_DIR}/src/Button_Handler.cpp
    ${CMAKE_SOURCE_DIR}/src/Pointer_Handler.cpp
    ${CMAKE_SOURCE_DIR}/src/Lines.cpp
    ${CMAKE_SOURCE_DIR}/src/Line.cpp
    ${CMAKE_SOURCE_DIR}/src/Menu_Handler.cpp
    ${CMAKE_SOURCE_DIR}/src/Rotation_Handler.cpp
    ${CMAKE_SOURCE_DIR}/src/Submenu.cpp
#	${CMAKE_SOURCE_DIR}/src/Dir_Select_Handler.cpp
    ${CMAKE_SOURCE_DIR}/src/Utils.cpp)

ADD_EXECUTABLE (pbterm.app
		${SRC_LIST})
target_link_options(pbterm.app PRIVATE "LINKER:-v")
target_link_options(pbterm.app PRIVATE "LINKER:-copy-dt-needed-entries")
target_link_libraries(pbterm.app PRIVATE pthread inkview freetype stdc++fs z)

INSTALL (TARGETS pbterm.app)

#INCLUDE_DIRECTORIES(${TARGET_INCLUDE})
#TARGET_LINK_LIBRARIES (pbterm.app ${TARGET_LIB})


