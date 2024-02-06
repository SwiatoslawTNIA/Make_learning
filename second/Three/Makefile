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
.PHONY: run
run: $(OUTPUT_FILES)
	echo "Starting experiment:"
	./experiment
	echo "Starting c2:"
	./c2
	echo "Starting hello:"
	./hello
	echo "Starting cpp:"
	./cpp

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

