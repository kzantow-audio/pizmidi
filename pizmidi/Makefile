# This is a GNU Makefile. -ag

#========================================
# S e t t i n g s
#========================================

# Check for some common locations of the SDK files. This falls back to
# /usr/local/src/vstsdk if none of these are found. In that case, or if make
# picks the wrong location, you can also set the SDK variable explicitly. -ag
sdkpaths = /usr/local/include /usr/local/src /usr/include /usr/src
sdkpat = vst* VST*
#SDK = /usr/local/src/vstsdk
SDK = $(firstword $(wildcard $(foreach path,$(sdkpaths),$(addprefix $(path)/,$(sdkpat)))) /usr/src/vstsdk)
# Steinberg's distribution zip has the SDK source files in the
# public.sdk/source/vst2.x subdirectory, while some Linux packages (e.g.,
# steinberg-vst on the AUR) keep them directly under $(SDK).
#SDKSRC = $(SDK)/public.sdk/source/vst2.x
SDKSRC = $(firstword $(patsubst %/,%,$(dir $(wildcard $(addsuffix vstplugmain.cpp,$(SDK)/ $(SDK)/public.sdk/source/vst2.x/)))) $(SDK)/public.sdk/source/vst2.x)

CC = g++
SO = .so
OUT = ../Release/
FFLAGS = -fmessage-length=0 -finline-functions -fvisibility=hidden -fPIC -fno-rtti
# We should do something about all these warnings some time - ag.
CFLAGS = -Wall -Wno-multichar -Wno-char-subscripts -Wno-write-strings -Wno-parentheses -Wno-unused-but-set-variable -Os $(FFLAGS) -D__cdecl= -I$(dir $<) -I$(SDK) -I$(SDKSRC)
LDFLAGS = -Wall -s -shared

.DEFAULT_GOAL := all

#========================================
# O b j e c t s
#========================================
# (common)
#----------------------------------------
OBJP = PizMidi
OBJM = vstplugmain
OBJA = audioeffect
OBJX = audioeffectx
# OBJP needs to be a separate instance for each plugin -ag
#OBJC = $(OBJP).o $(OBJM).o $(OBJA).o $(OBJX).o
OBJC = $(OBJM).o $(OBJA).o $(OBJX).o

%-$(OBJP).o : common/$(OBJP).cpp
	$(CC) $(CFLAGS) -I$(patsubst %-$(OBJP).o, %, $@) -c $< -o $@

$(OBJM).o : common/$(OBJM).cpp
	$(CC) $(CFLAGS) -c $< -o $@

$(OBJX).o : $(SDK)/$(OBJX).cpp
	$(CC) $(CFLAGS) -c $< -o $@

$(OBJA).o : $(SDK)/$(OBJA).cpp
	$(CC) $(CFLAGS) -c $< -o $@
#----------------------------------------
# (output)
#----------------------------------------
OBJE = midi2qwerty16 midi16CCRouter midiAlias midiAudioToCC midiBlackKeyFilter midiCCModulator midiCCReset midiCCStepper midiCCToggle midiChannelFilter midiChannelize midiChordHold midiChordSplit midiChs_noGUI midiConverter3 midiDelay midiDuplicateBlocker midiExactDelay midiFingered midiForceToKey midiForceToRange midiInvertNotes midiKeySplit midiKeySplit4 midiNotchFilter midiNoteGroups midiNotesToCC midiNoteToggle midiNRPNConverter midiOverlappingNoteKiller midiPitchBendQuantize midiPolyphony midiProbability midiProgramChange midiScaleChanger midiSimpleLFO midiSostenuto midiStrum midiStuckNoteKiller midiSwing midiTranspose midiTriggerList midiVelocityScale

#========================================
# B u i l d
#========================================
# all / clean
#----------------------------------------
all: $(addprefix $(OUT), $(addsuffix $(SO), $(OBJE)))

clean:
	rm -f *.o $(OUT)*.so

cleanobj:
	rm -f *.o
#----------------------------------------
# individual
#----------------------------------------
# This one needs special treatment (X11 libs). -ag
$(OUT)midi2qwerty16$(SO): LDFLAGS = -Wall -s -shared -L/usr/X11R6/lib

# Generic rules for compiling all plugins. -ag
$(OUT)%$(SO): %.o %-$(OBJP).o $(OBJC)
	$(CC) $(LDFLAGS) $^ -o $@
%.o: %/*.cpp
	$(CC) $(CFLAGS) -c $^ -o $@
