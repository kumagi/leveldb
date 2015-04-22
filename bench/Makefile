CXX=gcc
OPTS=-O2 -DNDEBUG

default: all

all: sqlite3 kyotocabinet lmdb bdb sophia ntdb

## SQLite3
sqlite3: sqlite3/sqlite3.so sqlite3/sqlite3.a sqlite3/sqlite3.h
sqlite3/sqlite3.so: sqlite3/sqlite3.c sqlite3/sqlite3.h
	$(CXX) $(LDFLAGS) $(OPTS) -o $@ $< -shared -fPIC
sqlite3/sqlite3.a: sqlite3/sqlite3.c sqlite3/sqlite3.h
	$(CXX) $(LDFLAGS) $(OPTS) -c -o $@ $< -static

## KyotoCabinet
kyotocabinet: kyotocabinet/libkyotocabinet.a
kyotocabinet/libkyotocabinet.a: kyotocabinet/*.h kyotocabinet/*.c
	cd kyotocabinet/ && ./configure && make -j8

## LMDB
lmdb: lmdb/libraries/liblmdb/liblmdb.a
lmdb/libraries/liblmdb/liblmdb.a:
	git clone https://gitorious.org/mdb/mdb.git lmdb && cd lmdb/libraries/liblmdb && make -j

## bdb
bdb: db-6.1.19/build_unix/libdb.a
db-6.1.19/build_unix/libdb.a:
	cd db-6.1.19/build_unix/ && ../dist/configure && make -j

## sophia
sophia: sophia/libsophia.a
sophia/libsophia.a:
	git clone git@github.com:pmwkaa/sophia.git
	cd sophia && make

ntdb: ntdb.h

