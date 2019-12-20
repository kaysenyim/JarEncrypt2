ifeq ($(shell uname), Linux)
  CC         = g++ -fPIC 
  LIBLINK    = -shared 
  INCLUDEDIR = -I $(shell echo ${JAVA_HOME})/include -I $(shell echo ${JAVA_HOME})/include/linux
  TARGET     = liblinux.so
endif

ifeq ($(shell uname), Darwin)
  CC		     = g++ 
  LIBLINK    = -dynamiclib
  INCLUDEDIR = -I $(shell echo ${JAVA_HOME})/include -I $(shell echo ${JAVA_HOME})/include/darwin -I /usr/local/opt/openssl/include
  TARGET     = libdarwin.dylib
endif

OBJS = decrypt.o

$(TARGET):$(OBJS)
	$(CC) $(LIBLINK) -o $(TARGET) $(OBJS)

decrypt.o: decrypt.cpp
	$(CC) $(INCLUDEDIR) -c decrypt.cpp

.PHONY:clean
clean:
	rm $(TARGET) $(OBJS)
