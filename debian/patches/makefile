Description: simple Makefile fixes
Author: Baruch Even <baruch@debian.org>

Various minor Makefile fixes. Not separating to patches, as to avoid a set
of conflicting patches.

* Have man pages reside under /usr/*share*/man .
* Avoid using the names CFLAGS and LDFLAGS, as cdbs may override them
  (#376470).
* Add the extra object term.c (should be part of patch term_size_get).
* No stripping.

--- bidiv-1.5.orig/Makefile
+++ bidiv-1.5/Makefile
@@ -1,28 +1,27 @@
 PREFIX=/usr/local
 BIN_DIR=$(PREFIX)/bin
-MAN_PATH=$(PREFIX)/man
+MAN_PATH=$(PREFIX)/share/man
 CC_OPT_FLAGS=-O2 -Wall
 
 
-CFLAGS= $(CC_OPT_FLAGS) $(DEFS) `fribidi-config --cflags`
-LDFLAGS=`fribidi-config --libs`
+PKG_CFLAGS= $(CC_OPT_FLAGS) $(DEFS) `fribidi-config --cflags`
+PKG_LDFLAGS=`fribidi-config --libs`
 
 all: bidiv
 
-bidiv: bidiv.o
-	$(CC) -o bidiv bidiv.o $(LDFLAGS)
+bidiv: bidiv.o term.o
+	$(CC) -o bidiv bidiv.o term.o $(PKG_LDFLAGS) $(LDFLAGS)
 
 clean:
-	rm -f bidiv.o *~
+	rm -f bidiv.o *~ bidiv term.o
 
 clobber: clean
 	rm -f bidiv
 
 .c.o:
-	$(CC) -c $(CFLAGS) $<
+	$(CC) -c $(PKG_CFLAGS) $(CFLAGS) $<
 
 install: all
-	strip bidiv
 	cp bidiv $(BIN_DIR)
 	chmod 755 $(BIN_DIR)/bidiv
 	cp bidiv.1 $(MAN_PATH)/man1/bidiv.1
