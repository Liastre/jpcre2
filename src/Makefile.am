EXTRA_DIST =

EXTRA_DIST += \
  jpcre2.hpp \
  test_match.cpp \
  test_replace.cpp \
  test_match2.cpp \
  test_replace2.cpp \
  test_shorts.cpp \
  test16.cpp \
  test32.cpp \
  test0.cpp \
  test.cpp \
  testio.cpp \
  testme.cpp \
  testcovme.cpp \
  testmd.cpp

include_HEADERS = \
  jpcre2.hpp
  
noinst_PROGRAMS = 
TESTS =


JPCRE2_SOURCES = 

COVERAGE_FLAGS =
DISTCLEANFILES =


if WITH_TEST_SUIT

noinst_PROGRAMS += test_match2 test_replace2 test_match test_replace test_shorts
TESTS += test_match test_replace test_shorts

#Building test_match2
test_match2_SOURCES = \
  test_match2.cpp \
  $(JPCRE2_SOURCES)
test_match2_CXXFLAGS = \
  $(AM_CXXFLAGS) \
  $(AM_LDFLAGS)

#Building test_match
test_match_SOURCES = \
  test_match.cpp \
  $(JPCRE2_SOURCES)
test_match_CXXFLAGS = \
  $(AM_CXXFLAGS) \
  $(AM_LDFLAGS)

#Building test_replace
test_replace2_SOURCES = \
  test_replace2.cpp \
  $(JPCRE2_SOURCES)
test_replace2_CXXFLAGS = \
  $(AM_CXXFLAGS) \
  $(AM_LDFLAGS)

#Building test_replace2
test_replace_SOURCES = \
  test_replace.cpp \
  $(JPCRE2_SOURCES)
test_replace_CXXFLAGS = \
  $(AM_CXXFLAGS) \
  $(AM_LDFLAGS)

#Building test_shorts
test_shorts_SOURCES = \
  test_shorts.cpp \
  $(JPCRE2_SOURCES)
test_shorts_CXXFLAGS = \
  $(AM_CXXFLAGS) \
  $(AM_LDFLAGS)

noinst_PROGRAMS += test16
TESTS += test16

#Building test16
test16_SOURCES = \
  test16.cpp \
  $(JPCRE2_SOURCES)
test16_CXXFLAGS = \
  $(AM_CXXFLAGS) \
  $(AM_LDFLAGS)


noinst_PROGRAMS += test32
TESTS += test32

#Building test32
test32_SOURCES = \
  test32.cpp \
  $(JPCRE2_SOURCES)
test32_CXXFLAGS = \
  $(AM_CXXFLAGS) \
  $(AM_LDFLAGS)


noinst_PROGRAMS += test0
TESTS += test0

#Building test0
test0_SOURCES = \
  test0.cpp \
  $(JPCRE2_SOURCES)
test0_CXXFLAGS = \
  $(AM_CXXFLAGS) \
  $(AM_LDFLAGS)

noinst_PROGRAMS += test testio testme testmd
TESTS += test testio testme testmd

#Building test
test_SOURCES = \
  test.cpp \
  $(JPCRE2_SOURCES)
test_CXXFLAGS = \
  $(AM_CXXFLAGS) \
  $(AM_LDFLAGS) \
  $(COVERAGE_FLAGS)

#Building testio
testio_SOURCES = \
  testio.cpp \
  $(JPCRE2_SOURCES)
testio_CXXFLAGS = \
  $(AM_CXXFLAGS) \
  $(AM_LDFLAGS) \
  $(COVERAGE_FLAGS)

#Building testme
testme_SOURCES = \
  testme.cpp \
  $(JPCRE2_SOURCES)
testme_CXXFLAGS = \
  $(AM_CXXFLAGS) \
  $(AM_LDFLAGS) \
  $(COVERAGE_FLAGS)
  
#Building testmd
testmd_SOURCES = \
  testmd.cpp \
  $(JPCRE2_SOURCES)
testmd_CXXFLAGS = \
  $(AM_CXXFLAGS) \
  $(AM_LDFLAGS) \
  $(COVERAGE_FLAGS)


endif


if WITH_COVERAGE

noinst_PROGRAMS += testcovme

testcovme_SOURCES = testcovme.cpp $(JPCRE2_SOURCES)
testcovme_CXXFLAGS = \
  $(AM_CXXFLAGS) \
  $(AM_LDFLAGS) \
  $(COVERAGE_FLAGS)

COVERAGE_TEST_NAME = $(PACKAGE)
COVERAGE_NAME = $(PACKAGE)-$(VERSION)
COVERAGE_OUTPUT_FILE = $(COVERAGE_NAME)-coverage.info
COVERAGE_OUTPUT_DIR = $(COVERAGE_NAME)-coverage

COV_PROGS = $(TESTS)

#COVERAGE_LCOV_EXTRA_FLAGS =
#COVERAGE_GENHTML_EXTRA_FLAGS =

#coverage_quiet = $(coverage_quiet_$(V))
#coverage_quiet_ = $(coverage_quiet_$(AM_DEFAULT_VERBOSITY))
#coverage_quiet_0 = --quiet


coverage: $(COV_PROGS) jpcre2.hpp
	-$(LCOV) $(coverage_quiet) --zerocounters --directory $(top_builddir)
	for test in $(COV_PROGS); do \
	./$$test | true ; \
	done
	$(LCOV) --no-external --test-name "$(COVERAGE_TEST_NAME)" \
		--directory . \
		--directory "$(srcdir)" \
		--capture \
		--output-file "$(COVERAGE_OUTPUT_FILE)"
	mkdir -p "$(COVERAGE_OUTPUT_DIR)"
	$(GENHTML) -o "$(COVERAGE_OUTPUT_DIR)" "$(COVERAGE_OUTPUT_FILE)"

distclean-local:
	rm -f *.info *.gcno *.gcda
	rm -rf "$(COVERAGE_OUTPUT_DIR)"
covclean: distclean-local


# Without coverage support, still arrange for 'make distclean' to get rid of
# any coverage files that may have been left from a different configuration.

endif


if WITH_VALGRIND

check: $(TESTS)
	for test in $(TESTS); do \
	$(VALGRIND) --show-reachable=no --leak-check=full --track-origins=yes ./$$test ; \
	done

endif


if WITH_THREAD_TEST
thread_tests = test_pthread
noinst_PROGRAMS += test_pthread
#TESTS += test_pthread


#Building test_pthread
test_pthread_SOURCES = \
  test_pthread.cpp \
  $(JPCRE2_SOURCES)
test_pthread_CXXFLAGS = \
  $(AM_CXXFLAGS) \
  $(AM_LDFLAGS) 

if WITH_CPP11
thread_tests += teststdthread
noinst_PROGRAMS += teststdthread
#TESTS += teststdthread

#Building teststdthread
teststdthread_SOURCES = teststdthread.cpp $(JPCRE2_SOURCES)
teststdthread_CXXFLAGS = \
  $(AM_CXXFLAGS) \
  $(AM_LDFLAGS) 

endif

check-local: $(thread_tests)
	for test in $(thread_tests); do \
	$(VALGRIND) --tool=drd ./$$test ; \
	done
endif

