################################################################################
# GNUmakefile for the LUXSim tools
#
# Change log:
# 17 March 2010 - Initial submission (Melinda)
# 20 April 2010 - Added LUXExampleAnalysis (Melinda)
# 22 April 2010 - Added LUXRoot2Dat and a -gstabs for macosx to
#                 get rid of .dSYM bundles created on OS X (Michael Woods)
# 27 Sep 2010 - Added LUXExampleAnalysis and NMDAnalysis to the cleanup section
#		(Kareem)
# 14 Feb 2012 - Removed funny ^M newline characters, and added LUXAsciiReader
#		(Matthew)
# 15 Aug 2012 - Changed order of arguments and corrected LIBDIRS to match
#               needs of latest g++ (Rich)
# 11 May 2015 - Removed the -g flag from the compilation, as well as the -gstabs
#               flag from the linking (Kareem)
################################################################################

CC			 = g++
CCFLAGS		 = -O2
INCLUDE		 = -I$(ROOTSYS)/include

ifeq ($(OSTYPE),darwin)
OSFLAGS	= -bind_at_load
endif

ifdef ROOTSYS
COMPILEJOBS	= LUXAsciiReader LUXRootReader LUXExampleAnalysis NMDAnalysis LUXSim2evt
ROOTLIBS	= $(shell $(ROOTSYS)/bin/root-config --libs)
LIBDIRS		= -L$(shell $(ROOTSYS)/bin/root-config --libdir)
INCLUDE		= -I$(shell $(ROOTSYS)/bin/root-config --incdir)
LDFLAGS		= $(shell $(ROOTSYS)/bin/root-config --ldflags)
PLATFORM	= $(shell $(ROOTSYS)/bin/root-config --platform)
OBJLIST		= LUXAsciiReader.o LUXRootReader.o LUXExampleAnalysis.o NMDAnalysis.o
endif

#ifeq ($(PLATFORM), macosx)
#OSFLAGS 	+=  -gstabs
#endif

ALLFLAGS	= $(CCFLAGS) $(LDFLAGS) $(OSFLAGS) $(INCLUDE)
ALLLIBS		= $(LIBDIRS) $(ROOTLIBS)

All:		$(COMPILEJOBS)

LUXAsciiReader:		LUXAsciiReader.cc
			$(CC) LUXAsciiReader.cc $(ALLFLAGS) $(ALLLIBS) -o LUXAsciiReader

LUXRootReader:          LUXRootReader.cc
			$(CC) LUXRootReader.cc $(ALLFLAGS) $(ALLLIBS) -o LUXRootReader

LUXExampleAnalysis:	LUXExampleAnalysis.cc
			$(CC)  LUXExampleAnalysis.cc $(ALLFLAGS) $(ALLLIBS) -o LUXExampleAnalysis

NMDAnalysis:		NMDAnalysis.cc
			$(CC) NMDAnalysis.cc $(ALLFLAGS) $(ALLLIBS) -o NMDAnalysis

.PHONY: LUXSim2evt
LUXSim2evt:		
			@cd LUXSim2evt && make #-C LUXSim2evt
			@#cd LUXSim2evt && make -B

neat:
		rm -rf *.o

cleanup:
		rm -rf *.o LUXAsciiReader LUXRootReader LUXExampleAnalysis NMDAnalysis LUXSim2evt/LUXSim2evt


