MCS_BUILD_DIR = ../../../build

thisdir = class/Facades/netstandard
SUBDIRS = 
include $(MCS_BUILD_DIR)/rules.make

LIBRARY_SUBDIR = Facades
LIBRARY_INSTALL_DIR = $(mono_libdir)/mono/$(FRAMEWORK_VERSION)/Facades

LIBRARY = netstandard.dll

KEYFILE = ../../Open.snk
LIBRARY_SNK = $(KEYFILE)
SIGN_FLAGS = /delaysign /nowarn:1616,1699 /nowarn:618
LIB_REFS = System System.Xml System.Xml.Linq System.Runtime.Serialization System.Core System.Numerics System.Numerics.Vectors System.Net.Http System.Transactions \
System.IO.Compression System.Data System.ComponentModel.Composition System.IO.Compression.FileSystem

LIB_MCS_FLAGS = $(SIGN_FLAGS) $(EXTRA_LIB_MCS_FLAGS)

ifeq ($(PROFILE),xammac_net_4_5)
LIB_REFS += System.Web.Services Facades/System.Drawing.Primitives
else ifeq (2.1, $(FRAMEWORK_VERSION))
LIB_REFS += System.Web.Services
else
LIB_REFS += System.Web
endif

ifeq ($(PROFILE),monodroid)
# XA implements System.Drawing API inside Mono.Android
API_BIN_REFS := Mono.Android
endif

ifeq ($(PROFILE),monotouch)
API_BIN_REFS := Xamarin.iOS OpenTK-1.0
endif

ifeq ($(PROFILE),monotouch_tv)
API_BIN_REFS := Xamarin.TVOS OpenTK-1.0
endif

ifeq ($(PROFILE),monotouch_watch)
API_BIN_REFS := Xamarin.WatchOS
endif

ifeq ($(PROFILE),xammac)
API_BIN_REFS := Xamarin.Mac OpenTK
endif

# profiles which build a System.Drawing.dll in the repo
REPO_DRAWING_DEP := $(filter net_4_x orbis winaot unreal wasm, $(PROFILE))

ifdef REPO_DRAWING_DEP
LIB_REFS += System.Drawing
endif

PLATFORM_DEBUG_FLAGS =

NO_TEST = yes

include $(MCS_BUILD_DIR)/library.make


