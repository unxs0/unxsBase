#
#FILE
#	unxsBase/unxsLib/Makefile
#	svn ID removed
#AUTHOR/LEGAL
#	(C) 2001-2017 Gary Wallis for Unixservice, LLC. GPLv2 license applies.
#
#NOTES
#	Work in progress try to create a library so we can remove all the unxsBind,
#	unxsRAD, etc., duplicated code here.
#

GIT_VERSION := $(shell git describe --dirty --always --tags)

CFLAGS=-Wall -DGitVersion=\"$(GIT_VERSION)\"
LIBS=-L/usr/lib/mysql -L/usr/lib64/mysql -L/usr/lib/openisp -L/usr/lib/oath -lmysqlclient -lz -lcrypt -lm -lssl -lucidr -ltemplate -loath -lunxsvz

install-libunxsvz: libunxsvz.a libunxsvz.h local.h
	mkdir -p /usr/lib/openisp
	mkdir -p /usr/include/openisp
	install libunxsvz.a /usr/lib/openisp/libunxsvz.a
	install libunxsvz.h /usr/include/openisp/unxsvz.h
	rm libunxsvz.a

libunxsvz.a: libunxsvz.o libunxsvz.h mysqlconnect.o local.h
	ar r libunxsvz.a libunxsvz.o

libunxsvz.o: libunxsvz.c libunxsvz.h mysqlconnect.o local.h
	cc -c libunxsvz.c -o libunxsvz.o $(CFLAGS)

mysqlconnect.o: mysqlconnect.c mysqlrad.h local.h
	cc -c mysqlconnect.c -o mysqlconnect.o $(CFLAGS)

clean:
	rm -f *.o

local.h: local.h.default
	@ if [ ! -f local.h ];then cp -i local.h.default local.h; fi

