#Trying to run the default Hello World program:
# run: hello
# 	./hello
# hello: c.c
# 	gcc -g -o hello c.c
#The same commands but with automatic vars:
VPATH = source headers
#Told make to look for the source files in source folder
run: hello cpp
	./hello 
	echo "Now running cpp:"
	./cpp

hello: c.c c.h
	gcc -g -o $@ $<

cpp: cpp.o cpp.h
	g++ -g -o $@ $<

cpp.o: c.cc cpp.h
	g++ -g -c $< -o $@

#the is that we have to specify the -g option to create information about debugging
#specifying the .PHONY to some target means, that the target is not a real file, + updating that
#target will be done each time it is called, not only when it's prerequisites were changed = an 
#embedded script into a makefile:
.PHONY: clean
clean: #each time the clean is called, it executes it's commands, even if the file clean exists
	rm -f *.o *.s hello cpp

