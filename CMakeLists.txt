cmake_minimum_required(VERSION 3.30)
project(FreeRTOS_Simulator C)

set(CMAKE_C_STANDARD 11)

add_executable(app

        ${CMAKE_CURRENT_SOURCE_DIR}/FreeRTOS-Kernel/croutine.c
        ${CMAKE_CURRENT_SOURCE_DIR}/FreeRTOS-Kernel/event_groups.c
        ${CMAKE_CURRENT_SOURCE_DIR}/FreeRTOS-Kernel/list.c
        ${CMAKE_CURRENT_SOURCE_DIR}/FreeRTOS-Kernel/queue.c
        ${CMAKE_CURRENT_SOURCE_DIR}/FreeRTOS-Kernel/stream_buffer.c
        ${CMAKE_CURRENT_SOURCE_DIR}/FreeRTOS-Kernel/tasks.c
        ${CMAKE_CURRENT_SOURCE_DIR}/FreeRTOS-Kernel/timers.c
        ${CMAKE_CURRENT_SOURCE_DIR}/FreeRTOS-Kernel/portable/MemMang/heap_5.c
        ${CMAKE_CURRENT_SOURCE_DIR}/FreeRTOS-Kernel/portable/MSVC-MingW/port.c

        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/AbortDelay.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/BlockQ.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/blocktim.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/countsem.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/crflash.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/crhook.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/death.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/dynamic.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/EventGroupsDemo.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/flop.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/GenQTest.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/integer.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/IntSemTest.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/MessageBufferAMP.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/MessageBufferDemo.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/PollQ.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/QPeek.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/QueueOverwrite.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/QueueSet.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/QueueSetPolling.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/semtest.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/StaticAllocation.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/StreamBufferDemo.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/StreamBufferInterrupt.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/TaskNotify.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/TaskNotifyArray.c
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/Minimal/TimerDemo.c

        code_coverage_additions.c
        Run-time-stats-utils.c
        main.c
        main_full.c
        main_blinky.c
)

target_link_libraries(app PRIVATE winmm)

add_compile_options(-DprojCOVERAGE_TEST=1)
target_compile_options(app PRIVATE -DprojCOVERAGE_TEST=1)
target_compile_options(app PRIVATE -DconfigTASK_NOTIFICATION_ARRAY_ENTRIES=3)

target_include_directories(app PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/config
        ${CMAKE_CURRENT_SOURCE_DIR}/Common/include
        ${CMAKE_CURRENT_SOURCE_DIR}/FreeRTOS-Kernel/include
        ${CMAKE_CURRENT_SOURCE_DIR}/FreeRTOS-Kernel/portable/MSVC-MingW
)

