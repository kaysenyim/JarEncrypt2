ifeq ($(shell uname), Linux)
  CC         = g++ -fPIC 
  LIBLINK    = -shared 
  INCLUDEDIR = -I $(shell JAVA_HOME)/include -I $(shell JAVA_HOME)/include/linux
  TARGET     = libencrypt.so
endif

ifeq ($(shell uname), Darwin)
  CC		     = g++ 
  LIBLINK    = -dynamiclib
  INCLUDEDIR = -I $(shell JAVA_HOME)/include -I $(shell JAVA_HOME)/include/darwin
  TARGET     = libencrypt.dylib
endif

OBJS = encrypt.o

$(TARGET):$(OBJS)
	$(CC) $(LIBLINK) -o $(TARGET) $(OBJS)

encrypt.o: encrypt.cpp
	$(CC) $(INCLUDEDIR) -c encrypt.cpp

.PHONY:clean
clean:
	rm $(TARGET) $(OBJS)
