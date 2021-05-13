NAME 		:= samtools
DIR_BUILD :=  $(realpath $(dir $(lastword $(MAKEFILE_LIST))))
DIR_SRC := $(realpath $(DIR_BUILD)/../../src)
DIR_INCLUDE :=$(realpath $(DIR_BUILD)/../../include)

ifeq ($(DIR_BUILD_CONFIG),)
export DIR_BUILD_CONFIG := $(realpath $(DIR_BUILD)/../../../../build-config/linux)
endif

include $(DIR_BUILD_CONFIG)/project.properties

# include the configuration details of any dependencies
-include $(DIR_BUILD)/user.prefs

export DIR_INSTALL=$(DIR_GRASSROOTS_INSTALL)/services

BUILD := debug


# BEGIN HTSLIB CONFIGURATION
ifneq ($(HTSLIB_HOME),)
DIR_HTSLIB := $(HTSLIB_HOME)
else
DIR_HTSLIB := /usr/local
endif
export DIR_HTSLIB_INC := $(DIR_HTSLIB)/include
export DIR_HTSLIB_LIB := $(DIR_HTSLIB)/lib
# END HTSLIB CONFIGURATION


VPATH := \
	$(DIR_SRC) \
	

INCLUDES := \
	-I$(DIR_INCLUDE) \
	-I$(DIR_GRASSROOTS_UUID_INC) \
	-I$(DIR_GRASSROOTS_UTIL_INC) \
	-I$(DIR_GRASSROOTS_UTIL_INC)/containers \
	-I$(DIR_GRASSROOTS_UTIL_INC)/io \
	-I$(DIR_GRASSROOTS_HANDLER_INC) \
	-I$(DIR_GRASSROOTS_NETWORK_INC) \
	-I$(DIR_GRASSROOTS_SERVICES_INC) \
	-I$(DIR_GRASSROOTS_SERVER_INC) \
	-I$(DIR_GRASSROOTS_PARAMS_INC) \
	-I$(DIR_GRASSROOTS_TASK_INC) \
	-I$(DIR_JANSSON_INC) \
	-I$(DIR_UUID_INC) \
	-I$(DIR_HTSLIB_INC)
	
SRCS := \
	paired_samtools_service.c \
	samtools_service.c \	
	

CPPFLAGS += -DSAMTOOLS_LIBRARY_EXPORTS 

LDFLAGS += -L$(DIR_JANSSON_LIB) -ljansson \
	-L$(DIR_HTSLIB_LIB) -lhts \
	-L$(DIR_GRASSROOTS_UTIL_LIB) -l$(GRASSROOTS_UTIL_LIB_NAME) \
	-L$(DIR_GRASSROOTS_UUID_LIB) -l$(GRASSROOTS_UUID_LIB_NAME) \
	-L$(DIR_GRASSROOTS_SERVICE_LIB) -l$(GRASSROOTS_SERVICE_LIB_NAME) \
	-L$(DIR_GRASSROOTS_NETWORK_LIB) -l$(GRASSROOTS_NETWORK_LIB_NAME) \
	-L$(DIR_GRASSROOTS_PARAMS_LIB) -l$(GRASSROOTS_PARAMS_LIB_NAME) \
	-lpthread


include $(DIR_BUILD_CONFIG)/generic_makefiles/shared_library.makefile

