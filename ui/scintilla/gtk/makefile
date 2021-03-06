# Make file for Scintilla on Linux or compatible OS
# Copyright 1998-2001 by Neil Hodgson <neilh@scintilla.org>
# The License.txt file describes the conditions under which this software may be distributed.
# This makefile assumes GCC 2.95.2 is used and changes will be needed to use other compilers.
# GNU make does not like \r\n line endings so should be saved to CVS in binary form.
# To build for GTK+ 2, define GTK2 on the make command line.

.SUFFIXES: .cxx .o .h .a
CC = g++
AR = ar
RANLIB = touch

ifeq ($(OSTYPE),darwin)
CC = c++
AR = ar
RANLIB = ranlib
endif

COMPLIB=../bin/scintilla.a

vpath %.h ../src ../include
vpath %.cxx ../src

INCLUDEDIRS=-I ../include -I ../src
CXXBASEFLAGS=-W -Wall -DGTK -DSCI_LEXER $(INCLUDEDIRS)

ifdef NOTHREADS
THREADFLAGS=-DG_THREADS_IMPL_NONE
else
THREADFLAGS=
endif

ifdef DEBUG
CXXFLAGS=-DDEBUG -g $(CXXBASEFLAGS) $(THREADFLAGS)
else
CXXFLAGS=-DNDEBUG -Os $(CXXBASEFLAGS) $(THREADFLAGS)
endif

ifdef GTK2
CONFIGFLAGS=pkg-config --cflags gtk+-2.0
else
CONFIGFLAGS=gtk-config --cflags
endif

.cxx.o:
	$(CC) `$(CONFIGFLAGS)` $(CXXFLAGS) -c $<

#++Autogenerated -- run src/LexGen.py to regenerate
#**LEXOBJS=\\\n\(\*.o \)
LEXOBJS=\
LexAda.o LexAsm.o LexAVE.o LexBaan.o LexBullant.o LexConf.o LexCPP.o \
LexCrontab.o LexCSS.o LexEiffel.o LexEScript.o LexFortran.o LexHTML.o \
LexLisp.o LexLout.o LexLua.o LexMatlab.o LexOthers.o LexPascal.o LexPerl.o \
LexPOV.o LexPython.o LexRuby.o LexSQL.o LexVB.o 
#--Autogenerated -- end of automatically generated section

# The LEXOBJS have to be treated specially as the functions in them are not called from external code

all: $(COMPLIB) $(LEXOBJS)

clean:
	rm -f *.o $(COMPLIB)

deps:
	$(CC) -MM `$(CONFIGFLAGS)` $(CXXFLAGS) *.cxx ../src/*.cxx >deps.mak

$(COMPLIB): DocumentAccessor.o WindowAccessor.o KeyWords.o StyleContext.o Document.o CallTip.o \
	ScintillaBase.o ContractionState.o Editor.o ExternalLexer.o PropSet.o PlatGTK.o \
	KeyMap.o LineMarker.o ScintillaGTK.o CellBuffer.o ViewStyle.o \
	RESearch.o Style.o Indicator.o AutoComplete.o UniConversion.o XPM.o
	$(AR) rc $@ $^
	$(RANLIB) $@

# Automatically generate header dependencies with "make deps"
include deps.mak
