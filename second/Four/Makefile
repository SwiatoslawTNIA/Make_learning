CFILES=c2 hello experiment
CXX_FILES=cpp
OUTPUT_FILES=$(CFILES) $(CXX_FILES)
vpath %.c source
vpath %.h headers
vpath %.cc source
#c++
CXX:=g++
CXXFLAGS:=-I headers  -c -g3 -Wall -Wextra -Wpedantic 
OUTPUT_OPTION_CXX=-o $@
COMPILE.cc=$(CXXFLAGS) $(OUTPUT_OPTION_CXX)
#c
CC:=gcc
CFLAGS:=-I headers -c -g3 -Wall -Wextra -Wpedantic 
OUTPUT_OPTION=-o $@
COMPILE.c=$(CFLAGS) $(OUTPUT_OPTION)

%.o: %.c 
	$(CC) $(COMPILE.c) $<
	echo "created $@"
# %.o: %.c++
# 	$(CXX) $(COMPILE.cc) $<
# 	echo "created $@"
%.o: %.cc
	$(CXX) $(COMPILE.cc) $<
	echo "created $@"
#create rules:
#Testing the default values of the env vars, then reset the global var here, and echo again:
# ifdef LOLLY
# .PHONY: run
# run: $(OUTPUT_FILES)
# 	echo "Starting experiment:"
# 	./experiment
# 	echo "Starting c2:"
# 	./c2
# 	echo "Starting hello:"
# 	./hello
# 	echo "Starting cpp:"
# 	./cpp
# else
# 	VAL1=2
# 	VAL2=3
# 	ifeq ($(VAL1), $(VAL2))
# 		run:
# 			echo "Sorry, no files"
# 	else
# 		run:
# 			echo "Else nothing changes."
# 	endif
# endif
# A little bit of funcs:
#1.String funcs:
STR1 := c.c c1.h c1.c c2.h c3.h ...
# STR1_NOT = $(filter-out %.c, $(STR1))
# #the findstring func:
# FOUND = $(findstring ..., $(STR1))
# FOUND_NOT = $(findstring ..., $(filter %.c, $(STR1)))
# SUBSTITUTED = $(subst .h,.p,$(STR1))
# #Delete all "c" letters:
# DELETE_C = $(patsubst c%,,$(STR1))
# default: #The default target:
# 	@echo "The STR1: $(STR1)"	
# 	@echo "The filter: $(filter %.c, $(STR1))"
# 	@echo "The STR1_NOT: $(STR1_NOT)"
# 	@echo "The FOUND: $(FOUND)"
# 	@echo "The FOUND_NOT: $(FOUND_NOT)"
# 	@echo "The SUBSTITUTED: $(SUBSTITUTED)"
# 	@echo "The DELETE_C: $(DELETE_C)"
# 	@echo
# 	@echo "My HOME dir has $(words $(subst /, ,$(HOME))) dirs"

#miscellaneous functions:

#A script to create a set of dirs if those don't exist:
# REQ_DIRS := 
# A := jolly
# B := A
# #To test all vars are defined:
# VARS := A B C D 
# $(foreach i,$(VARS), \
# 	$(if $($i),,\
# 	$(shell echo $i has not value > /dev/stderr)))
# #TO select all the *.c files:
# $(if $(filter $(MAKE_VERSION), 3.80 4.3),,\
# 	$(error This makefile requires Makefile version 3.80))
# ALL_C_FILES :=$(wildcard *.cc */*.cc)
# Make_dirs:=	 $(shell for d in $(REQ_DIRS);\
# 							do \
# 								[[ -d $$d ]] || mkdir -p $$d; \
# 							done)
run:
	@echo $($(B))
	$(error You can't stop me!!!)
	@echo $(sort $(STR1))
	@echo "All files of .cc extension: $(ALL_C_FILES)"
	$(Make_dirs)
#Individual words manipulation:
#The function to get the user_id;
user_id: $(wordlist 3,4,\
						$(subst :, , \
							$(shell grep "^$1:" /etc/passwd)))
def: 
	@echo "calling the user_id func:"
	$(call $(user_id), $(USERNAME))
#Can't find the solution
	@echo "The amount of words in STR1 var: $(words $(STR1))" 
#Output: 6
	@echo "The 1 word of STR1: $(word 1,$(STR1))"
#Output: c.c
	@echo "The last word of STR1: $(word $(words $(STR1)), $(STR1))"


c2.o: c.h
cpp.o:cpp.h
hello.o: c.h
experiment.o: c.h
#Linking:
c2: c2.o
	$(CC) $(OUTPUT_OPTION) $^

hello: hello.o
	$(CC) $(OUTPUT_OPTION) $^

experiment: experiment.o
	$(CC) $(OUTPUT_OPTION) $^

cpp: cpp.o
	$(CXX) $(OUTPUT_OPTION_CXX) $^

.INTERMEDIATE: hello.o experiment.o c2.o cpp.o 
.PHONY: clean

clean:
	rm -f *.o $(OUTPUT_FILES)
#Build dependencies:
.PHONY: buildC
buildC: $(CFILES)
	$(CC) $(CFLAGS) -M  $^ >> $@

.PHONY: buildCXX
buildCXX: $(CXX_FILES)
	$(CXX) $(CXXFLAGS) -M  $^ >> $@

depend: buildC buildCXX
	echo "Building dependencies:..."
	cat ./buildC >> $@
	cat ./buildCXX >> $@

