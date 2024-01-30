# # # #Some simple constants:
# # # CC := 0 
# # # #undeclare the default declarations
# # # MAKE_D = $(CC) -M
# # # MAKE_D_1 := $(CC) -M
# # # #The variable MAKE_D expands when it's used, while MAKE_D_1 expands at the declaration
# # # #To see the diff:

# # # CC := gcc
# # # p: 
# # # 	echo $(MAKE_D)
# # # 	echo $(MAKE_D_1)

# # # MKDIR := mkdir -p
# # # #internal vars:
# # # sources = *.c
# # # objects = $(subst .c, .o, $(sources))

# # # # LIBRARY = libio.a #This variable contains a trailing space
# # # # missing_file: 
# # # # 	touch $(LIBRARY)
# # # # 	ls -alF | grep "$(LIBRARY)"
# # # # In this case the variable CC has been defined above, so the expansion should make to gcc -M:
# # # VAR_1 := $(CC) -M
# # # MAKE_DEPEND = $(CC) -M
# # # print: 
# # # 	echo $(VAR_1) 
# # # 	echo $(MAKE_DEPEND)

# # # VAR_2 := $(CCC) -M 
# # # # In the case above the CCC var was not defined, so it will be expanded to nothing + -M
# # # print_2: 
# # # 	echo $(VAR_2)
# # C = 14
# # #The variable C is defined, it has a value:
# # C ?= 24
# # print:
# # 	echo $(C)
# # # C = $(C) + 4

# # # here makefile returns an error, since the var can not reference itself
# # C += 4
# # pr:
# # 	echo $(C)
# # #The output is 14
# # #Another way to declare some variables is: 
# # #Let's assume we have a multiple-line script to execute:
# # echo Creating something...
# # echo Starting the build...
# # $(RM) $(TMP_JAR_DIR)
# # $(MKDIR) $(TMP_JAR_DIR)
# # $(CP) -r $^ $(TMP_JAR_DIR)
# # cd $(TMP_JAR_DIR) && $(JAR) $(JARFLAGS) $@ .
# # $(JAR) -ufm $@ $(MANIFEST)
# # $(RM) $(TMP_JAR_DIR)
# # #Now to not define it 10 thousand times, we could use a macro:
# # define create-jar 
# # 	echo Creating something...
# # 	echo Starting the build...
# # 	$(RM) $(TMP_JAR_DIR)
# # 	$(MKDIR) $(TMP_JAR_DIR)
# # 	$(CP) -r $^ $(TMP_JAR_DIR)
# # 	cd $(TMP_JAR_DIR) && $(JAR) $(JARFLAGS) $@ .
# # 	$(JAR) -ufm $@ $(MANIFEST)
# # 	$(RM) $(TMP_JAR_DIR)
# # endef
# # #now the macro create-jar contains all the code lines above

# # OUTPUT_DIR := /tmp 
# # $(OUTPUT_DIR)/very_big_file:
# # 	$(free-space)

# # define free-space
# # 	$(PRINTF) "Freeing disk space"
# # 	$(DF) . | $(AWK) 'NR == 2 { print $$4}'
# # endef
# # BIN := /usr/bin 
# # PRINTF := $(BIN)/printf 
# # DF := $(BIN)/df 
# # # AWK := $(BIN)/awk

# ifdef COM
# 	SOURCES := /home/swiatoslaw/Documents/testing
# else
# 	SOURCES := /home/swiatoslaw/Documents/coding
# endif
# #You have to use correct vars, you dummy!!!
# #echo $(CC)
# # echo $(CFLAGS)
# display:
# 	echo "Executed correctly"
# 	echo $(PATH)
# 	echo $(SOURCES)
# #echo $(SOURCES)
# # echo $(PWD)
# # The rule above should display the "gcc"



%.o: %.cpp
	$(COMPILE.C) $(OUTPUT_OPTION) $<
%: %.o
	$(LINK.o) $^ $(LOADLIBES) $(LDLIBS) -o $@

COMPILE.C = $(COMPILE.cc)
COMPILE.cc = $(CXX) $(CXXFLAGS) $(CPPFLAGS) $(TARGET_ARCH) -c
CXX = g++
OUTPUT_OPTION = -o $@
#Linking:
LINK.o = $(CC) $(LDFLAGS) $(TARGET_ARCH)
CC = gcc 
#The default c++ linker is gcc
#The variables LDFLAGS and TARGET_ARCH have no default value
c.o: c.cpp
c: c.o

run: c
	./c