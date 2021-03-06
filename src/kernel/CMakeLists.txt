#cmake file for project kernel
#author:T
#created:2015-05-12 15:07:04

INCLUDE_DIRECTORIES(
    "${PROJECT_SOURCE_DIR}/src/Public"
    "${PROJECT_SOURCE_DIR}/src/API"
    "${PROJECT_SOURCE_DIR}/src/kernel"
    "${PROJECT_SOURCE_DIR}/src/kernel/interface"
    "${PROJECT_SOURCE_DIR}/src/kernel/net/"
    "${PROJECT_SOURCE_DIR}/src/kernel/net/epoll"
    "${PROJECT_SOURCE_DIR}/src/kernel/net/iocp"
    )

SET(KERNEL_INTERFACE
    "${PROJECT_SOURCE_DIR}/src/kernel/interface/ICore.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/interface/IConfigmgr.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/interface/ILogicmgr.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/interface/INetengine.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/interface/ITimermgr.h"
    )

SET(KERNEL_CONFIG_MGR
    "${PROJECT_SOURCE_DIR}/src/kernel/configmgr/Configmgr.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/configmgr/Configmgr.cpp"
    )

SET(KERNEL_EPOLLER
    "${PROJECT_SOURCE_DIR}/src/kernel/net/epoll/Pipe.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/net/epoll/CPipe.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/net/epoll/CPipe.cpp"
    "${PROJECT_SOURCE_DIR}/src/kernel/net/epoll/SPipe.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/net/epoll/SPipe.cpp"
    "${PROJECT_SOURCE_DIR}/src/kernel/net/epoll/epollheader.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/net/epoll/epoller.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/net/epoll/epoller.cpp"
    "${PROJECT_SOURCE_DIR}/src/kernel/net/epoll/epollWorker.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/net/epoll/epollWorker.cpp"
    )

SET(KERNEL_IOCPER
    "${PROJECT_SOURCE_DIR}/src/kernel/net/Header.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/net/iocp/iocper.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/net/iocp/iocper.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/net/iocp/iocper.cpp"
    "${PROJECT_SOURCE_DIR}/src/kernel/net/iocp/iocpworker.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/net/iocp/iocpworker.cpp"
    "${PROJECT_SOURCE_DIR}/src/kernel/net/iocp/iocphead.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/net/iocp/iocphead.cpp"
    "${PROJECT_SOURCE_DIR}/src/kernel/net/iocp/Pipe.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/net/iocp/CPipe.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/net/iocp/CPipe.cpp"
    "${PROJECT_SOURCE_DIR}/src/kernel/net/iocp/SPipe.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/net/iocp/SPipe.cpp"
    )

SET(KERNEL_LOGIC_MGR
    "${PROJECT_SOURCE_DIR}/src/kernel/logicmgr/Logicmgr.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/logicmgr/Logicmgr.cpp"
    )

SET(KERNEL_TIMER_MGR
    "${PROJECT_SOURCE_DIR}/src/kernel/timermgr/TimeNode.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/timermgr/TimeNode.cpp"
    "${PROJECT_SOURCE_DIR}/src/kernel/timermgr/Timermgr.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/timermgr/Timermgr.cpp"
    "${PROJECT_SOURCE_DIR}/src/kernel/timermgr/TimeSlot.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/timermgr/TimeSlot.cpp"
    )

SET(KERNEL_LOGGER
    "${PROJECT_SOURCE_DIR}/src/kernel/logger/Logger.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/logger/Logger.cpp"
    )

SET(KERNEL
    "${PROJECT_SOURCE_DIR}/src/kernel/Kernel.h"
    "${PROJECT_SOURCE_DIR}/src/kernel/Kernel.cpp"
    "${PROJECT_SOURCE_DIR}/src/kernel/main.cpp"
)
   
SOURCE_GROUP(API FILES ${API})
SOURCE_GROUP(Public\\tinyxml FILES ${TINYXML})
SOURCE_GROUP(Public FILES ${PUBLIC})

SOURCE_GROUP(src\\interface FILES ${KERNEL_INTERFACE})
SOURCE_GROUP(src\\configmgr FILES ${KERNEL_CONFIG_MGR})
SOURCE_GROUP(src\\logicmgr FILES ${KERNEL_LOGIC_MGR})
SOURCE_GROUP(src\\timermgr FILES ${KERNEL_TIMER_MGR})
SOURCE_GROUP(src\\iocper FILES ${KERNEL_IOCPER})
SOURCE_GROUP(src\\epoller FILES ${KERNEL_EPOLLER})
SOURCE_GROUP(src\\logger FILES ${KERNEL_LOGGER})
SOURCE_GROUP(src FILES ${KERNEL})

IF(UNIX)
ADD_EXECUTABLE(Kernel
        ${API}
        ${TINYXML}
        ${PUBLIC}
        ${KERNEL_INTERFACE}
        ${KERNEL_CONFIG_MGR}
        ${KERNEL_LOGIC_MGR}
        ${KERNEL_TIMER_MGR}
        ${KERNEL_EPOLLER}
        ${KERNEL_LOGGER}
        ${KERNEL}
        )
ENDIF(UNIX)

IF(WIN32)
ADD_EXECUTABLE(Kernel
        ${API}
        ${TINYXML}
        ${PUBLIC}
        ${KERNEL_INTERFACE}
        ${KERNEL_CONFIG_MGR}
        ${KERNEL_LOGIC_MGR}
        ${KERNEL_TIMER_MGR}
        ${KERNEL_IOCPER}
        ${KERNEL_LOGGER}
        ${KERNEL}
        )
ENDIF(WIN32)
IF(UNIX)
SET(EXECUTABLE_OUTPUT_PATH "${PROJECT_SOURCE_DIR}/build/linux")
ENDIF(UNIX)

IF(WIN32)
SET(EXECUTABLE_OUTPUT_PATH "${PROJECT_SOURCE_DIR}/build/windows")
ENDIF(WIN32)

TARGET_LINK_LIBRARIES(Kernel ${STATIC_LIBRARYS})


