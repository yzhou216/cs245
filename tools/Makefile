# Makefile template
# Based on https://www.cs.swarthmore.edu/~newhall/unixhelp/javamakefiles.html
JC = javac
JFLAGS = -g
.SUFFIXES: .java .class
.java.class:
	$(JC) $(JFLAGS) $*.java

CLASSES = Demo.java

default: classes

classes: $(CLASSES:.java=.class)

clean:
	$(RM) *.class
