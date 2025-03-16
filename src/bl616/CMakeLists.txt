cmake_minimum_required(VERSION 3.15)

include(proj.conf)

find_package(bouffalo_sdk REQUIRED HINTS $ENV{BL_SDK_BASE})

sdk_add_compile_definitions(-DCONFIG_CLI_CMD_ENABLE)
sdk_add_include_directories(. ../u8g2/csrc)

target_sources(app PRIVATE
   	wifi_tcp_client.c
   	wifi_tcp_server.c
   	mcu_hw.c
   	../core.c
   	../core_atarist.c
   	../core_c64.c
   	../core_vic20.c
   	../core_amiga.c
   	../core_atari2600.c
   	../hidparser.c
   	../hid.c
   	../inifile.c
   	../menu.c
   	../sdc.c
   	../osd_u8g2.c
   	../sysctrl.c
   	../config.c
   	../xml.c
)

file(GLOB COMPONENT_SRCS ../u8g2/csrc/*.c  ../u8g2/sys/bitmap/common/*.c)
target_sources(app PRIVATE ${COMPONENT_SRCS})

sdk_set_main_file(../main.c)

sdk_set_linker_script(bl616_flash.ld)
project(fpga_companion)
