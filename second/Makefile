#Trying to run the default Hello World program:
# run: hello
# 	./hello
# hello: c.c
# 	gcc -g -o hello c.c
#The same commands but with automatic vars:
VPATH = source headers
#Told make to look for the source files in source folder
.PHONY: run
run: hello cpp experiment
	./hello 
	echo "Now running cpp:"
	./cpp
	echo "Now running experiment:"
	./experiment

hello: c.c c.h
	gcc -I headers -g -o $@ $<

cpp: cpp.o cpp.h
	g++ -I headers -g -o $@ $<

cpp.o: c.cc cpp.h
	g++ -I headers -g -c $< -o $@

experiment: experiment.c c.h
	gcc -I headers -g -o $@ $< 
#the is that we have to specify the -g option to create information about debugging
#specifying the .PHONY to some target means, that the target is not a real file, + updating that
#target will be done each time it is called, not only when it's prerequisites were changed = an 
#embedded script into a makefile:
.PHONY: clean
clean: #each time the clean is called, it executes it's commands, even if the file clean exists
	rm -f *.o *.s hello cpp experiment

