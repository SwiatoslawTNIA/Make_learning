#Trying to run the default Hello World program:
# run: hello
# 	./hello
# hello: c.c
# 	gcc -g -o hello c.c
#The same commands but with automatic vars:
# VPATH = source headers
vpath %.c source
vpath %.h headers
vpath %.cc source

#Told make to look for the source files in source folder
.PHONY: run
run: hello cpp experiment c2
	./hello 
	echo "Now running cpp:"
	./cpp
	echo "Now running experiment:"
	./experiment
	echo "Now running c2:"
	./c2

# hello: c.c c.h
# 	gcc -I headers -g -o $@ $<

# cpp: cpp.o cpp.h
# 	g++ -I headers -g -o $@ $<

# cpp.o: c.cc cpp.h
# 	g++ -I headers -g -c $< -o $@

# experiment: experiment.c c.h
# 	gcc -I headers -g -o $@ $< 

# c2: c2.c c.h
# 	gcc -I headers -g -o $@ $< 
#Le't try to write some rules:
%: %.c
	gcc -I headers -g -o $@ $<
%: %.o 
	g++ -I headers -g -o $@ $<
%.o: %.cc 
	g++ -I headers -g -c -o $@ $<
hello: c.h
cpp: cpp.h
cpp.o: cpp.h
experiment: c.h 
c2: c.h 
.INTERMEDIATE : cpp.o

#The rule below provides a sorted four column listing of the available make targets:
.PHONY: help
help:
@$(MAKE) --print-data-base --question no-such-target | \
$(GREP) -v -e '^no-such-target' -e '^makefile' |\
$(AWK) '/^[^.%][-A-Za-z0-9_]*:/\
{ print substr($$1, 1, length($$1)-1) }' |\
$(SORT) |\
$(PR) --omit-pagination --width=80 --columns=4\
#the is that we have to specify the -g option to create information about debugging
#specifying the .PHONY to some target means, that the target is not a real file, + updating that
#target will be done each time it is called, not only when it's prerequisites were changed = an 
#embedded script into a makefile:
.PHONY: clean
clean: #each time the clean is called, it executes it's commands, even if the file clean exists
	rm -f *.o *.s hello cpp experiment c2
#create a rule for generating dependencies:
.PHONY: depend #Now the file will be updated each time it is called.
depend: experiment.c c2.c hello.c
	gcc -I headers -M $(CPPFLAGS) $^ > $@
	more depend